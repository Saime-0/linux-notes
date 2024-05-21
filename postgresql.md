https://www.geeksforgeeks.org/how-to-install-postgresql-on-arch-based-linux-distributions-manjaro/
https://www.bigbinary.com/blog/configure-postgresql-to-allow-remote-connection
### server
install package
```sh
yay postgresql
```

check version
```sh
postgres --version
```

init cluster
```sh
sudo initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
```

enable and start service
```sh
sudo systemctl enable postgresql.service
```

open psql
```sh
sudo -u postgres psql
```
### psql
create user
```psql
CREATE USER <username> WITH ENCRYPTED PASSWORD ‘<password>’;
```

crate db
```psql
CREATE DATABASE <dbname>;
```

grant user to use db, and exit from psql
```psql
GRANT ALL PRIVILEGES ON DATABASE <dbname> TO username;
```
### local pc
let's test connect from another pc:
```sh
telnet <ip> 5432
```
> u take `telnet: Unable to connect to remote host: Connection refused```

### server

Allow connect to postgres from another pc:
find config file of cluster
```sh
sudo find / -name "postgresql.conf"
```

open found file, and replace string
from: `#listen_addresses = 'localhost'`to:
```conf
listen_addresses = '*'
```

then restart server
```sh
sudo systemctl restart postgresql.service
```
> if u try connect now with psql client from another pc, take this error: `[28000] FATAL: no pg_hba.conf entry for host "176.59.82.160", user "uchcb", database "ccb_db", no encryption`

add strings to end of file `pg_hba.conf`
```conf
host    all             all              0.0.0.0/0                       md5
host    all             all              ::/0                            md5
```
and restart again server
```sh
sudo systemctl restart postgresql.service
```
