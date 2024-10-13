create systemd system service and enable it:
```service
[Unit]
Description=Reverse tunnel via SSH for forward ports
After=network.target

[Service]
User=user
Group=group
ExecStart=/usr/bin/ssh -i pathToIdentity -o ServerAliveInterval=180 -o ServerAliveCountMax=2 -o ExitOnForwardFailure=yes -N -R port:port login@host
Restart=always
RestartSec=5
RuntimeMaxSec=1d

[Install]
WantedBy=default.target
```
test line below, but now works:
```service
ExecStart=expect -c "set timeout -1; spawn /usr/bin/ssh -i pathToIdentity -o ServerAliveInterval=180 -o ServerAliveCountMax=2  -N -R port:port login@host; expect \"port forwarding failed\" { exit 1 }"
```
