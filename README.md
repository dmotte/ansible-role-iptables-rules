# ansible-role-iptables-rules

[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/dmotte/ansible-role-iptables-rules/release?logo=github&style=flat-square)](https://github.com/dmotte/ansible-role-iptables-rules/actions)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-dmotte.iptables__rules-blueviolet?logo=ansible&style=flat-square)](https://galaxy.ansible.com/dmotte/iptables_rules)

Ansible role to define **persistent iptables rules**.

In addition, this repository contains also a useful example of an iptables [`rules.v4`](test/rules.v4) file.

## Usage

1. Install this role using the `ansible-galaxy` CLI tool
2. You can then include it into the `tasks` section of your _Ansible Playbook_ like this:

   ```yaml
   - name: Set persistent iptables rules
     ansible.builtin.include_role: { name: dmotte.iptables_rules }
     vars:
       ansible_become: true
       rules_v4: "{{ lookup('ansible.builtin.file', 'rules.v4') }}"
       restart_services: [docker]
   ```

> **Note**: this role must be run as root (`ansible_become: true`).

> **Note**: this role may not respect trailing newlines at the end of the rules text. In addition, the `lookup('ansible.builtin.file', ...)` filter performs an `rstrip` on the file contents by default (see [this](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_lookup.html) and [this](https://github.com/ansible/ansible/issues/30829)). In any case there should be no problem, as empty lines are ignored by _iptables-persistent_.

### Role variables

| Variable           | Description                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------- |
| `rules_v4`         | If set, content for the `/etc/iptables/rules.v4` file. If not set, that file won't be created |
| `rules_v6`         | If set, content for the `/etc/iptables/rules.v6` file. If not set, that file won't be created |
| `restart_services` | List of services to be restarted after restarting _iptables-persistent_ (default: `[]`)       |

## Development

If you want to contribute to this project, you can use the [`test/playbook.yml`](test/playbook.yml) file to test the role while editing it.

Place your inventory file (e.g. `hosts.yml`) inside the `test` folder.

Edit the `vars` section of the [`test/playbook.yml`](test/playbook.yml) file to match your scenario. Then put your `rules.v4` and/or `rules.v6` files into the `test` folder.

You can then **execute the playbook** against your host:

```bash
cd test/
ansible-playbook -i hosts.yml playbook.yml
```
