```sh
paru -S xorg-server xorg-xinit qtile"
echo "exec qtile start" >> .xinitrc
cp /usr/share/doc/qtile/default_config.py .config/qtile/config.py
startx
```