# What 
Here you will find ansible scripts to deploy the following apps on a **standalon linux box**. With box we mean, depending on which cloud provider will use a different name (i.e Droplet, Instance, etc...)

## Apps

Each app is implemented into a separate container providing the ability to decide which app is installed and whic not. Each app is attached to a role. You can find more information about how to setup each role inside [role folder](./roles)

- [x] Setup node: Setup basic stuff on the node.
- [x] Cardano node: Install the Cardano node.
    - [x] Support for Digital Ocean: By default we will use the Digital ocean droplets.
    - [ ] Support for AWS: Add the featur to choose under which cloud provider the cardano node will be installed.
- [x] Cardano cli: Install the cardano cli by pulling the docker image or building from this [github repo](https://github.com/adrabenche-org/yacc-builder.git)
- [ ] [Oura](https://github.com/txpipe/oura.git):  A implementation of a pipeline that connects to the tip of a Cardano node and submits Wto pluggable observers called "sinks".
- [ ] [Scrolls](https://github.com/txpipe/scrolls.git): A tool for building and maintaining read-optimized collections of Cardano's on-chain entities.

## Requirements

Before start

1) ssh access to the box, instance, droplet, etc you want to configure
2) ansible installed. Access [this link](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) for documentation.
3) Install the following ansible collections executing the folowing command:
```bash
$ ansible-galaxy collection install -r ansible_collection.yml
```

## Files and folders

A deep dive on the content of each folder. 

```
group_vars:
    \_ all:
        \_  ansible_ssh_user:
        |_  operator_home:
        |_  operator_user_name:
        |_  operator_user_comment:
        |_  operator_user_id:
        |_  ansible_ssh_common_args:
inventory:
    \_ hosts_inventory:
roles:
    \_  cardano_cli:
    |_  cardano_node:
    |_  setup_server:
ansible_collection.yml:
install-cardano-cli.yml:
install-cardano-node.yml:
setup-node.yml:
install-full-stack.yml:
```