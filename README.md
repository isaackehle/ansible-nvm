# Ansible: nvm

Global NVM Installation for a system

Available on Ansible Galaxy: [pgkehle.nvm](https://galaxy.ansible.com/pgkehle/nvm)

## Variables
```yaml
deploy_dir:     Required for where the base path lives
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
      - { role: pgkehle.nvm, do_init: true }
      - { role: pgkehle.nvm, do_configure: true }
```

## Noteworthy

This playbook modifies /etc/environment by adding a PATH definition to the end, which effectively overwrites the default set by the system.
Also, the two directories created in /usr/local, `nvm_path` and `node_path` are set with group ownership of `admin`.  Ensure your user has this group.

## License

MIT

## Author Information

Paul Kehle  
@pgkehle ([twitter](https://twitter.com/pgkehle), [github](https://github.com/pgkehle), [linkedin](https://www.linkedin.com/in/pgkehle))

## For local development testing

```bash
rsync -av ~/code/ansible-nvm/* ~/.ansible/roles/pgkehle.nvm
```

