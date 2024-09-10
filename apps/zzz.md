
### allow run zzz wo passwd
open `visudo`, using command:
```sh
EDITOR=helix sudo visudo
```
and add next line to file and save it
```conf
%wheel ALL=(ALL) NOPASSWD: /usr/bin/zzz
```

### create alias wh sudo for zzz
open `~/.bashrc`, add line next line to file and save it
```sh
alias zzz='sudo zzz'
```
