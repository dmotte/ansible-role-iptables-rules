# ansible-role-iptables-rules

[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/dmotte/ansible-role-iptables-rules/release?logo=github&style=flat-square)](https://github.com/dmotte/ansible-role-iptables-rules/actions)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-dmotte.iptables__rules-blueviolet?logo=ansible&style=flat-square)](https://galaxy.ansible.com/dmotte/iptables_rules)

Ansible role to define **persistent iptables rules**.

In addition, this repository contains also a useful example of an iptables [`rules.v4`](test/rules.v4) file.

## Usage

1. Install this role using the `ansible-galaxy` CLI tool
2. You can then include it into the `tasks` section of your _Ansible Playbook_ like this:

   ```yaml
   - name: Include the dmotte.iptables_rules role
     include_role: { name: dmotte.iptables_rules }
     vars:
       ansible_become: yes
       rules_v4: "{{ lookup('file', 'rules.v4') }}"
       restart_services: [docker]
   ```

> **Note**: this role must be run as root (`ansible_become: yes`).

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
