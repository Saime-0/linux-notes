### Client - Setup ssh on local machine

Generate key
```sh
ssh-keygen -t rsa -f ~/.ssh/<key-name> <user>@<host>
```

Copy key to server
```sh
ssh-copy-id -i ~/.ssh/<key-name> <user>@<host>
```

Save connection to config and use like: `ssh <connection-name>`
```config
echo "Host <name>
     User <username>
     Hostname <host>
     IdentityFile ~/.ssh/<key-name>
     Compression yes" >> ~/.ssh/config
```

### Server - Setup ssh daemon on server

In this section we add includes to sshd config 

check and add if lines not exists in `/etc/ssh/sshd_config`
```conf
# Include drop-in configurations
Include /etc/ssh/sshd_config.d/*.conf
```
after adding some include or config modify, service required restart
```sh
sudo systemctl restart sshd.service
```

> [!WARNING]
! next includes requires copy client public key to `.ssh/authorized_keys`

Include: restrict login to `root`

add include
```sh
sudo echo "PermitRootLogin no" > /etc/ssh/sshd_config.d/restrict_root_login.conf
```

Include: connect using **only** public keys for **only** users of specific group

create group and add user
```ssh
sudo groupadd -U <usernames> ssh_login_only_key
```

add include
```config
sudo echo "PubkeyAuthentication no
PasswordAuthentication no
Match Group ssh_login_only_key
   PubkeyAuthentication yes" > /etc/ssh/sshd_config.d/login_only_key.conf
```
