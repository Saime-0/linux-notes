
### WM Qtile intro
install
```sh
paru -S xorg-server xorg-xinit qtile
```
create `~/.xinitrc`
```sh
#!/bin/bash

xset r rate 185 40 # Параметры повторения клавиш
setxkbmap -layout us,ru -option "grp:win_space_toggle,grp_led:caps,caps:super" # Раскладка клавиатуры
qtile start # Запуск не в exec, чтобы работал setxkbmap 
```
copy default config, and edit it
```sh
cp /usr/share/doc/qtile/default_config.py .config/qtile/config.py
```

for qtile
```sh
startx
```

### Packages
- `nnn` - terminal file manager
- `alacritty` - terminal

### Config

Alactritty config file: `.config/alacritty/alacritty.toml`
```toml
[font.normal]
family = "Agave Nerd Font Mono"
```
