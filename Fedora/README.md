# Description

My automated configurations for [Fedora](https://getfedora.org/)

**Notice**

1. Create a custom inventory file or use the default.
1. Variables are defined in `play.yml`, read the playbook role to fullfil them as needed.
1. The playbook doesn't contain any remote user information for security purposes. This is provided at runtime, see `Usage`


# Requirements

* SSH must be enabled
* sudo access
* Python (on targets)


# Usage

The workflow proposed is to provide the `remote Ansible user` and that `SSH` and `become` password are different. Therefore Ansible will ask for these information at playbook's runtime. 

The flags needed to acomplish this are the following:

* `-k`: Ask SSH user password
* `-K`: Ask sudo user password
* `-u`: Remote user
* `-i`: Custom inventory

Depending on the scenario it can be executed as follows

```
ansible-playbook -Kki CustomInventory -u SomeUser play.yml
