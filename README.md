haproxy-pg
=========

This roles adds settings for postgres to exist haproxy config or creates new haproxy instance.

Requirements
------------

This role isn't depend on other role.

Role Variables
--------------



Dependencies
------------

This role is optionally dependency for postgres role for many projects. But it is used as independent role.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
- hosts: postgres
  roles:
    - role: postgres

- hosts: pgproxy
  roles:
    - role: haproxy-pg
	- role: pgbouncer
```

License
-------

GPLv2

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
