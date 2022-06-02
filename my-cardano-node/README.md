# What

This is a quick way to have a cardano node up and running to perform tests. It's not intended to have a perfect setup. Do his work and that's it. 
The idea is follow the KISS motto.

# Download config files and create db folder
It's very important to understand that you need a filesystem with enough space to hold the `cardanodb` folder. This is because this filesystem will hold the cardano blockchain.

In this example, I have a FS with enough space inside `~/deploy` folder.

```bash
$ df -h ~/deploy
```
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda        248G   76M  236G   1% /home/ubuntu/deploy
```
Now, let's download the config files for the cardano node on testnet:

```bash
$ cd ~/deploy
$ mkdir -p relay/conf_files/testnet
$ mkdir -p cardanodb
$ mkdir -p keysandaddresses
$ cd relay/conf_files/testnet
$ wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/testnet-config.json
$ wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/testnet-shelley-genesis.json
$ wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/testnet-byron-genesis.json
$ wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/testnet-alonzo-genesis.json
$ wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/testnet-topology.json
$ cd ~/deploy
```
# Start the `cardano-node`
Start the cardano-node where

* `~/deploy/cardanodb`: It's where 
    - The cardano blockchain lives.
    - The `node.socket` file is. Keep this in mind because **you will need it whenever you want to use a cardano-cli connected to this node**.
* `~/deploy/cardanodb/relay/conf_files/testnet`: It's where the config files are
* `~/deploy/cardanodb/keysandaddresses`: Where your key material should be.
`

```bash
$ sudo docker run -d \
--name cardano-node  \
--hostname cardano-node \
-v ${PWD}/cardanodb:/var/lib/cardanodb \
-v ${PWD}/relay/conf_files/testnet:/etc/cardano-node \
-v ${PWD}/keysandaddresses:/var/lib/keysandaddresses \
-p 3001:3001/tcp \
inputoutput/cardano-node:1.34.0 run \
   --topology /etc/cardano-node/testnet-topology.json \
   --database-path /var/lib/cardanodb \
   --socket-path /var/lib/cardanodb/node.socket \
   --host-addr 0.0.0.0\
   --port 3001 \
   --config /etc/cardano-node/testnet-config.json
```
