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
-   [systemd](https://docs.ansible.com/ansible/latest/systemd_module.html)
-   [shell](https://docs.ansible.com/ansible/latest/shell_module.html)
-   [command](https://docs.ansible.com/ansible/latest/command_module.html)
-   [file](https://docs.ansible.com/ansible/latest/file_module.html)

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
  vars:
    - wtd_rsnapshot_config_shapshot_root: '/backup/'
    - wtd_rsnapshot_config_retains:
      - name: 'daily'
        value: '7'
    - wtd_rsnapshot_config_backups:
      - backup: /home/cinux
        target: home/
```

Advanced Example:
rsnapshot is not designed to run multiple instance at the same time by using one config-file.
Because of this its possible to set the `wtd_rsnapshot_config_multi` variable as following:
```yaml
- hosts: servers 
  roles:
    - { role: while-true-do.rsnapshot }
  vars:
    - wtd_rsnapshot_config_multi:
      - name: documents-cinux
        retains:
          - name: daily
            value: '7'
          - name: weekly
            value: '4'
            time: '02:15'
        time: '02:00'
        backups:
          - src: /home/cinux/documents
            dest: homes/
        snapshot_root: '/backup-documents'
      - name: pictures-cinux
        retains:
          - name: daily
            value: '7'
          - name: weekly
            value: '4'
            time: '02:15'
        time: '02:00'
        backups:
          - src: /home/cinux/pictures
            dest: homes/
        snapshot_root: '/backup'
```

For each entry a seperate configuration file gets created under /etc/rsnapshot.
Additionaly to this for each retains we create a timer which trigger the rsnapshot run if the time is arrived. And of course you can create for each retains a different time. This helps to run different retains on different times.

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
