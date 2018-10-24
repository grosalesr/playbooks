# Description

My automated configurations for [Fedora](https://getfedora.org/)

# Requirements

* SSH must be enabled
* sudo access
* Python (on targets)

# Usage

The playbook doesn't contain any user information for security purposes. 

* `-k`: Ask SSH user password
* `-K`: Ask sudo user password
* `-u`: Remote user
* `-i`: Custom inventory

Depending on the scenario it can be executed as follows

```
ansible-playbook -Kki CustomInventory -u SomeUser play.yml
