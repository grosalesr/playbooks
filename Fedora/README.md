# Description

Fedora automated configuration

# Requirements

* SSH must be enabled
* sudo access

# Usage

The playbook doesn't contain any user information for security purposes. 

* `-k`: Ask SSH user password
* `-K`: Ask sudo user password
* `-u`: Remote user
* `-i`: Custom inventory

Depending on the scenario it can be executed as follows, notice this example uses ansible3 (python 3)

```
ansible-playbook-3 -Kki CustomInventory -u SomeUser play.yml
```
