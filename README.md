# SaltStack Dev Environment

This is my personal SaltStack dev environment setup using Docker containers to launch 
masters/minions. This is really oriented to my workflow and may not really fit with yours
but here it is anyway.

## Getting Started

Boot a master first:

`docker-compose up -d salt-master`

Then you can boot a minion

`docker-compose up -d salt-minion`

Verify it worked by doing:

`docker-compose exec salt-master salt \* test.ping`

Resetting everything just run:

`docker-compose down -v`

The -v flag will remove the pki volume which is important if you are doing a full reset.

## Configuration, States and Other Data

Important directories

### Master

* `data/master/config` is where you put the additional configuration for the master and maps to `/etc/salt/master.d/`
* `data/master/pillar` you can store your pillar information here and maps to `/srv/pillar`
* `data/master/salt` is where your state and other data can do and maps to `/srv/salt`

The master also has a docker volume called master_pki which maps to `/etc/salt/pki` and stores the PKI data

### Minion

* `data/minion/config` is the configuration for the minion and maps to `/etc/salt/minion.d`

Note: I don't store PKI data for minions so once the container is gone their key is lost.

### Database

* `data/db/init` stick your .sql files here and it will be loaded on the first boot


# Credits

This is based off of the project here https://github.com/tomwalsh/saltstack-docker-development but it's been heavily modified to fit
my personal workflow.