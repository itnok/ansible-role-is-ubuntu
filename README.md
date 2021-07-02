is-ubuntu
=========

[![Build Status](https://github.com/itnok/ansible-role-is-ubuntu/workflows/CI/badge.svg)](https://github.com/itnok/ansible-role-is-ubuntu/actions/workflows/main.yml) [![GitHub tag](https://img.shields.io/github/v/tag/itnok/ansible-role-is-ubuntu?sort=semver)](https://github.com/itnok/ansible-role-is-ubuntu/tags/) [![Ansible Role](https://img.shields.io/ansible/role/52993)](https://galaxy.ansible.com/itnok/is_ubuntu)

Detects whether the target Ubuntu host is... a container or eventually localhost.

Steps performed are:

  - Set is_ubuntu_localhost fact
  - Check whether inside a container or not
  - Set is_ubuntu_inside_container fact
  - Check whether proxy settings are present or not


## :exclamation: Requirements
-----------------------------

None.


## :abcd: Role Variables
------------------------

| Variable           | Description                                                                                                   | Default Value |
|--------------------|---------------------------------------------------------------------------------------------------------------|---------------|
| `is_force_lookup`  | Lookup of custom additional facts does not happen if they already exist. This is to force looking up for them | `no`          |
| `is_test_url_list` | List of URLs to test to detect Internet connectivity/accessibility                                            | `[]`          |


## :link: Dependencies
----------------------

None.


## :loudspeaker: Facts
----------------------

This role creates the following facts that can be used by other roles or playbooks involved:

| Fact                              | Description                                                                                                                                                                 |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `is_ubuntu_behind_proxy`          | Version tagged for the current Ansible Role when executed _(this fact is **NOT** updated if present, unless `is_force_lookup` is set to `yes`)_                             |
| `is_ubuntu_inside_container`      | True when inside a container. This happens when PID 1 is neighter `init` or `systemd` _(this fact is **NOT** updated if present, unless `is_force_lookup` is set to `yes`)_ |
| `is_ubuntu_localhost`             | True when the Role target machine is `localhost` _(this fact is **NOT** updated if present, unless `is_force_lookup` is set to `yes`)_                                      |
| `is_ubuntu_network_reachable`     | True when all URLs passed in with `is_test_url_list` are reachable _(it also includes all URLs from `/etc/apt/sources.list` by default )_                                   |
| `is_ubuntu_url_reachable_list`    | List of all reachable URLs                                                                                                                                                  |
| `is_ubuntu_url_unreachable_list`  | List of all unreachable URLs                                                                                                                                                |


## :notebook: Example Playbook
------------------------------

Here an example of how to use this role in your playbooks:

```yaml
---
- hosts: servers
  remote_user: ubuntu   # optional (your remote user)
  gather_facts: yes     # optional

  roles:
    - { role: itnok.is_ubuntu }
```

## :microscope: Testing
-----------------------

This role supports testing using [Molecule](https://molecule.readthedocs.io/en/latest/index.html) to verify its functionalities in a generic environment.

Molecule is **NOT** needed to use the Role, but it is necessary to test it on a local installation or in CI.
An example of the use of Molecule for CI can be found in this repository's GitHub Actions.
To install Molecule please refer to the instructions on the [Molecule online documentation](https://molecule.readthedocs.io/en/latest/installation.html). If the necessary dependencies listed there are in place everything should be as simple as running:

```bash
$ python3 -m pip install --user "molecule[ansible,docker,lint]"
```

The tests are running inside containers built on-the-fly for the purpose _(to be as generic as possible)_. For this very reason Molecule needs Docker to be installed. If Podman is eventually a preferred alternative way to deal wih containers the needed command to install Molecule should be changed as follows:

```bash
$ python3 -m pip install --user "molecule[ansible,podman,lint]"
```

To use Podman the driver used by Molecule should also be changed in the `molecule/default/molecule.yml` file: lines #5-6 should be changed as follows:

```yaml
driver:
  name: podman
```

All tests, on top of checks for formatting, linting and idempotency, can be run using:

```bash
$ molecule test --parallel
```

_(The use of the optional `--parallel` option launching the test suite is strongly encouraged because, testing over multiple target containers it cut down the test runtime significantly!)_

Additional tests can be added to the `molecule/default/verify.yml` playbook should the need arise.


## :guardsman: License
----------------------

MIT _([read more](LICENSE.md))_
