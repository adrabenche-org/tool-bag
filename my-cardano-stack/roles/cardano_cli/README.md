# What

This playbook only pull or build a cardano cli docker image. Does not start a container.

## Setup
Look after the `yes` field on the `mandatory` column to know which variables you need to setup

|File|Variable|Description|Mandatory|
|----|--------|-----------|---------|
|../../inventory/hosts_inventory|Under `[cardano_nodes]` tag|Place the IP address/es, URL, FQDN, hostname, etc of the box where you want to connect to.|`yes`
|../../group_vars/all|ansible_ssh_user|The user to authenticate against each box. This shall change depending on which distro and cloud you are using. i.e, if you are using Digital Ocean must be root, if you are using aws and Ubuntu must be ubuntu.|`yes`|
|../../group_vars/all|ansible_ssh_common_args|Arguments when performing the ssh connection against the box.inventory|`no`|
|./defaults/main.yml|image_build| Set to `true` if you want to build the cardano-cli image. You need to pay atention to two things: (1) If `true`, it's tested only for the `"https://github.com/adrabenche-org/yacc-builder.git"` repository and (2) if `true`, this takes several time. Like an hour or so (depending the box CPU and memory setup)|`no`|
|./defaults/main.yml|cardano_cli_git_repo|Cloned git repository to build the cardano-cli. This works only if `image_build` is set to true|`no`|
|./defaults/main.yml|cardano_cli_image_repo| The docker hub where the image is pulled. Works only if `image_build` is set to `false`|`no`|
|./defaults/main.yml|cardano_cli_image_tag| The tag of the decker image to pull. Depending the Docker hub this will change.|`no`|

## Playbook execution
```bash
$ cd ../../
$ ansible-playbook -i inventory/ -l cardano-nodes install-cardano-cli.yml
```