# What 
Here you will find ansible scripts to deploy the following apps on a **standalon linux box** setting up **a user named operato**. With box we mean, depending on which cloud provider will use a different name (i.e Droplet, Instance, etc...)

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

## Files and folders

A deep dive on the content of each folder. 

```
group_vars:
    \_ all:
        \_  ansible_ssh_user: The user to authenticate against each box
        |_  operator_home: home of the operator user
        |_  operator_user_name: User name of the operator. Leave it as it is unless you know what you are doing
        |_  operator_user_comment: Comment of the user. The "description" part inside the /etc/passwd file
        |_  operator_user_id: UID of the user
        |_  ansible_ssh_common_args: Arguments when performing the ssh connection against the box.
inventory:
    \_ hosts_inventory:
roles:
    \_  cardano_cli:
    |_  cardano_node:
    |_  setup_server:
ansible_collection.yml: ansible modules to install. New modules must be added here.
install-cardano-cli.yml: cardano client role to install cardano-cli.
install-cardano-node.yml: cardano node role to install a cardano node
setup-node.yml: Setup a common ground inside the box. This means a mandatory setup to deploy the other roles.
install-full-stack.yml: Install all the roles. Starting with setup of course.
```

## What to do first

The following tasks are recommended (almost mandatory) to be performed before the installation of any app:

### 1. First install the ansible modules 

Executing the folowing command. This will be required for some roles:
```bash
$ ansible-galaxy collection install -r ansible_collection.yml
```

### 2. Setup and configure the node. 

This **does not** install any app. This will configure a common ground to install the apps. Remeber, each app is attached to a role and each role has a folder under the [roles](./roles) folder.

Append the IP address/es (FQDN, hostname make your pick) of the node/es inside the [inventory/hosts_inventory](./inventory/hosts_inventory) file.

```bash
$ vi inventory/hosts_inventory
```
```
[cardano-nodes]
111.222.223.xyz
```
Append or add your ssh key to the authorized key file:

```bash
$ ssh-add -L  > roles/setup_server/files/authorized_keys
```
