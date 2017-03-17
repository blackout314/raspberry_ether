# HOWTO RaspberryPi connect by usb0

## raspberry pi zero

### activate usb0

```
  echo "dtoverlay=dwc2" | sudo tee -a /boot/config.txt
  echo "dwc2" | sudo tee -a /etc/modules
  echo "g_ether" | sudo tee -a /etc/modules
```

### config network - add in /etc/network/interfaces
```
  allow-hotplug usb0
  iface usb0 inet static
    address 192.168.250.2
    netmask 255.255.255.0
    network 192.168.250.0
    broadcast 192.168.250.255
    gateway 192.168.250.1
```

### install isc-dhcp-server

```
  apt-get -y install isc-dhcp-server
```

### configure isc-dhcp-server

```
  subnet 192.168.250.0 netmask 255.255.255.0 {
    option broadcast-address 255.255.255.255;
    range 192.168.250.1 192.168.250.1;
  }
```

### update resolv.conf (add line)

```
  nameserver 8.8.8.8
```

### enable ssh (raspberry pi way)

```
  sudo raspi-config
```

## your laptop

### activate forward

```
  echo 1 > /proc/sys/net/ipv4/ip_forward
  iptables -t nat -A POSTROUTING -o $ETHX -j MASQUERADE
```

### plug usb

plug data usb (not power) to laptop
