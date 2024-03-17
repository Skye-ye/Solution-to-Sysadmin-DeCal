# Solution to Lab6a

## Q1a

Running a ping command is not always sufficient to determine whether you can reach a server because it only tests ICMP (Internet Control Message Protocol) connectivity. Firewalls may block ICMP packets, a server may respond to ping but not offer specific services (like HTTP or SSH), and successful ping results do not guarantee that higher-level services are operational. Thus, while useful for basic connectivity checks, ping does not provide a complete picture of server accessibility.

## Q1b

1. `auto lo` means the loopback interface is automatically brought up at boot time.
2. `iface lo inet loopback` means loopback interface uses `IPv4` and it is mapped with the name "**loopback**".
3. If you delete these lines and reboot, the "loopback" interface will be lost and the `localhost` will not be able to be accessed.

## Q1c

```
auto test
iface test inet static
    address 192.168.13.37
    netmask 255.255.0.0
```

## Q2a

1. `tcp_syncookies`: This file is a tunable kernel parameter that controls the usage of TCP SYN cookies. This file has two states `0` for off and `1` for on. Enabling SYN cookies can be a useful defense against SYN flood attacks, especially on servers that are directly exposed to the internet and might be targeted by such attacks. 

2. `sysctl`: This option is a tool used to modify kernel parameters at runtime. For example:
   ```bash
   sudo sysctl -w net.ipv4.tcp_syncookies=1

## Q3a

1. You should add `hosts: dns files` to the "**/etc/nsswitch.conf** " file.

## Q3b

1. `n` should be set to 1.



## Exercise

