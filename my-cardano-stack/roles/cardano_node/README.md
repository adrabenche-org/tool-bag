# What

This playbook install a cardano node using a Docker container.

## Setup
Look after the `yes` field on the `mandatory` column to know which variables you need to setup

|File|Variable|Description|Mandatory|
|----|--------|-----------|---------|
|../../inventory/hosts_inventory|Under `[cardano_nodes]` tag|Place the IP address/es, URL, FQDN, hostname, etc of the box where you want to connect to.|`yes`
|../../group_vars/all|ansible_ssh_user|The user to authenticate against each box. This shall change depending on which distro and cloud you are using. i.e, if you are using Digital Ocean must be root, if you are using aws and Ubuntu must be ubuntu.|`yes`|
|./defaults/main.yml|setup_fs_for_cardanodb|Set to `true` if you want to install the cardano stoff in a separate file system. If true, setup the `cardano_node_db_fs` variable. Else, if you want all in the same filesystem leave it to `false`|`yes`|
|./defaults/main.yml|cardano_node_db_fs| If `setup_fs_for_cardanodb` was set to true, then this is the filesystem to use as the filesystem for the cardano stuff. If `setup_fs_for_cardanodb` is `false`; then this variable will be ignored.|`yes`|
|./defaults/main.yml|cardano_node_deploy_folder|the folder inside the filesystem where the cardano stuff will be deployed|`no`|
|./defaults/main.yml|cardano_node_version|Version of the cardano-node|`no`|
|./defaults/main.yml|cardano_node_config_files|List of the config files ofr the node|`no`|
|./defaults/main.yml|cardano_node_config_url|URL to download the cardano-node config files|`no`|
|./defaults/main.yml|docker_network|Name of the docker network to be created|`no`|
|./defaults/main.yml|network_mode|Network mode of the docker network specified in `docker_network`|`no`|
|./files/keysandaddresses|files|All the cardano node keys, certs. Like payment address, stake vkey, skey, etc. If empty, no key will be pushed; but the folder will be created. You can, if you want, to manually push the keys, or use another folder.|`no`|
|../../group_vars/all|operator_home|Home of the operator user|`no`|
|../../group_vars/all|operator_user_name|User name of the operator. Leave it as it is unless you know what you are doing.|`no`|
|../../group_vars/all|operator_user_id|UID of the user|`no`|
|../../group_vars/all|ansible_ssh_common_args|Arguments when performing the ssh connection against the box.inventory|`no`|

## Playbook execution
```bash
$ cd ../../
$ ansible-playbook -i inventory/ -l cardano-nodes install-cardano-node.yml 
```
