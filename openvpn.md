
## Server part

1. cd to `scripts` directory
2. run below command for install and run script
```
curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh \
&& chmod +x openvpn-install.sh \
&& sudo ./openvpn-install.sh
```

you will run with trouble: `read UDPv4 [ECONNREFUSED]: Connection refused (fd=3,code=111)`
cause this problem concluded in `not permitted actions`, for check it, run:
```sh
sudo journalctl -xeu openvpn-server@server.service | grep "not permitted"
```
if out contains some lines, follow next steps for fix it:

1. allow read openvpn read config
```sh
sudo chown -R openvpn:network /etc/openvpn
```

allow openvpn write logs
```sh
sudo chown -R openvpn:network /var/log/openvpn
```

and comment below lines in /etc/openvpn/server.conf
```
user nobody
group nobody
```

## Client part

1. open cd to home directory
2. run below command for cp file `.ovpn` locally
```sh
scp <name>@<host>:/home/<name>/<filename>.ovpn ./
```

install openvpn if not installed
```sh
yay -S openvpn
```

make available run openvpn without password
```sh
echo "%openvpn All=(root) NOPASSWD: /usr/bin/openvpn" >> /etc/sudoers.d/included
```

