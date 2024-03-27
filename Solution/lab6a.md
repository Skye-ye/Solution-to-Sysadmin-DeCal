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

1. You should add `hosts: dns files` to the **/etc/nsswitch.conf**  file.

## Q3b

1. `n` should be set to 1.



## Exercise

### 2.py

1. I found that my network connectivity is lost and websites can't be accessed.
2. I tried to `ping -c 4 8.8.8.8` and `ping -c 4 google.com` but failed.
3. Then I checked route table using `route -n` and found the gateway of my default interface was changed to my computer ip, which led to the network connection lost.
4. Simpliy `sudo systemctl restart networking` and `sudo systemctl restart NetworkManager` will help.

### 3.py

1. I found that I couldn't open "google.com". But other websites can still be accessed.
2. I `ping google.com` and succeeded, so I think that the network connection is sound but the DNS entry of "google.com" may be changed.
3. I ran `dig google.com` and found that the ip of "google.com" was set to "72.66.115.13"
4. To fix this, I edited the **/etc/hosts** , deleting the entry and saved.
### 5.py

1. I found that all the domain entry has been set to 72.66.115.13 (Does this ip has special meanings?) after running `dig <domain_name>` with several websites.

2. I also found that when I ran `dig` command, there's always error message:

   ```
   communications error to <my_computer_ip>#53: connection refused
   ```

   It seems that my DNS server is not running correctly.

3. Then I checked **/etc/hosts**, nothing weired.

4. But something seems to be changed in **/etc/resolv.conf** because the nameserver is set to 127.0.0.1, which used to be 127.0.0.53.

5. I ran `sudo netstat -peanut` to check which service is listening 127.0.0.1 and I found it's `dnsmasq`. By the way, `systemd-resolve` is listening 127.0.0.53

6. So I ran to **/etc/dnsmasq.conf**, the content is:
   ```
   no-dhcp-interface=
   server=8.8.8.8
   
   no-hosts
   addn-hosts=/etc/dnsmasq.hosts
   address=/com/72.66.115.13
   ```

   and the content in **/etc/dnsmasq.hosts** is:

   ```
   72.66.115.13 www.facebook.com facebook.com
   ```

   The problem is clear: system nameserver is set to 127.0.0.1, which is listened by `dnsmasq`, and in **/etc/dnsmasq.conf**, every domain suffixed with "com" will be directed to 72.66.115.13. In **/etc/dnsmasq.hosts**, Facebook.com is bound to 72.66.115.13.

7. So the solution is deleting these two lines and restart `dnsmasq` service using `systemctl`. Everything wents well.

8. Tips: you had better to change the content in **/etc/resolv.conf** back using the backup in **/etc/resolv.conf.bak**.

