# ansible-role-unattended-upgrades

[![GitHub latest release](https://img.shields.io/github/v/release/dmotte/ansible-role-unattended-upgrades?logo=github&style=flat-square)](https://github.com/dmotte/ansible-role-unattended-upgrades/actions)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-dmotte.unattended__upgrades-blueviolet?logo=ansible&style=flat-square)](https://galaxy.ansible.com/dmotte/unattended_upgrades)

Ansible role to **configure unattended upgrades** on _Debian_.

This role has been tested with **Debian 12** (_bookworm_).

See the [official Debian wiki](https://wiki.debian.org/UnattendedUpgrades) for more information about unattended upgrades.

## Usage

1. Install this role using the `ansible-galaxy` CLI tool
2. You can then include it into the `tasks` section of your _Ansible Playbook_. See [`test/playbook.yml`](test/playbook.yml) for an example of how to do that. Remember to replace the role name with `dmotte.unattended_upgrades`.

> :bulb: **Tip**: if you want to see how a **systemd calendar event expression** will behave, you can use the `systemd-analyze` command:
>
> ```bash
> systemd-analyze calendar '*-*-* 6,18:00' --iterations 10
> ```
>
> See [the `systemd.time` manual](https://www.freedesktop.org/software/systemd/man/systemd.time.html) for more information.

> **Note**: this role must be run as root (`ansible_become: true`).

> **Note**: this role may not respect trailing newlines at the end of the file contents. In addition, if you choose to use the `lookup('ansible.builtin.file', ...)` filter, you should know that it performs an `rstrip` on the file contents by default (see [this](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_lookup.html) and [this](https://github.com/ansible/ansible/issues/30829)). In any case there should be no problem, as empty lines in the _unattended-upgrades_ and _systemd_ configuration files are ignored.

### Role variables

See [`defaults/main.yml`](defaults/main.yml).

## Development

If you want to contribute to this project, you can use the [`test/playbook.yml`](test/playbook.yml) file to test the role while editing it.

Place your inventory file (e.g. `hosts.yml`) inside the `test` folder.

Edit the `vars` section of the [`test/playbook.yml`](test/playbook.yml) file to match your scenario.

You can then **execute the playbook** against your host:

```bash
cd test/
ansible-playbook -i hosts.yml playbook.yml
```
