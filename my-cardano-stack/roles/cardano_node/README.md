# What

Files and folders from the `cardano-node` that exeutes this role to install and setup  cardano node.

## Before start

* Linux instance, box, droplet, etc.
* Ubuntu user already setup.

## Files and folders

```
defaults: Default vars for the cardano-node
        \_ node.yml
                    \_ cardano_node_version: Version of the cardanos node.
                    |_ cardano_node_config_files: List of the cardano node config files.

files: Files to push to the server.
     \_ keysandadreses: Folder to place key material of the node, i.e stake verification key, payment keys...
                      \_ .gitignore: By default keys placed here won't be pushed for privacy reaasons.
tasks: Tasks to execute
     \_ playbook.yml: Main playbook.
```
