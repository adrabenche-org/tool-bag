# What 
Here you will find ansible scripts to deploy the following apps on a **standalone linux box** setting up **a new user named operator** to run a cardano node with some tools. With box we mean, depending on which cloud provider will use a different name (i.e Droplet, Instance, etc...)

If you want to save some time, the default setup will work on:
* Digital Ocean cloud
* Ubuntu box
* A separate volume for the cardanodb
* Add the ip addres inside the `./inventory/hosts_inventory`
* Add the ssh keys inside `./roles/setup_server/files/authorized_keys`
* Go to the last line.

## Apps

Each app is implemented into a separate container providing the ability to decide which app is installed and whic not. Each app is attached to a role. You can find more information about how to setup each role inside [role folder](./roles).

- [x] Setup node: Setup basic stuff on the node.
- [x] Cardano node: Install the Cardano node.
    - [x] Support for Digital Ocean: By default we will use the Digital ocean droplets.
    - [ ] Support for AWS: Add the features to support deploy on AWS instances
- [x] Cardano cli: Install the cardano cli by pulling the docker image or building from this [github repo](https://github.com/adrabenche-org/yacc-builder.git)
- [ ] [Oura](https://github.com/txpipe/oura.git):  A implementation of a pipeline that connects to the tip of a Cardano node and submits Wto pluggable observers called "sinks".
- [ ] [Scrolls](https://github.com/txpipe/scrolls.git): A tool for building and maintaining read-optimized collections of Cardano's on-chain entities.

## Requirements

Before start

1) ssh access to the box, instance, droplet, etc you want to configure
2) ansible installed. Access [this link](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) for documentation.

## Deploy

You must deploy the ansible playbboks on the following order. To know how to do it you must check on each role `README.md` file.

1. [setup_server](roles/setup_server/README.md)
2. [cardano_node](roles/cardano_node/README.md)
3. [cardano_cli](roles/cardano_cli/README.md)

Or, if you want to deploy all the ansible playbooks with all the apps, just configure each role (as said on each README.md file previously mentioned) and execute
```bash
$ ansible-playbook -i inventory/ -l cardano-nodes install-full-stack.yml
```