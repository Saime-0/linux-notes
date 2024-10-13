
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
- `ttf-jetbrains-mono ttf-jetbrains-mono-nerd` - monospace JetBrains fonts (coding)
- `locale-en_ru` - Update en_RU.UTF-8 locale

### Config

Alactritty config file: `.config/alacritty/alacritty.toml`
```toml
[font.normal]
family = "Agave Nerd Font Mono"
```

`~/.xinitrc`
```sh

export XCURSOR_SIZE=24
export QT_QPA_PLATFORM=xcb
export GDK_BACKEND=x11,*
export SDL_VIDEODRIVER=x11
export CLUTTER_BACKEND=x11
export XDG_CURRENT_DESKTOP=Qtile
export XDG_SESSION_TYPE=x11
export XDG_SESSION_DESKTOP=Qtile

export XCURSOR_THEME=Adwaita
export GTK_THEME=Fluent-round-Dark
export GTK_ICON_THEME=gruvbox-dark-icons-gtk
export QT_STYLE_OVERRIDE=qt6ct-style
export QT_QPA_PLATFORMTHEME=qt6ct

export SSH_AUTH_SOCK=$XDG_RUNTIME_DIR/ssh-agent.socket 

# Установка параметров повторения клавиш
xset r rate 185 40

# Установка раскладки клавиатуры
setxkbmap -layout us,ru -option "grp:win_space_toggle,grp_led:caps,caps:super"

# Демон уведомлений
dunst &

# Запуск qtile
qtile start
```

user dirs `~/.config/user-dirs.dirs`
```sh
XDG_DESKTOP_DIR="$HOME/downloads"
XDG_DOWNLOAD_DIR="$HOME/downloads"
XDG_TEMPLATES_DIR="$HOME/dirs/documents/templates"
XDG_PUBLICSHARE_DIR="$HOME/dirs/documents/public"
XDG_DOCUMENTS_DIR="$HOME/dirs/documents"
XDG_MUSIC_DIR="$HOME/dirs/music"
XDG_PICTURES_DIR="$HOME/dirs/pictures"
XDG_VIDEOS_DIR="$HOME/dirs/videos"
```

Bashrc: `~/.bashrc`
```sh
# If not running interactively, don't do anything
[[ $- != *i* ]] && return


#############
#### ENV ####
#############

export XDG_CONFIG_HOME=$HOME/.config

export PATH=$PATH:$HOME/.emacs.d/bin
export GOPATH=$(go env GOPATH)

# Ignore duplicate commands and has ' ' prefiix
HISTCONTROL=ignoreboth:erasedups

# Setup prompt
Fuchsia="$(tput setaf 13)"
Grey50="$(tput setaf 244)"
Reset="$(tput sgr0)"
PS1='${Fuchsia}\u@${Grey50}\h \W \\$ ${Reset}'


###############
#### FUNCS ####
###############

# Print battary level
alias batcap='cat /sys/class/power_supply/BAT0/capacity'

# Set brighness level
function setbright() {
	echo $1 | sudo tee /sys/class/backlight/amdgpu_bl1/brightness >> null
}

alias ls='ls --color=auto'
alias grep='grep --color=auto'

goclifast() {
    local processors=$1
    # Запускаем команду в новой оболочке
    if [ -n "$processors" ]; then
        bash -c "ulimit -v 10000000 && taskset -c 0-$processors golangci-lint run -v --fast"
    else
        bash -c "ulimit -v 10000000 && golangci-lint run -v --fast"
    fi
}


#################
#### PLUGINS ####
#################

# User specific aliases and functions
for rc in ~/.bashrc.d/*; do
    [ -f "$rc" ] && . "$rc"
done
```
