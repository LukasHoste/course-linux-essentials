# guide

- rasp pi OS niet full en niet lite op sd
- IP: 172.16.103.211
- MAC: ethernet: e4:5f:01:1d:73:b5 , wifi: e4:5f:01:1d:73:b6

- statische ip: 172.16.240.5 /16 default-gateway: 172.16.0.1

## user maken

sudo adduser lulu
sudo usermod -aG sudo lulu

## statisch ip voor bedraad

ifconfig eth0 192.168.1.5 netmask 255.255.255.0 up
route add default gw 192.168.1.1

## wifi instellen

sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=BE

network={
    ssid="YOURSSID"
    psk="YOURPASSWORD"
    scan_ssid=1
}
