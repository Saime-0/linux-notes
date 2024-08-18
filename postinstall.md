

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


### AUR helper

switch to user manually, and run one of below commands for install you prefer helper
*change directory to tmp*
```sh
cd /tmp
```

[yay](https://github.com/Jguer/yay) - Yet another Yogurt - An AUR Helper written in Go
```sh
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
[paru](https://github.com/Morganamilo/paru) - Feature packed AUR helper
```sh
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```


### Packages

- `bash-completion` - Programmable completion for the bash shell
