# Linux final challenge

## flashing

```text
install raspberry pi imager
press CTRL SHIFT X andedit ssh, wifi and hostname settings.
choose os and storage and press write.
```


## headless system and ssh | Ip from mac

```text
Add a file "ssh" to the boot partition of the card.
Now we need to connect with ssh using the ip address. We can try using
raspberry as the ip but this most likely wont work.

mac-address (ethernet): e4:5f:01:1d:73:b5
To find out the ip we can use the command tcpdump -vvv -i -interface- | grep -mac-

Or use dhcpfilter and dhcpecho scripts. Grep can be used on a script to find the device with the correct mac.
Do this before plugging the ethernet cable into the pi as we want to
intercept dhcp packets.
```

default password is raspberry

## static ip

```text
sudo nano /etc/dhcpcd.conf
go to interface eth0
change static ip address to your ip and static routers to the default
gateway: can be found using route -n
```

## hostname

```text
sudo raspi-config
system options -> hostname -> enter the hostname -> enter -> finish
reboot for changes to take effect
```

## creating accounts

sudo adduser -name-

## creating groups

```text
sudo addgroup -name-
adding a user to the group: sudo adduser -username- -groupname
or
sudo usermod -aG -group/groups- -user-
```

## locking accounts

```text
sudo passwd -l -name-
sudo usermod --expiredate 1 -name-
```

## SSH using keys

```text
get the public key of your device (not the pi).
On windows: cd ~/.ssh -> cat id_rsa.pub same when using a linux machine
copy this.
connect to the pi using ssh -> create an ssh dir in the home dir -> mkdir ~/.ssh
nano ~/.ssh/authorized_keys -> paste the key
sudo chmod -R 600 ~/.ssh
sudo chmod 700 ~/.ssh
```

## setup default shell for an account

```text
chsh -s /bin/-shell-
```

## installing zsh

sudo apt install zsh

## wireless netwerk via command line


```text
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=BE

network={
    ssid="YOURSSID"
    psk="YOURPASSWORD"
    scan_ssid=1
}

sudo wpa_cli -i wlan0 reconfigure
```

## UFW firewall

```bash
sudo apt install ufw
sudo systemctl enable ufw
sudo ufw allow ssh
sudo systemctl start ufw
```

## apache

```bash
sudo apt install apache2
sudo ufw allow http

cd /var/www/html
```

To see if it is working go to the ip address of the device on another device.

## docker

```text
curl -sSL https://get.docker.com | sh
sudo adduser pi docker
sudo systemctl enable docker
sudo systemctl start docker
```

### running docker

```text
basic: sudo docker run hello-world -> sudo docker stop hello-world
sudo docker images to see installed images
sudo docker ps to see running containers
sudo docker run --detach --publish 4000:1880 --restart=always nodered/node-red
docker update --restart=no <naam van container> om de automatische restart te stoppen
```

## cron post

curl -X POST -d "stuff" site je pense

## creating dirs and files and setting up permissions and ownership

```text
create file -> touch -name-
create dir -> mkdir -name-

ownership file -> chown -user- -file-
ownership dir -> chown -R -username- -dir-

permissions file -> chmod ugo+rwx -file-
permissions dir -> chmod -R if you want to change the permissions of everything inside of it as well
```

## cloning git repos

```text
sudo apt install git
ssh-keygen
add the key on github
git clone <ssh thingy>
```

## installing with apt

```text
sudo apt install -package-
```

## mqtt broker

NOG NIET GEZIEN

## create regular backups of a directory with cron

### backups

use something simialar to this script

```bash
#!/usr/bin/env bash

now=$(date '+%F_%H'h'-%M'm'-%S's'')
# doesnt work when using %T ?

tar -czvf "oefeningen_${now}.tar.gz" $HOME/oefeningen
```

### cron backups

crontab -e
0 0 */1 * * tar -czvf "/tmp/home-backup.tar.gz" /home/lulu

