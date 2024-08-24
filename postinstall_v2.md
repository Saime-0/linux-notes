enable iwd dhcp client [wiki](https://wiki.archlinux.org/title/Iwd#Enable_built-in_network_configuration), create/edit `/etc/iwd/main.conf` and add the following section to it:
```
[General]
EnableNetworkConfiguration=true
```

then `systemctl enable --now iwd.service` - start iwd

and connect to network using `iwctl`

** `echo "127.0.0.1\tlocalhost" >> /etc/hosts`

befo install paru - `pacman -S --needed git base-devel`
