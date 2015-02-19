# pgbouncer

[![Puppet Forge](http://img.shields.io/puppetforge/v/conzar/pgbouncer.svg)](https://forge.puppetlabs.com/conzar/pgbouncer)
[![Build Status](https://travis-ci.org/Conzar/pgbouncer.svg?branch=master)](https://travis-ci.org/Conzar/pgbouncer)

## Overview
Installs and configures [pgbouncer](https://wiki.postgresql.org/wiki/PgBouncer).

## Module Description
This module installs the pgbouncer package and configures it to pool connections for postgresql databases.
By default, the service uses port 6432 as this is the default port of pgbouncer.

## Setup

### What pgbouncer affects

* /etc/pgbouncer/pgbouncer.ini
* /etc/pgbouncer/userlist.txt
* /etc/default/pgbouncer

### Setup Requirements 

Requires a Debian based system.

### pgbouncer with amazon_ses

To install pgbouncer and have it connect to a database with default parameters.
Where all pgbouncer is installed on the postgresql server.  The database db2 is available.  An authorized user is postgres with password postgres.

```puppet 
  class{'pgbouncer': 
    databases => [ '* = port=5432',
                   "database2 = host=localhost port=5432 dbname=db2"],
    auth_list => [ "\"postgres\" \"password\""],
  }
```

## Usage

###Classes

This module modifies the pgbouncer configuration files and replaces the main configuration file.

####Class: `pgbouncer`

The primary class that installs and configures pgbouncer.  It also ensures the pgbouncer service is running.

**Parameters within `pgbouncer`:**

#####`databases`
	An array of entries to be written to the databases section in the pbbouncer.ini
	Array entry format: database_alias_name = connection_string

#####`logfile`
   	The full path to the log file.
   	Default: /var/log/postgresql/pgbouncer.log

#####`pidfile`
   	The full path to the pid file for the pgbouncer process.
   	Default: /var/run/postgresql/pgbouncer.pid

#####`listen_addr`
   	The address that are listened to by pgbouncer.
   	Default: * (all addresses)

#####`listen_port`
   	The port for pgbouncer to listen on.
   	Default: 6432

#####`admin_users`
   	A comma-seperated list of users allowed to access the admin console who
   	then can perform connection pool management operations and obtain
   	information about the connection pools.

#####`stats_users`
   	A comma-seperated list of users allowed to access the admin console
   	who can obtain information about the connection pools.

#####`auth_list`
   	An array of auth values (user/password pairs).
   	This array is written to /var/lib/postgresql/pgbouncer.auth line by line.
   	Array entry format: 
    "\"<username>\" \"<password\"

## Limitations

Works with debian based OS's.

## Development

The module is open source and available on github.  Please fork!