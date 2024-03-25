# Solution to Lab5a

1. Take `sshd` as an example, which listens for incoming connections from clients via `SSH` . 

2. The `systemctl reload yourservice` command is used to reload the configuration of a service without interrupting its current operation. It is useful to maintain the service status. 

   The `systemctl restart yourservice` command stops the service and then starts it again. It's a more forceful way to apply changes or recover a service than `reload`

3. Command I use: 
```bash
curl -X POST -H "Content-Type: application/json" -d '{"crash":"true"}' http://localhost:5000/crash
```
4. toy.service:

```
[Unit]
Description=Webserver toy for Sysadmin DeCal Lab4
After=network.target

[Install]
WantedBy=multi-user.target

[Service]
ExecStart=path/to/run
User=yourusername
Restart=always
RestartSec=10
