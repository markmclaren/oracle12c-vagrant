# oracle12c-vagrant
A vagrant box that provisions Oracle 12c automatically.

## Getting started
1. Clone this repository
2. Download the Oracle Database 12c binaries `linuxamd64_12102_database_1of2.zip` and `linuxamd64_12102_database_2of2.zip`
from http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html and unzip to `database/`
    2. Ensure you unzip into the same directory and they merge. There are some common directories in each. On the commandline, you can run `unzip '*.zip'` to do this for you.
3. Install Virtualbox
4. Install Vagrant
5. Install VirtualBox plugin `vagrant plugin install vagrant-vbguest`
6. Run `vagrant up`
    6. The first time you run this it will provision everything and may take a while. Ensure you have a good internet connection!
7. Connect to the database.
8. you can shutdown the box via the usual `vagrant halt` and the start it up again via `vagrant up`.

## Connecting to Oracle
SID: `orcl`
Installation path: `/opt/oracle/`

All passwords are `password`.

## Known issues

#### Repeated authentication failure message

On `vagrant up` if you experience this issue:
````
default: Error: Authentication failure. Retrying...
default: Error: Authentication failure. Retrying...
default: Error: Authentication failure. Retrying...
default: Error: Authentication failure. Retrying...
default: Error: Authentication failure. Retrying...
````
Then you may have hit a bug in vagrant 1.8.5. See
http://stackoverflow.com/questions/22922891/vagrant-ssh-authentication-failure

The solution is to:
````
vagrant ssh 
password: vagrant 
chmod 0600 ~/.ssh/authorized_keys
exit
````

then `vagrant reload`.

#### Connection time after startup
Once Oracle and the listener starts up, it may take a few moments until you are able to connect to the DB, eg via SQL Developer.

