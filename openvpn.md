
## Server part

1. cd to `scripts` directory
2. run below command for install and run script
```
curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh \
&& chmod +x openvpn-install.sh \
&& sudo ./openvpn-install.sh
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

