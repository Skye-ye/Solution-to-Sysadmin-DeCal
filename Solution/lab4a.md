# Solution to Lab4a

## Q1

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AABAIBbpOeshZjo5sgYc6ItLkYN43qT8HJwHl8h21oSO441O skyzheng@Sky's MacBook Pro
```

## Q2

The owner(me) has the permission to read and write both public and private key, which is acceptable since the owner created the keys and should have the access to them. 

However, other group members have only read permission of the public key and no permission for the private key. This is also natural since the public key is open to everyone and the private key should be kept secretly to the owner.

## EC1

### Steps

1. Edit '/etc/ssh/sshd_config', like `sudo vim /etc/ssh/sshd_config`

2. Uncomment `PasswordAuthentication` and set its value to `no`

3. Save and Quit

4. Reload the `sshd` service using `sudo systemctl reload sshd` (system using `systemctl`)

## Q3

`sudo ufw allow <port>`

## Q4

```
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), deny (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22                         ALLOW IN    10.147.18.0/24
9993                       ALLOW IN    10.147.18.0/24
```

## Q5

Setting up a firewall is important because it acts as a barrier that controls the traffic between your internal network and untrusted external networks, such as the internet. It helps to prevent unauthorized access and cyber attacks.

Exposing a port can be risky because it may:

1. Allow attackers to access or attack the system if the service on the port is vulnerable.
2. Be targeted for exploitation, leading to unauthorized access or data breaches.
3. Be overwhelmed by traffic in a Denial of Service (DoS) attack.
4. Allow sensitive data to be intercepted if not encrypted.

## EC2

`sudo ufw allow from x.x.x.x/16 to any port 22`

## EC3

1. `sudo apt update && sudo apt install fail2ban` to install fail2ban

2. `sudo nano /etc/fail2ban/jail.local` to edit the config file

3. Edit the `sshd` config

```File: /etc/fail2ban/jail.local
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
findtime = 600
bantime = 3600
ignoreip = 127.0.0.1
```

4. `sudo systemctl restart fail2ban` to reload the new config
5. Using `sudo fail2ban-client status sshd` to check status
```
Status for the jail: sshd
|- Filter
|  |- Currently failed: 0
|  |- Total failed:     0
|  `- File list:        /var/log/auth.log
`- Actions
   |- Currently banned: 0
   |- Total banned:     0
   `- Banned IP list:
```

