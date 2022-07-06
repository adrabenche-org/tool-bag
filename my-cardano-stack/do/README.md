# What 
Deploy on standalone Digital Ocean Droplet, or any box with root access via ssh.

If you want to save some time, the default setup will work on:
* Digital Ocean cloud or box with ssh access
* A separate volume for the cardanodb
* Add the ip addres inside the `./inventory/hosts_inventory`
* Add the ssh keys inside `./roles/setup_server/files/authorized_keys`

## Deploy

You must deploy the ansible playbboks on the following order. To know how to do it you must check on each role `README.md` file.

1. [setup_server](roles/setup_server/README.md)
2. [cardano_node](roles/cardano_node/README.md)
3. [cardano_cli](roles/cardano_cli/README.md)

Or, if you want to deploy all the ansible playbooks with all the apps, just configure each role (as said on each README.md file previously mentioned) and execute
```bash
$ ansible-playbook -i inventory/ -l cardano-nodes install-full-stack.yml
```