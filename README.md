# Ansible Role - nvm

Global NVM Installation and Control for a node server

Available on Ansible Galaxy: [isaackehle.nvm](https://galaxy.ansible.com/isaackehle/nvm)

Two directories created in `/usr/local`, `nvm_dir` and `node_dir` are set with group ownership of `nvm`. This group is created and
assigned to the ansible user.
The configured version of node/npm are linked into `/usr/local/bin`.

## Flags and Variables

```YAML
vars:
  flags:
    - init            # Downloads the nvm project and installs it globally
    - configure       # Runs the configure scripts to install and change the default type
    - clean           # Remove local packages folder and nvm
    - packages        # Install global and local packages
    - upgrade         # Upgrade global and local packages
    - restart         # Restart the node process(es)
    - processes       # Handle configuration of the process(es) on reboot

  enable_gui: true    # When set to true, node will be allowed to open ports as non-root

  generic_user:
    username: ''      # Username of the user for which to install


  nvm:
    type:   "node"    # `node`, `iojs`, etc
    ver:    "10.8.0"   # version to install
```

## Examples

```YAML
- hosts: all
  vars:
    nvm:
      type:               "node"
      ver:                "10.8.0"

  roles:
    - { role: isaackehle.nvm, flags: ['init'] }
    - { role: isaackehle.nvm, flags: ['clean'] }
    - { role: isaackehle.nvm, flags: ['configure'] }
    - { role: isaackehle.nvm, flags: ['upgrade'] }
    - { role: isaackehle.nvm, flags: ['processes'] }
    - { role: isaackehle.nvm, flags: ['restart'] }
```

```bash
export nvm="'nvm': {'type':'node', 'ver': '10.8.0'}"
export remote_base_dir="'remote_base_dir': '/srv/myserver/'"
export remote_deploy_dir="'remote_deploy_dir': '/srv/myserver/dist/server'"

ansible-playbook playbooks/nvm.yml -e "{'flags': ['init']}"
ansible-playbook playbooks/nvm.yml -e "{'flags': ['configure'], ${nvm }}"
ansible-playbook playbooks/nvm.yml -e "{'flags': ['port_enable'], ${nvm }}"
ansible-playbook playbooks/nvm.yml -e "{'flags': ['packages'], ${remote_base_dir}, ${remote_deploy_dir }}"
ansible-playbook playbooks/nvm.yml -e "{'flags': ['pm2'], ${remote_base_dir}, ${remote_deploy_dir }}"
```

## Linting

```bash
yamllint -c yamllint.yaml .
ansible-lint .
```

## License

MIT

## Author Information

Isaac Kehle
@isaackehle ([twitter](https://twitter.com/isaackehle), [github](https://github.com/isaackehle), [linkedin](https://www.linkedin.com/in/isaackehle))
