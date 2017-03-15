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
    - packages
    - upgrade
```

## Examples

```YAML

  - hosts: all  
    vars:

    roles:
      - { role: pgkehle.nvm }
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

