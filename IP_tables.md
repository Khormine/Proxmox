# Configure IP tables:

## Configure bridge:

Edit the file `/etc/network/interfaces`:
```
auto vmbr2
iface vmbr2 inet static
        address  <@IP>
        netmask  <netmask>
        bridge_ports none
        bridge_stp off
        bridge_fd 0
 
        post-up echo 1 > /proc/sys/net/ipv4/ip_forward
        post-up   iptables -t nat -A POSTROUTING -s '<NETWORK>' -o vmbr1 -j MASQUERADE
        post-down iptables -t nat -D POSTROUTING -s '<NETWORK>' -o vmbr1 -j MASQUERADE
```

Restart networking:
```
$ systemtcl restart networking
```
https://kifarunix.com/configure-ubuntu-20-04-as-linux-router/
