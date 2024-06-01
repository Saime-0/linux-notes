## restrict login to root
```sh
sudo echo "PermitRootLogin no" > /etc/ssh/ssh_config.d/restrict_root_login.conf
```


## save frequency\favorit connection to config

1. open `~/.ssh/config` using editor
2. add lines
```config
Host <name>
     Hostname <host>
     User <username>
     Compression yes
```
 3. use `ssh <name>` for use setup connection


## enable login only key

create group and add user
```ssh
sudo groupadd -U <usernames> ssh_login_only_key
```

open(create) in editor `/etc/ssh/ssh_config.d/login_only_key.conf`
and write lines
```config
PubkeyAuthentication no
PasswordAuthentication no
User ssh_login_only_key
   PubkeyAuthentication yes
```
