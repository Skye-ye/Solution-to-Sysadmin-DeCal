# Solution to Lab5b

## Short Answer Questions

1. HTTP uses `TCP` because TCP provides reliable, ordered, and error-checked delivery of a stream of bytes. By contrast, Discord and Skype use `UD`P for real-time voice and video due to its lower latency.
2. Realtek
3. 2<sup>24</sup>
4. A, NS and MX records

## Programming Exercise

1. 

```bash
# is_on.sh
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
# mac.sh
#!/bin/bash
ip addr show eth0 | grep "link/ether" | cut -d' ' -f6
```
