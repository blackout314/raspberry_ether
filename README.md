


# attivare il forward

```
  echo 1 > /proc/sys/net/ipv4/ip_forward
  iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
```
