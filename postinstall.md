

add `wheel` access to `sudo` 
```sh
echo "%wheel ALL=(ALL:ALL) ALL" > /etc/sudoers.d/included
```

install first needed deps
```
sudo pacman -S --needed git base-devel
```

create new user and add to `wheel`, after command succesful, reboot pc
```
useradd -G wheel -m <name>
passwd <name>
```


switch to user manually, and run below command for install yay
```sh
cd /tmp && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si
```
