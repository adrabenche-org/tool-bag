# What

This playbook setup a common ground so we can execute the other playbooks.

## Setup
Look after the `yes` field on the `mandatory` column to know which variables you need to setup

|File|Variable|Description|Mandatory|
|----|--------|-----------|---------|
|../../inventory/hosts_inventory|Under `[cardano_nodes]` tag|Place the IP address/es, URL, FQDN, hostname, etc of the box where you want to connect to.|`yes`
|./files/authorized_keys|*file content*|This is the `.ssh/authorized_keys` file containing the ssh keys to access the server. An execution of `ssh-add -L  > ./files/authorized_keys` shall work|`yes`|
|../../group_vars/all|ansible_ssh_user|The user to authenticate against each box. This shall change depending on which distro and cloud you are using. i.e, if you are using Digital Ocean must be root, if you are using aws and Ubuntu must be ubuntu.|`yes`|
|./defaults/main.yml|cardano_node_initial_apps| Basically, the packets to install using the deb package manager|`no`|
|../../group_vars/all|operator_home|Home of the operator user|`no`|
|../../group_vars/all|operator_user_name|User name of the operator. Leave it as it is unless you know what you are doing.|`no`|
|../../group_vars/all|operator_user_comment|Comment of the user. The "description" part inside the /etc/passwd file|`no`|
|../../group_vars/all|operator_user_id|UID of the user|`no`|
|../../group_vars/all|ansible_ssh_common_args|Arguments when performing the ssh connection against the box.inventory|`no`|

## Playbook execution
```bash
$ cd ../../
$ ansible-playbook -i inventory/ -l cardano-nodes setup-node.yml 
```
