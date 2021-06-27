is-ubuntu
=========

[![Build Status](https://travis-ci.org/itnok/ansible-role-is-ubuntu.svg?branch=master)](https://travis-ci.org/itnok/ansible-role-is-ubuntu) [![GitHub tag](https://img.shields.io/github/v/tag/itnok/ansible-role-is-ubuntu?sort=semver)](https://github.com/itnok/ansible-role-is-ubuntu/tags/) [![Ansible Role](https://img.shields.io/ansible/role/52993)](https://galaxy.ansible.com/itnok/is_ubuntu)

Detects whether the target Ubuntu host is... a container or eventually localhost.

Steps performed are:

  - Set is_ubuntu_localhost fact
  - Check whether inside a container or not
  - Set is_ubuntu_inside_container fact


## :exclamation: Requirements
-----------------------------

None.


## :abcd: Role Variables
------------------------

| Variable          | Description                                                                                                   | Default Value |
|-------------------|---------------------------------------------------------------------------------------------------------------|---------------|
| `is_force_lookup` | Lookup of custom additional facts does not happen if they already exist. This is it force looking up for them | `no`          |


## :link: Dependencies
----------------------

None.


## :notebook: Example Playbook
------------------------------

Here an example of how to use this role in your playbooks:

```
---
- hosts: servers
  remote_user: ubuntu   # optional (your remote user)
  gather_facts: yes     # optional

  roles:
    - { role: itnok.is_ubuntu }
```

## :guardsman: License
----------------------

MIT _([read more](LICENSE.md))_
