# Migration

## Prerequisites

1. having `git` or `wget` installed and in path
2. having `/usr/bin/env` (should be trivial : it is everywhere even it freebsd)
3. having `expect` installed and in path
4. be able to use SSL
5. clone or download the git repository
```bash
$ git clone https://github.com/Siweb-France/migrate # or
$ git clone https://github.com/Siweb-France/migrate /var/scripts/migrate # for custom location, or
$ wget https://github.com/Siweb-France/migrate/archive/master.zip && tar -xf master.zip && rm master.zip # if git is inaccessible
```


## How to

```bash
$ . enableMigrationTools # to add program to the Path (facultative)
$ migrate <user@hostname> <database 1> [ <database 2> <database 3> ... ]
```
Note that the remote host connection must be transparent : at least register as a `authorized_key`

```ssh
# Make connection automatic by adding local public key to 
ssh-copy-id username@hostname
```

You can also preset the connection in `.ssh/config` :

```ssh
# make a preset for the connection
host alias_name
    hostname server_name
    user user_name
```

And then simply use `ssh alias_name`, or in our case, `migrate alias_name <bases ...>`

## Explication

**migrate** will : 
1. migrate the database :
    * ask for local identifiants
    * dump required databases
    * scp the dump on remote server
    * ask for remote identifiants
    * integrate the dump on remote mysql
2. loop ask if there is some folders to copy until users says no :
    * find corresponding folders with the help of the user
    * ask for new location on remote server
    * rsync the data on required location. actual configuration : over ssh, compressed and update only.
