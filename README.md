# Ansible Role: contojo.awx

**Ansible role for setting up contojo.awx.**

## Supported Platforms

| OS Family | Distribution  | Latest | Supported Version(s) | Comment |
|-----------|---------------|--------|----------------------|---------|
| Debian    | Debian        | :x: | 10 | |
| Debian    | Debian        | :heavy_check_mark: | 11 | |
| Debian    | Ubuntu        | :x: | 22.04 | |

## Requirements

Ansible Core 2.11 or higher.

## Variables

See [defaults/main.yml](defaults/main.yml) for all variables and their defaults.

## Dependencies

None.

## Example Playbook

```yaml
---

- hosts: all
  become: true
  gather_facts: true
  roles:
    - role: contojo.awx
```

## License and Author

- Author:: [aussielunix](https://gitlab.com/aussielunix/)
- Copyright:: 2022, [Contojo Pty Ltd](https://gitlab.com/aussielunix/)

Licensed under the [MIT License](https://opensource.org/licenses/MIT).
See [LICENSE](https://gitlab.com/aussielunix/ansible/awx/blob/main/LICENSE) file in repository.
