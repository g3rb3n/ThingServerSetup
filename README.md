
# Synopsis
Installer scripts for:
- Mosquitto 
- InfluxDB
- Node-RED
- Grafana

#
## Mosquitto
Standard ubuntu package

## InfluxDB
Standard ubuntu package

## Node-RED
nodesource.com version

## Grafana
The armhf package found on
https://github.com/fg2it/grafana-on-raspberry


# Procedure
IP=""

## Burn image

put SD card in laptop
```
sh write-img-to-disk

etcher-electron
```
put SD card in pi

## Change password and setup ssh
ssh root@IP
Change password
reboot
ssh-copy-id root@$IP

## Place scripts on SD
rsync -auv armbian root@$IP:~/

## Install
ssh root@$IP
chown -R root:root armbian
chmod -R +x armbian/install
cd armbian
sh install

## Tighten security
cp -a fs/* /

### Grafana
Goto http://<ip>:3000/ and log in with admin admin
Change password

### Node Red
Create a password hash
```
node-red-admin hash-pw
```
Change password in /home/nodered/.node-red/settings.js
Goto http://<ip>:1880/

### Mosquitto
```
mosquitto_passwd /etc/mosquitto/passwd admin
```

### Influx
Change password
