Ansible Role: Go language SDK
=============================

[![CI](https://github.com/hybridadmin/ansible-role-golang/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/hybridadmin/ansible-role-golang/actions/workflows/build.yml)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-hybridadmin.golang-blue.svg)](https://galaxy.ansible.com/hybridadmin/golang)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/hybridadmin/ansible-role-golang/master/LICENSE)

Role to download and install the [`Go language SDK`](https://golang.org/).

Requirements
------------

* Ansible >= 2.9

Role Variables
--------------

The following variables will change the behavior of this role (default values
are shown below):

```yaml
# Go language SDK version number
golang_version: '1.15.8'

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

* `1.16`
* `....`
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

> The correct hash can be found at [`Downloads`](https://golang.org/dl/) and should be for Go SDK version specified in the `golang_version` variable


Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - role: hybridadmin.golang
       golang_gopath: '$HOME/workspace-go'
```

Role Facts
----------

This role exports the following Ansible facts for use by other roles:

* `ansible_local.golang.general.version`

    * e.g. `1.7.3`

* `ansible_local.golang.general.home`

    * e.g. `/opt/golang/1.7.3`


Development & Testing
---------------------

To develop or test you'll need to have installed the following:

* Linux (e.g. [`Ubuntu`](http://www.ubuntu.com/))
* [`Docker`](https://www.docker.com/)
* [`Python3`](https://www.python.org/) (including python3-pip)
* [`Ansible`](https://www.ansible.com/)
* [`Molecule`](http://molecule.readthedocs.io/)


Note: some of the dependencies need `sudo` permission to install.

License
-------

MIT

Author Information
------------------

[`Hybridadmin`](https://github.com/hybridadmin)
