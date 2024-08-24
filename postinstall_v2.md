enable builtin-dhcp client of iwd [wiki](https://wiki.archlinux.org/title/Iwd#Enable_built-in_network_configuration), create/edit `/etc/iwd/main.conf` and add the following section to it:
```
[General]
EnableNetworkConfiguration=true
[Network]
NameResolvingService=systemd
```
then `systemctl enable --now systemd-resolved` - start dns
then `systemctl enable --now iwd` - start iwd

and connect to network using `iwctl`

** `echo "127.0.0.1\tlocalhost" >> /etc/hosts`

befo install paru - `pacman -S --needed git base-devel`
