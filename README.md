[TOC]

haproxy-pg
=========

This roles adds settings for postgres to exist haproxy config or creates new haproxy instance.

Copyright (C) 2023  Mikhail Shurutov

This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License
as published by the Free Software Foundation; either version 2
of the License, or any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.

Requirements
------------

This role isn't depend on other role.

Role Variables
--------------

### common variables
`haproxy_packages` is list of packages;
`haproxy_user` is system user for haproxy service;
`haproxy_group` is system group for haproxy service by default same as user.

### pathnames to files and directories
`haproxy_templates_dir` is directory for templates;
`haproxy_cfg_dir` is directory for configuration;
`haproxy_cfg_file` is configuration file.

### configuration variables
#### common variables
Prefix "`^[0-9]{2}_`" is necessary for ordering place in config. When template of config is placed into config directroy this prefix is cutted. By default there are defined three sections: `[global]` with define `maxconn = 500` variable; `[defaults]` with define logging mode and timeout variables; `[listen stats]` with variables for output stats by HTTPs.

#### postgres variables
`haproxy_pg_max_conn` is the max connections to postgres instance;
`haproxy_check_pg_port` is port for checking postgres instance health when using patroni cluster for postgres HA;
`haproxy_pg_check_options` is check options for checking postgres instance health when using patroni cluster for postgres HA;
`haproxy_pg_port` is the port what postgres is listening;

#### default is read/write definition
`haproxy_pg_clusters_default` - there is defined only one read/write cluster with minimal settings.

#### Distro-depended variables

Currently only package lists are defined for each package manager.

Dependencies
------------

This role is optionally dependency for postgres role for many projects. But it is used as independent role.

Using a Role
----------------

### Variables Used

* `ANSIBLE_ROOT_DIR` is path for static content: roles,configs,etc, for example: /data/ansible
* `ANSIBLE_ROOT_ROLE_DIR` is path in `roles_path` config variable, for example: /data/ansible/roles  
Content of my ~/.ansible.cfg:
```
...
# additional paths to search for roles in, colon separated
#roles_path    = /etc/ansible/roles
roles_path    = /data/ansible/roles
...
```

### Install role
#### GIT repo

    user@host ~ $ cd $ANSIBLE_ROOT_ROLE_DIR
    user@host roles $ git clone https://shurutov@git.code.sf.net/p/haproxy-pg/code haproxy_pg

#### Ansible galaxy
##### Installation from command

    user@host ~ $ cd $ANSIBLE_ROOT_DIR
    user@host ansible $ ansible-galaxy role install mshurutov.haproxy_pg -p roles

##### Installation from requirements.yml

    user@host ~ $ cd $ANSIBLE_ROOT_DIR
    user@host ansible $ grep haproxy_pg requirements.yml
    - name: mshurutov.haproxy_pg
    user@host ansible $ ansible-galaxy role install -r requirements.yml -p roles

### Example Playbook

#### Role installed as git repo

    ...
    - hosts: haproxy_pg_group
      roles:
         - role: haproxy_pg
    ...

#### Role installed by ansible-galaxy

    ...
    - hosts: haproxy_pg_group
      roles:
         - role: mshurutov.haproxy_pg
    ...

License
-------

[GPLv2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.txt)

Author Information
------------------

My name is Mikhail Shurutov, I'm an operations engineer since 1997.
