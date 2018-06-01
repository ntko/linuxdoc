### Using postgresql on Ubuntu linux

#### Install and run postgresql:

Install server and common utilities:

> `sudo apt-get install postgresql-10`

Add Postgresql bin to PATH:

> Edit ~/.profie, and append`PATH="$PATH":"/usr/lib/postgresql/10/bin"`

Start pg server:

* Init Cluster:

>    mkdir /var/lib/postgresql/10/data

>    chown postgres /var/lib/postgresql/10/data

>    sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/data initdb

* start server:

> sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/data -l /var/log/postgresql/postgresql-10-data.log start

Stop pg server:

> sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/data stop

Check pg server status:
> sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/data status
