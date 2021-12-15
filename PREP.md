# Linux final challenge

## flashing

install raspberry pi imager
press CTRL SHIFT X andedit ssh, wifi and hostname settings.
choose os and storage and press write.


## headless system and ssh | Ip from mac

Add a file "ssh" to the boot partition of the card.
Now we need to connect with ssh using the ip address. We can try using
raspberry as the ip but this most likely wont work.

mac-address (ethernet): e4:5f:01:1d:73:b5
To find out the ip we can use the command tcpdump -vvv -i -interface- | grep -mac-
Do this before plugging the ethernet cable into the pi as we want to
intercept dhcp packets.

## static ip

sudo nano /etc/dhcpcd.conf
go to interface eth0
change static ip address to your ip and static routers to the default
gateway

## hostname

sudo raspi-config
network options -> hostname -> enter the hostname -> enter -> finish
reboot for changes to take effect

## creating accounts

sudo adduser -name-

## creating groups

sudo addgroup -name-
adding a user to the group: sudo adduser -username- -groupname
or
sudo usermod -aG -group/groups- -user-

## locking accounts

sudo passwd -l -name-
usermod --expiredate 1 -name-

## SSH using keys

get the public key of your device (not the pi).
On windows: cd ~/.ssh -> cat id_rsa.pub
copy this.
connect to the pi using ssh -> (creat an ssh dir in the home dir) this should already exist.
nano ~/.ssh/authorized_keys -> paste the key
sudo chmod -R 600 ~/.ssh
sudo chmod 700 ~/.ssh

## setup default shell for an account

chsh -s /bin/-shell-

## installing zsh

sudo apt install zsh

## wireless netwerk via command line

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

## docker

curl -sSL https://get.docker.com | sh
sudo adduser pi docker
sudo systemctl enable docker
sudo systemctl start docker

## cron post

curl -X POST -d "stuff" site je pense

## creating dirs and files and setting up permissions and ownership

create file -> touch -name-
create dir -> mkdir -name-

ownership file -> chown -user- -file-
ownership dir -> chown -R -username- -dir-

permissions file -> chmod ugo+rwx -file-
permissions dir -> chmod -R if you want to change the permissions of everything inside of it as well

## cloning git repos

sudo apt install git
git clone (use the http if your devices key has not been added to github.com)

## installing with apt

sudo apt install -package-

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

