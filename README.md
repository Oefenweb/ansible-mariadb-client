## mariadb-client

[![CI](https://github.com/Oefenweb/ansible-mariadb-client/workflows/CI/badge.svg)](https://github.com/Oefenweb/ansible-mariadb-client/actions?query=workflow%3ACI)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-mariadb--client-blue.svg)](https://galaxy.ansible.com/Oefenweb/mariadb_client)

Set up a [mariadb-server](https://mariadb.com/products/technology/server) client in Debian-like systems.

#### Requirements

None

#### Variables

* `mariadb_client_install`: [default: `[]`]: Additional packages to install

* `mariadb_client_my_cnf_files`: [default: `[]`]: `.my.cnf` files to configure
* `mariadb_client_my_cnf_files.{n}.dest`: [optional, default: `~owner/.my.cnf'`]: The remote path of the file to copy
* `mariadb_client_my_cnf_files.{n}.owner`: [required]: The name of the user that should own the file
* `mariadb_client_my_cnf_files.{n}.group`: [optional, default: `owner`]: The name of the group that should own the file
* `mariadb_client_my_cnf_files.{n}.mode`: [optional, default: `0600`]: The mode of the file
* `mariadb_client_my_cnf_files.{n}.login_host`: [optional, default: `localhost`]: The host running the server
* `mariadb_client_my_cnf_files.{n}.login_port`: [optional, default: `3306`]: The port of the server
* `mariadb_client_my_cnf_files.{n}.login_user`: [optional, default: `owner`]: The username used to authenticate with
* `mariadb_client_my_cnf_files.{n}.login_password`: [required]: The password used to authenticate with

* `mariadb_client_my_cnf_files.{n}.ssl`: [optional]: Whether or not to use SSL when connection (deprecated)
* `mariadb_client_my_cnf_files.{n}.ssl_mode`: [optional]: Specifies the desired security state of the connection to the server (e.g. `VERIFY_CA`)

* `mariadb_client_my_cnf_files.{n}.ssl_ca`: [optional, default: `ca-cert`]: The identifier of the ca certificate file in ssl map
* `mariadb_client_my_cnf_files.{n}.ssl_cert`: [optional, default: `client-cert`]: The identifier of the ssl certificate file in ssl map
* `mariadb_client_my_cnf_files.{n}.ssl_key`: [optional, default: `client-key`]: The identifier of the ssl key file in ssl map

* `mariadb_client_ssl_map`: [default: `{}`]: SSL declarations
* `mariadb_client_ssl_map.key`: [required]: The identifier of the file (e.g. `ca-cert`)
* `mariadb_client_ssl_map.key.src`: [required]: The local path of the file to copy, can be absolute or relative (e.g. `../../../files/mariadb-client/etc/mysql/ca-cert.pem`)
* `mariadb_client_ssl_map.key.dest`: [required]: The remote path of the file to copy (e.g. `/etc/mysql/ca-cert.pem`)
* `mariadb_client_ssl_map.key.owner`: [optional, default `root`]: The name of the user that should own the file
* `mariadb_client_ssl_map.key.group`: [optional, default `mysql`]:The name of the group that should own the file
* `mariadb_client_ssl_map.key.mode`: [optional, default `0640`]: The mode of the file

## Dependencies

None

## Recommended

* `mariadb-server` ([see](https://github.com/Oefenweb/ansible-mariadb-server))

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
    mariadb_client_my_cnf_files:
      - dest: '~root/.my.cnf'
        owner: root
        ansible.builtin.group: root
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
