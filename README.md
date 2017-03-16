# Ansible: nvm

Global NVM Installation for a system

Available on Ansible Galaxy: [pgkehle.nvm](https://galaxy.ansible.com/pgkehle/nvm)

Two directories created in `/usr/local`, `nvm_path` and `node_path` are set with group ownership of `nvm`.  This group is created and 
assigned to the ansible user. 
The configured version of node/npm are linked into `/usr/local/bin`.

## Tags and Variables

```YAML
tags:
  - init
  - configure

vars: 
  flags:
    - init            Downloads the nvm project and installs it globally
    - configure       Runs the configure scripts to install and change the default type
    - packages        Installed global packages using npm

  vm_client_type:     When set to `gui`, node will be allowed to open ports as non-root

  nvm:
    type:   "node"    `node`, `iojs`, etc
    ver:    "7.7.1"   version to install
```

## Examples

```YAML
- hosts: all  
  vars:
    nvm:
      type:               "node"
      ver:                "7.7.1"

  roles:
    - { role: pgkehle.nvm, flags: ['init'] }        # Install the nvm script to the server
    - { role: pgkehle.nvm, flags: ['configure'] }   # Configure nvm to use the version/type in the nvm variable 
    - { role: pgkehle.nvm, flags: ['packages'] }    # Install global packages 
```

## License

MIT

## Author Information

Paul Kehle  
@pgkehle ([twitter](https://twitter.com/pgkehle), [github](https://github.com/pgkehle), [linkedin](https://www.linkedin.com/in/pgkehle))

## For local development testing

```bash
rsync -av ~/code/ansible-nvm/* ~/.ansible/roles/pgkehle.nvm
```

