# Solution to Lab5b

## Short Answer Questions

1. HTTP uses `TCP` because TCP provides reliable, ordered, and error-checked delivery of a stream of bytes. By contrast, Discord and Skype use `UD`P for real-time voice and video due to its lower latency.

2. Realtek

3. 2<sup>24</sup>

4. A, NS and MX records

5. While `ping` is a useful tool for a quick check of network connectivity to a server, it's not a comprehensive test of server accessibility. For a complete assessment, you should check connectivity on the specific ports and protocols your application uses (e.g., using `telnet`, `curl`, or specialized monitoring tools) in addition to `ping`.

## Programming Exercise

1. 

```bash
#!/bin/bash

ping -c 1 $1 > /dev/null 2>&1

if [ $? -eq 0 ]; then
    echo "OK"
else
    echo "Host is not reachable"
fi
```

2. 
```bash
#!/bin/bash
ip addr show eth0 | grep "link/ether" | cut -d' ' -f6
```
