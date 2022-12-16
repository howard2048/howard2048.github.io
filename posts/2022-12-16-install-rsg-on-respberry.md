# RSG Installation Guild

## Install OS on Respberry

## Install Docker

```shell
curl -fsSL https://get.docker.com -o get-docker.sh
DRY_RUN=1 sudo sh ./get-docker.sh
```

See [https://docs.docker.com/engine/install/debian/]().

## Install Docker Compose

```shell
apt-get update
#....
```

See ...

## Connect to Respberry

```shell
ssh landingsite@192.168.123.1
```

### Switch to user root
```shell
sudo su
```

### Set Wi-Fi

```shell
nano /etc/wpa_supplicant/wpa_supplicant.conf
```

```diff
network {
-  #ssid='_LandingSite_5G'
-  #psk="LandingSite2020!"
+  ssid='_LandingSite_5G'
+  psk="LandingSite2020!"  
}
```


### Set static IP address

```shell
sudo nano /etc/dhcpcd.conf
```

```diff
+ interface eth0
+ static ip_address=192.168.123.1/24
+ interface wlan0
+ static ip_address=192.168.0.100/24
```

### Reboot Respberry

```shell
reboot
```

#### Restart network
```
ifconfig eth0 down
ifconfit eth0 up
```


```shell
ssh-kengen -R 192.168.123.1
```

### Start docker

```shell
systemctl start docker
```


### Start Docker when boot

```
systemctl enable docker
```
