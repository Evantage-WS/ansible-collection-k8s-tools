# Role: install_kubectl

This role installs and sets up `install_kubectl` for Kubernetes tooling.

## Requirements

- Ansible 2.9 or higher
- Targeted OS: openSUSE /SUSE Linux Enterprise (SLES)

## Role Variables

Update the variables as required in `~/vars.yml`:

```bash
home_user: "" # home_user
```

## Dependencies

None.

## Example

To use this role, include it in your playbook as follows:

### local
```bash
# site.yml
---
- hosts: localhost
  become: yes
  vars_files:
    - ~/vars.yml
  collections:
    - evantage_ws.k8s_tools
  roles:
    - install_kubectl
```

### Remote
```bash
# site.yml
---
- hosts: <hosts> # Remote Server
  become: yes
  vars_files:
    - ~/vars.yml
  collections:
    - evantage_ws.k8s_tools
  roles:
    - install_kubectl
```