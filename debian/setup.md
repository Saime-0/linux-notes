```sh
sudo apt install sudo neofetch zsh sshfs

echo "# set PATH so it includes sbin if it exists
if [ -d "/usr/sbin" ] ; then
    PATH="/usr/sbin:$PATH"
fi" >> .profile

source .profile

usermod -aG sudo username

chsh -s /bin/zsh

echo "EDITOR="vim"

setopt histignorealldups sharehistory

# Use emacs keybindings even if our EDITOR is set to vi
bindkey -e

# Keep 1000 lines of history within the shell and save it to ~/.zsh_history:
HISTSIZE=1000
SAVEHIST=1000
HISTFILE=~/.zsh_history
setopt appendhistory # Сохраняем всю историю в файл, чтобы она не стиралась, если мы выключим и включим шелл

PROMPT='%F{138}%n%F{137}@%F{138}%m %F{15}%~ %F{137}$ %F{115}'" > ~/.zshrc

touch ~/.hushlogin
