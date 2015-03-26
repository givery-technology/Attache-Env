# How to setup Attache development environment

## Prerequisite

- VirtualBox
- Vagrant 1.7 or later
- Ansible

Add ubunt1404 to vagrant box

``` bash
vagrant box add ubuntu1404 https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box
```

Add following envvars

``` bash
# SSH private key path for GitHub
export PRIVATE_KEY_PATH=~/.ssh/id_rsa
# AWS setting
export AWS_KEY="AWS access key for attache-dev"
export AWS_SECRET="AWS secret key for attache-dev"

```

AWS_KEY and AWS_SECRET for aws-dev are written in [here](https://github.com/givery-technology/Attache/wiki/Server%20Management).

## Make local environment

``` bash
mkdir Attache
cd Attache
mkdir data
git clone https://github.com/givery-technology/Attache-Env vagrant
cd vagrant
vagrant up
ansible-playbook setup.yml
```

It makes following directories structure.

- Attache
  - data
    - Attache
    - Attache_Android
  - vagrant

data directory is synced with virtual machine.
So, you can edit source codes from host machine.

## Run
Access following urls with your browser

- Top - http://192.168.33.10:8888/
- Admin - http://192.168.33.10:8888/patrash
- Company - http://192.168.33.10:8888/companies
- Student - http://192.168.33.10:8888/sp

No user is registered initially.  
You can make admin user with following command

```
vagrant ssh
cd data/Attache
php oil console
>>> Auth::create_user('Your username', 'Your password', 'Your email', 100);
```

You can login from /patrash with following id/password.

## mysql
It uses local mysql server.  
You can access mysql-cli from virtual machine with following command.

```
mysql -uattache -pattache -Dattache
```

## Develop
ToDo

## Trouble shooting
### Use vagrant 1.7 or later
The location of ssh private key was changed from 1.7.  
Check existence of .vagrant/machines/default/virtualbox/private_key

### Maintain ~/.ssh/known_hosts
If you destroyed the virtual machine and recreate it.  
Its host signature changes.  
So, you have to remove existing host signature(192.168.33.10) from known_hosts.

### Passphrase for ssh private key
If you set passphrase to ssh private key, setup.yml might not work fine.  
If so, please comment out git clone task and do it manually.

