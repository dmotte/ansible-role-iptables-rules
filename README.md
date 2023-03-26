# ansible-role-iptables-rules

[![GitHub latest release](https://img.shields.io/github/v/release/dmotte/ansible-role-iptables-rules?logo=github&style=flat-square)](https://github.com/dmotte/ansible-role-iptables-rules/actions)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-dmotte.iptables__rules-blueviolet?logo=ansible&style=flat-square)](https://galaxy.ansible.com/dmotte/iptables_rules)

Ansible role to define **persistent iptables rules**.

In addition, this repository contains also a useful example of an iptables [`rules.v4`](test/rules.v4) file.

## Usage

1. Install this role using the `ansible-galaxy` CLI tool
2. You can then include it into the `tasks` section of your _Ansible Playbook_. See [`test/playbook.yml`](test/playbook.yml) for an example of how to do that. Remember to replace the role name with `dmotte.iptables_rules`.

> **Note**: this role must be run as root (`ansible_become: true`).

> **Note**: this role may not respect trailing newlines at the end of the rules text. In addition, the `lookup('ansible.builtin.file', ...)` filter performs an `rstrip` on the file contents by default (see [this](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_lookup.html) and [this](https://github.com/ansible/ansible/issues/30829)). In any case there should be no problem, as empty lines are ignored by _iptables-persistent_.

### Role variables

See [`defaults/main.yml`](defaults/main.yml).

## Development

If you want to contribute to this project, you can use the [`test/playbook.yml`](test/playbook.yml) file to test the role while editing it.

Place your inventory file (e.g. `hosts.yml`) inside the `test` folder.

Edit the `vars` section of the [`test/playbook.yml`](test/playbook.yml) file to match your scenario. Then put your `rules.v4` and/or `rules.v6` files into the `test` folder.

You can then **execute the playbook** against your host:

```bash
cd test/
ansible-playbook -i hosts.yml playbook.yml
```
