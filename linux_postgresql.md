<!-- TOC -->

- [Using postgresql on Ubuntu linux](#using-postgresql-on-ubuntu-linux)
    - [Install and run postgresql:](#install-and-run-postgresql)
    - [Create & Drop database cluster](#create--drop-database-cluster)
    - [Start & Stop pg server:](#start--stop-pg-server)
        - [Init Cluster:](#init-cluster)
        - [start server:](#start-server)
        - [Stop pg server:](#stop-pg-server)
        - [Check pg server status:](#check-pg-server-status)

<!-- /TOC -->

# Using postgresql on Ubuntu linux

## Install and run postgresql:

Install server and common utilities:

> `sudo apt-get install postgresql-10`

Add Postgresql bin to PATH:

> Edit ~/.profie, and append`PATH="$PATH":"/usr/lib/postgresql/10/bin"`

## Create & Drop database cluster

    sudo pg_dropcluster 10 data
    sudo pg_createcluster 10 data

## Start & Stop pg server:

### Init Cluster:

    mkdir /var/lib/postgresql/10/data
    chown postgres /var/lib/postgresql/10/data
    sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/data initdb

### start server:

    sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/data -l /var/log/postgresql/postgresql-10-data.log start

### Stop pg server:

    sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D   /var/lib/postgresql/10/data stop

### Check pg server status:

    sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/data status
