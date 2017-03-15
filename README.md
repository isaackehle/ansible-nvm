# Ansible: nvm

Global NVM Installation for a system

Available on Ansible Galaxy: [pgkehle.nvm](https://galaxy.ansible.com/pgkehle/nvm)

## Variables
```yaml
do_init:            Downloads the nvm project and installs it globally
do_configure:       Runs the configure scripts to install and change the default type
vm_client_type:     When set to `gui`, node will be allowed to open ports as non-root

nvm:
  type:   "node"    `node`, `iojs`, etc
  ver:    "7.7.1"   version to install
```

## Tags

```YAML
  tags:
    - install
    - configure
```

## Examples

```YAML

  - hosts: all  
    vars:
      nvm:
        type:               "node"
        ver:                "7.7.1"

    roles:
      - { role: pgkehle.nvm, do_init: true }        # Install the nvm script to the server
      - { role: pgkehle.nvm, do_configure: true }   # Configure nvm to use the version/type in the nvm variable 
```

## Noteworthy

This playbook modifies /etc/environment by adding a PATH definition to the end, which effectively overwrites the default set by the system.
Also, the two directories created in /usr/local, `nvm_path` and `node_path` are set with group ownership of `nvm`.  This group is created and 
assigned to the ansible user. 

## License

MIT

## Author Information

Paul Kehle  
@pgkehle ([twitter](https://twitter.com/pgkehle), [github](https://github.com/pgkehle), [linkedin](https://www.linkedin.com/in/pgkehle))

## For local development testing

```bash
rsync -av ~/code/ansible-nvm/* ~/.ansible/roles/pgkehle.nvm
```

