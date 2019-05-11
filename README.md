# Description

Playbooks for [Fedora](https://getfedora.org/), [CentOS](https://www.centos.org/) and [KDE Neon](https://neon.kde.org/).

**Notice**

1. Create a custom inventory file or use the default.
1. Variables are defined in `play.yml`, read the playbook role to fullfil them as needed.
1. The playbook doesn't contain any remote user information for security purposes. This is provided at runtime, see `Execution`

## Execution

The workflow proposed is to provide the `remote Ansible user` and that `SSH` and `become` password are different. Therefore Ansible will ask for these information at playbook's runtime. 

The flags needed to acomplish this are the following:

* `-K`: Ask sudo user password
* `-k`: Ask SSH user password
* `-i`: Custom inventory
* `-u`: Remote user


Also, `play.yml` has the `target` variable, this allow us to pass targets on runtime instead of having to modify `play.yml`.

This is achieved using `--extra-vars` flag, in the example below the target is wave0 (servers section in the inventory file

```
ansible-playbook -Kki inventory -u root play.yml --extra-vars "target=prod"
```

**notice** `-u` flag is only needed when the user on the targets is different from the user that is executing the playbook.

Also, `tags` are used to make playbooks flexible enough to execute or omit specific tasks in the playbook's role.


* `--tags`: Only executes a given task or tasks(separated by comma) from a role
* `--skip-tags`: Skips a given task or tasks(separated by comma) from a role

eg:

From the common role, run *only* the task with tag `updateOS`, which will update all targets on the inventory file

```
ansible-playbook -Kki inventory -u root play.yml --extra-vars "target=all" --tags "updateOS"
```

From the common role, run everything **except** the task with tag `flathub`, which will be executed for the servers under *qa* category.

```
ansible-playbook -Kki inventory -u root play.yml --extra-vars "target=qa" --skip-tags "flathub"
```

## Roles

Below you will find information about current roles and what they do

### Fedora

* common
    * Setup RPM Fusion
    * Installs multimedia packages
    * Installs some system utilities
    * Setup flathub repository
    * Full system update
* development
    * Installs KDevelop
    * Installs virtualization group packages
    * Starts virtualization service
    * Append a given user to libvirt group
* docker
    * Removes previous docker versions
    * Adds docker repository
    * Installs docker-ce
    * Install docker-compose
    * Append a given user to the docker group
* plasma
    * Removes unneeded? packages
    * Install [redshift](https://github.com/jonls/redshift) applet for Plasma desktop
* upgrade (EXPERIMENTAL)
    * Upgrade Fedora releases, eg: 28 --> 29, 29 --> 30, etc
* ftp
    * An FTP server that works only for local accounts

### CentOS

**WIP**

* moodle
* virtHost

### KDE Neon

Setups the requirements needed to develop for KDE using KDE Neon