
### WM Qtile intro
install
```sh
paru -S xorg-server xorg-xinit qtile python-psutil
```
create `~/.xinitrc`
```sh
xset r rate 185 40 # Параметры повторения клавиш
setxkbmap -layout us,ru -option "grp:win_space_toggle,grp_led:caps,caps:super" # Раскладка клавиатуры
# Демон уведомлений
dunst &
qtile start # Запуск не в exec, чтобы работал setxkbmap 
```
copy default config, and edit it
```sh
cp /usr/share/doc/qtile/default_config.py .config/qtile/config.py
```

for start qtile
```sh
startx
```

### Packages

- `nnn` - terminal file manager
- `alacritty` - terminal
- `dunst` - lightweight notification-daemon
- `ttf-agave-nerd` - font Agave from nerd fonts library (terminal)
- `terminus-font` - Monospace bitmap font (tty)
- `ttf-jetbrains-mono-nerd` - monospace JetBrains fonts (coding)
- `locale-en_ru` - Update en_RU.UTF-8 locale

### Config

Alactritty config file: `.config/alacritty/alacritty.toml`
```toml
[font.normal]
family = "Agave Nerd Font Mono"
```

Bashrc: `~/.bashrc`
```sh
# If not running interactively, don't do anything
[[ $- != *i* ]] && return

# Ignore duplicate commands and has ' ' prefiix
HISTCONTROL=ignoreboth:erasedups

# Setup prompt
Fuchsia="$(tput setaf 13)"
Grey50="$(tput setaf 244)"
Reset="$(tput sgr0)"
PS1='${Fuchsia}\u@${Grey50}\h \W \\$ ${Reset}'

# Print battary level
alias batcap='cat /sys/class/power_supply/BAT0/capacity'

# Set brighness level
function setbright() {
	echo $1 | sudo tee /sys/class/backlight/amdgpu_bl1/brightness >> null
}

alias ls='ls --color=auto'
alias grep='grep --color=auto'
```
