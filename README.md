# Ansible Role - nvm

Global NVM Installation and Control for a node server

Available on Ansible Galaxy: [pgkehle.nvm](https://galaxy.ansible.com/pgkehle/nvm)

Two directories created in `/usr/local`, `nvm_path` and `node_path` are set with group ownership of `nvm`.  This group is created and 
assigned to the ansible user. 
The configured version of node/npm are linked into `/usr/local/bin`.

## Flags and Variables

```YAML
vars: 
  flags:
    - init            # Downloads the nvm project and installs it globally
    - configure       # Runs the configure scripts to install and change the default type
    - wipe            # Remove local packages folder
    - packages        # Install global packages using npm, local packages using yarn
    - upgrade         # Upgrade global packages using npm, local packages using yarn
    - restart         # Restart the node process(es)
    - processes       # Handle configuration of the process(es) on reboot

  vm_client_type:     # When set to `gui`, node will be allowed to open ports as non-root
                      # When set to `worker` or `scheduler`, tunnels will be auto stopped

  nvm:
    type:   "node"    # `node`, `iojs`, etc
    ver:    "7.7.4"   # version to install
```

## Examples

```YAML
- hosts: all  
  vars:
    nvm:
      type:               "node"
      ver:                "7.7.1"

  roles:
    - { role: pgkehle.nvm, flags: ['init'] }        
    - { role: pgkehle.nvm, flags: ['wipe'] }
    - { role: pgkehle.nvm, flags: ['configure'] }
    - { role: pgkehle.nvm, flags: ['upgrade'] }     
    - { role: pgkehle.nvm, flags: ['processes'] }     
    - { role: pgkehle.nvm, flags: ['restart'] }     
```

```bash
export nvm="'nvm': {'type':'node', 'ver': '7.8.0'}"
export deploy="'deploy_dir': '/opt/servers/node'"

ansible-playbook playbooks/nvm.yml -e "{'flags': ['init']}" 
ansible-playbook playbooks/nvm.yml -e "{'flags': ['configure'], ${nvm}}" 
ansible-playbook playbooks/nvm.yml -e "{'flags': ['port_enable'], ${nvm}}" 
ansible-playbook playbooks/nvm.yml -e "{'flags': ['packages'], ${deploy}}" 
ansible-playbook playbooks/nvm.yml -e "{'flags': ['pm2'], ${deploy}}"
```


## License

MIT

## Author Information

Paul Kehle  
@pgkehle ([twitter](https://twitter.com/pgkehle), [github](https://github.com/pgkehle), [linkedin](https://www.linkedin.com/in/pgkehle))

## For local development testing

```bash
rsync -av --delete ~/code/ansible-nvm/* ~/.ansible/roles/pgkehle.nvm
```

