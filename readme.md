# Migration

## Prerequisites

1. having a functionnal git
2. having a functionnal /usr/bin/env
3. clone the git repository
```bash
$ git clone https://github.com/Siweb-France/migrate <optional new folder to create># for https clone
```


## How to

* enable the migration tools in path by running :
```bash
$ . enableMigrationTools
```
* migrate the data
```bash
$ migrate "target host added to .ssh/config" "as" "much" "bases" "as" "needed"
```

## Explication

**migrate** will : 
1. migrate the database
    * ask for local identifiants
    * dump required databases
    * scp the dump on remote server
    * ask for remote identifiants
    * integrate the dump on remote mysql
2. ask if there is some folders to copy
    * find corresponding folders with the help of the user
    * ask for new location on remote server
    * rsync the data on required location. actual configuration : over ssh, compressed and update only.

