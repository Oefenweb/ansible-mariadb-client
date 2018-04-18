## mariadb-client 

[![Build Status](https://travis-ci.org/Oefenweb/ansible-mariadb-client.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-mariadb-client) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-percona--client-blue.svg)](https://galaxy.ansible.com/tersmitten/mariadb-client)

Set up a [percona-server](https://www.percona.com/software/mysql-database/percona-server) client in Debian-like systems.

#### Requirements

None

#### Variables

* `percona_client_version`: [default: `5.6`]: Version to install (e.g. `5.6`)
* `percona_client_install`: [default: `[]`]: Additional packages to install

* `percona_client_my_cnf_files`: [default: `[]`]: `.my.cnf` files to configure
* `percona_client_my_cnf_files.{n}.dest`: [optional, default: `~owner/.my.cnf'`]: The remote path of the file to copy
* `percona_client_my_cnf_files.{n}.owner`: [required]: The name of the user that should own the file
* `percona_client_my_cnf_files.{n}.group`: [optional, default: `owner`]: The name of the group that should own the file
* `percona_client_my_cnf_files.{n}.mode`: [optional, default: `0600`]: The mode of the file
* `percona_client_my_cnf_files.{n}.login_host`: [optional, default: `localhost`]: The host running the server
* `percona_client_my_cnf_files.{n}.login_port`: [optional, default: `3306`]: The port of the server
* `percona_client_my_cnf_files.{n}.login_user`: [optional, default: `owner`]: The username used to authenticate with
* `percona_client_my_cnf_files.{n}.login_password`: [required]: The password used to authenticate with

* `percona_client_my_cnf_files.{n}.ssl`: [optional]: Whether or not to use SSL when connection

* `percona_client_my_cnf_files.{n}.ssl_ca`: [optional, default: `ca-cert`]: The identifier of the ca certificate file in ssl map
* `percona_client_my_cnf_files.{n}.ssl_cert`: [optional, default: `client-cert`]: The identifier of the ssl certificate file in ssl map
* `percona_client_my_cnf_files.{n}.ssl_key`: [optional, default: `client-key`]: The identifier of the ssl key file in ssl map

* `percona_client_ssl_map`: [default: `{}`]: SSL declarations
* `percona_client_ssl_map.key`: [required]: The identifier of the file (e.g. `ca-cert`)
* `percona_client_ssl_map.key.src`: [required]: The local path of the file to copy, can be absolute or relative (e.g. `../../../files/mariadb-client/etc/mysql/ca-cert.pem`)
* `percona_client_ssl_map.key.dest`: [required]: The remote path of the file to copy (e.g. `/etc/mysql/ca-cert.pem`)
* `percona_client_ssl_map.key.owner`: [optional, default `root`]: The name of the user that should own the file
* `percona_client_ssl_map.key.group`: [optional, default `mysql`]:The name of the group that should own the file
* `percona_client_ssl_map.key.mode`: [optional, default `0640`]: The mode of the file

## Dependencies

None

## Recommended

* `percona-server` ([see](https://github.com/Oefenweb/ansible-percona-server))

#### Example(s)

##### Simple

```yaml
---
- hosts: all
  roles:
    - mariadb-client
```

##### With .my.cnf file(s)

```yaml
---
- hosts: all
  roles:
    - mariadb-client
  vars:
    percona_client_my_cnf_files:
      - dest: '~root/.my.cnf'
        owner: root
        group: root
        mode: '0600'
        login_host: localhost
        login_port: 3306
        login_user: root
        login_password: 'pw4Root'

      - owner: vagrant
        login_password: 'pw4Vagrant'
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-mariadb-client/issues)!
