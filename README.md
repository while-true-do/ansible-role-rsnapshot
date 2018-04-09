[![Build Status](https://travis-ci.org/while-true-do/ansible-role-rsnapshot.svg?branch=master)](https://travis-ci.org/while-true-do/ansible-role-rsnapshot)

# Ansible Role: rsnapshot
| Install and configure rsnapshot.

## Motivation

Easy, everyone needs backups. :) 
And keep in mind:
**No Backup, No Mercy**

## Installation

Install from [Ansible Galaxy](https://galaxy.ansible.com/while-true-do/rsnapshot)

```
ansible-galaxy install while-true-do.rsnapshot
```

Install from [Github](https://github.com/while-true-do/ansible-role-rsnapshot)

```
git clone https://github.com/while-true-do/ansible-role-rsnapshot.git while-true-do.rsnapshot
```

## Requirements

Used Modules:

-   [packages](http://docs.ansible.com/ansible/latest/package_module.html)
-   [template](http://docs.ansible.com/ansible/latest/template_module.html)

## Dependencies

<!--
Describe, if other roles are needed and link them here.
You also have to put the dependencies in the requirements.yml.

```
ansible-galaxy install -r requirements.yml
```

If nothing is needed, please write "None."
-->

## Role Variables

<!-- 
The variable files should explain itself and pasted/linked here.
Explanation should be done **in** the files, if needed. 
-->

```yaml
# defaults/main.yml
wtd_rsnapshot_state: "present"
wtd_rsnapshot_packages: "rsnapshot"

wtd_rsnapshot_config_version: 1.2

wtd_rsnapshot_config_snapshot_root: "/backup"

wtd_rsnapshot_config_cmd_rm: "/usr/bin/rm"
wtd_rsnapshot_config_cmd_rsync: "/usr/bin/rsync"
wtd_rsnapshot_config_cmd_logger: "/usr/bin/logger"

wtd_rsnapshot_config_retains:
  - name: "alpha"
    value: "6"
  - name: "beta"
    value: "7"
  - name: "gamma"
    value: "4"
  - name: "delta"
    value: "3"

wtd_rsnapshot_config_verbose: 3
wtd_rsnapshot_config_loglevel: 3
wtd_rsnapshot_config_logfile: "/var/log/rsnapshot"

wtd_rsnapshot_config_lockfile: "/var/run/rsnapshot.pid"

wtd_rsnapshot_config_backups:
  - backup: /home/
    target: localhost/
```

## Example Playbook

Simple Example:

```yaml
- hosts: servers 
  roles:
    - { role: while-true-do.rsnapshot }
```

Advanced Example:

```yaml
- hosts: servers 
  roles:
    - { role: while-true-do.rsnapshot, wtd_rsnapshot_config_ssh_args: -p 1022 }
```

## Testing

All tests are located in [test directory](./tests/).

Basic testing:

```
bash ./tests/test-spelling.sh
bash ./tests/test-ansible.sh
```

## Contribute / Bugs

Thank you so much for considering to contribute. Every contribution helps us.
We are really happy, when somebody is joining the hard work. Please have a look 
at the links first.

-   [Code of Conduct](./docs/CODE_OF_CONDUCT.md)
-   [Contribution Guidelines](./docs/CONTRIBUTING.md)
-   [Create an issue or Request](https://github.com/while-true-do/ansible-role-rsnapshot/issues)
-   [See who was contributing already](https://github.com/while-true-do/ansible-role-rsnapshot/graphs/contributors)

## License

This work is licensed under a [BSD License](https://opensource.org/licenses/BSD-3-Clause).

## Author Information

Site: [while-true-do.org](https://while-true-do.org)

Mail: [hello@while-true-do.org](mailto:hello@while-true-do.org)
