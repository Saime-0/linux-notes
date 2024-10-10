install fonts
```sh
pacman -S terminus-font
```
change temporarily font
```sh
setfont ter-222b
```
save for auto load
```sh
echo "FONT=ter-222b" >> /etc/vconsole.conf
```