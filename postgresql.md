https://www.geeksforgeeks.org/how-to-install-postgresql-on-arch-based-linux-distributions-manjaro/
https://www.bigbinary.com/blog/configure-postgresql-to-allow-remote-connection

install package
```
yay postgresql
```

check version
```
postgres --version
```

init cluster
```
sudo initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
```

enable and start service
```
sudo systemctl enable postgresql.service
```

open psql
```
sudo -u postgres psql
```

create user
```
CREATE USER <username> WITH ENCRYPTED PASSWORD ‘<password>’;
```

crate db
```
CREATE DATABASE <dbname>;
```

grant user to use db
```
GRANT ALL PRIVILEGES ON DATABASE <dbname> TO username;
```

let's test connect from another pc:
```
telnet <ip> 5432
```
> u take `telnet: Unable to connect to remote host: Connection refused```

Allow connect to postgres from another pc:
find config file of cluster
```
sudo find / -name "postgresql.conf"
```

open found file, and replace string
from: `#listen_addresses = 'localhost'`to:
```
listen_addresses = '*'
```

then restart server
```
sudo systemctl restart postgresql.service
```
> if u try connect now with psql client from another pc, take this error: `[28000] FATAL: no pg_hba.conf entry for host "176.59.82.160", user "uchcb", database "ccb_db", no encryption`

add strings to end of file `pg_hba.conf`
```
host    all             all              0.0.0.0/0                       md5
host    all             all              ::/0                            md5
```
and restart again server
```sudo systemctl restart postgresql.service```
