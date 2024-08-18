### Create key on local machine
generate key
```sh
ssh-keygen -t rsa -f ~/.ssh/<key-name> <user>@<host>
```
copy to server
```sh
ssh-copy-id -i ~/.ssh/<key-name> <user>@<host>
```

### Restrict login to root
```sh
sudo echo "PermitRootLogin no" > /etc/ssh/sshd_config.d/restrict_root_login.conf
```


### Save connection to config

1. open `~/.ssh/config` using editor
2. add lines
```config
Host <name>
     Hostname <host>
     User <username>
     Compression yes
```
 3. use `ssh <name>` for use setup connection


### Enable login only key
[!WARNING]
! required copy client public key to `.ssh/authorized_keys`

create group and add user
```ssh
sudo groupadd -U <usernames> ssh_login_only_key
```

open(create) in editor `/etc/ssh/sshd_config.d/login_only_key.conf`
and write lines
```config
PubkeyAuthentication no
PasswordAuthentication no
Match Group ssh_login_only_key
   PubkeyAuthentication yes
```

check and add if lines not exists in `/etc/ssh/sshd_config`
```conf
# Include drop-in configurations
Include /etc/ssh/sshd_config.d/*.conf
```
restart service
```sh
sudo systemctl restart sshd.service
```
