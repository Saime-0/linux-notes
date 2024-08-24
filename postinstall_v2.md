enable builtin-dhcp client of iwd [wiki](https://wiki.archlinux.org/title/Iwd#Enable_built-in_network_configuration), create/edit `/etc/iwd/main.conf` and add the following section to it:
```
[General]
EnableNetworkConfiguration=true
[Network]
NameResolvingService=systemd
```
then `systemctl enable --now systemd-resolved` - start NSS
then `systemctl enable --now iwd` - start iwd

and connect to network using `iwctl`

befo install paru and create user - `pacman -S --needed git base-devel sudo rustup`

`export EDITOR=/usr/bin/vim` - for visudo

exec cmd `visudo` and uncomment line: `%wheel ALL=(ALL:ALL) ALL`
or write plugin
```sh
echo "%wheel ALL=(ALL:ALL) ALL" > /etc/sudoers.d/included
```

create new user and add to `wheel`
```sh
useradd -G wheel -m <username>
passwd <username>
```

exec cmd `su <username>` for login via the user
exec cmd `rustup default stable` for install rust (its required by paru)
exec cmd `mkdir ~/tmp` for create tmp dir

then change dir and install paru
```sh
cd ~/tmp
```
[paru](https://github.com/Morganamilo/paru) - Feature packed AUR helper
```sh
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```
