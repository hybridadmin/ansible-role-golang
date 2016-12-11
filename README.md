Ansible Role: Go language SDK
=============================

[![Build Status](https://travis-ci.org/gantsign/ansible-role-golang.svg?branch=master)](https://travis-ci.org/gantsign/ansible-role-golang)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-gantsign.golang-blue.svg)](https://galaxy.ansible.com/gantsign/golang)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/gantsign/ansible-role-golang/master/LICENSE)

Role to download and install the [Go language SDK](https://golang.org/).

Requirements
------------

* Ansible >= 2.0

* Linux Distribution

    * Debian Family

        * Debian

            * Wheezy (7)
            * Jessie (8)

        * Ubuntu

            * Trusty (14.04)
            * Xenial (16.04)

    * RedHat Family

        * CentOS

            * 6
            * 7

    * Note: other versions are likely to work but have not been tested.

Role Variables
--------------

The following variables will change the behavior of this role (default values
are shown below):

```yaml
# Go language SDK version number
golang_version: '1.7.4'

# Mirror to download the Go language SDK redistributable package from
golang_mirror: 'https://storage.googleapis.com/golang'

# Base installation directory the Go language SDK distribution
golang_install_dir: '/opt/go/{{ golang_version }}'

# Directory to store files downloaded for Go language SDK installation
golang_download_dir: "{{ x_ansible_download_dir | default(ansible_env.HOME + '/.ansible/tmp/downloads') }}"

# Location for GOPATH environment variable
golang_gopath:
```

### Supported Go language SDK Versions

The following versions of Go language SDK are supported without any additional
configuration (for other versions follow the Advanced Configuration
instructions):

* `1.7.4`
* `1.7.3`

Advanced Configuration
----------------------

The following role variable is dependent on the Go language SDK version; to use
a Go language SDK version **not pre-configured by this role** you must configure
the variable below:

```yaml
# SHA256 sum for the redistributable package (i.e. "go{{ golang_version }}.linux-amd64.tar.gz")
golang_redis_sha256sum: '6e3e9c949ab4695a204f74038717aa7b2689b1be94875899ac1b3fe42800ff82'
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - role: gantsign.golang
       golang_gopath: '$HOME/workspace-go'
```

Role Facts
----------

This role exports the following Ansible facts for use by other roles:

* `ansible_local.golang.general.version`

    * e.g. `1.7.3`

* `ansible_local.golang.general.home`

    * e.g. `/opt/golang/1.7.3`

More Roles From GantSign
------------------------

You can find more roles from GantSign on
[Ansible Galaxy](https://galaxy.ansible.com/gantsign).

Development & Testing
---------------------

This project uses [Molecule](http://molecule.readthedocs.io/) to aid in the
development and testing; the role is unit tested using
[Testinfra](http://testinfra.readthedocs.io/) and
[pytest](http://docs.pytest.org/).

To develop or test you'll need to have installed the following:

* Linux (e.g. [Ubuntu](http://www.ubuntu.com/))
* [Docker](https://www.docker.com/)
* [Python](https://www.python.org/) (including python-pip)
* [Ansible](https://www.ansible.com/)
* [Molecule](http://molecule.readthedocs.io/)

To run the role (i.e. the `tests/test.yml` playbook), and test the results
(`tests/test_role.py`), execute the following command from the project root
(i.e. the directory with `molecule.yml` in it):

```bash
molecule test
```

License
-------

MIT

Author Information
------------------

John Freeman

GantSign Ltd.
Company No. 06109112 (registered in England)