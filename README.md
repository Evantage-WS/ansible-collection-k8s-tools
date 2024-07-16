# k8s-tools

Based on https://github.com/somaz94/ansible-k8s-iac-tool and https://github.com/Pandemonium1986/ansible-collection-k8s-toolbox

This Ansible collection is dedicated to setting up Kubernetes tooling on the SUSE Linux Family. The collection comprises several roles, each focusing on a specific tool or configuration:

- `install_kubectl`     : Install kubectl binary
- `install_kubectx`     : Install kubectx binary
- `install_krew`        : Install krew binary
- `install_krew_plugins`: Install specified krew plugins
- `install_helm`        : Install helm
- `install_k9s`         : Install K9s
- `setup_bashrc`        : Adds specific configurations to the bashrc

<br/>

## Requirements

- Ansible 2.9 or higher
- Targeted OS: openSUSE /SUSE Linux Enterprise (SLES)
<br/>

## Example Playbook

### Running Locally

#### 1. Setting Up the Variable File

Define the necessary variables in the `vars.yml` file:
```bash
# vars.yml
home_user: "root"
krew_plugins:
  - "ctx"
  - "neat"
  - "ns"
  # more...
```

- For a comprehensive list of available krew plugins, visit the official [krew plugins directory](https://krew.sigs.k8s.io/plugins/). For the krew version, visit https://github.com/kubernetes-sigs/krew/releases/

#### 2. Creating the Playbook

Write the playbook in the `site.yml` file:
```bash
# site.yml
---
- hosts: localhost
  become: yes
  vars_files:
    - ~/vars.yml
  collections:
    - evantage.k8s-tools
  roles:
    - setup_bashrc
    - install_kubectl
    - install_kubectx
    - install_krew
    - install_krew_plugins
    - install_helm
    - install_k9s

```

#### 3. Running the Playbook

Execute the playbook with the following command:
```bash
ansible-playbook site.yml
```

<br/>

### Post-Task Actions

After the tasks have been completed, apply the changes on the installed machine by running:
```bash
source ~/.bashrc
```
- This command will apply any changes made in the .bashrc file to the current shell session.


<br/>

## Role Variables

The variables below can be modified in the `~/vars.yml` file as per your requirements:

- `home_user`: User for which the tooling setup should be applied.
- `krew_version`: Desired version of krew. Default: `v0.4.4`
- `krew_plugins`: List of krew plugins to be installed.

<br/>

## Dependencies

None.

<br/>

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

