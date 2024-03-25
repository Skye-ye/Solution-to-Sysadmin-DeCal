# Solution to Lab7b

1. Take `sshd` as an example, which listens for incoming connections from clients via `SSH` . 

2. The `systemctl reload yourservice` command is used to reload the configuration of a service without interrupting its current operation. It is useful to maintain the service status. 

   The `systemctl restart yourservice` command stops the service and then starts it again. It's a more forceful way to apply changes or recover a service than `reload`

3. toy.service:

```
[Unit]
Description=Webserver toy for Sysadmin DeCal Lab7b
After=network.target

[Install]
WantedBy=multi-user.target

[Service]
ExecStart=path/to/run
User=yourusername
Restart=always
RestartSec=10
