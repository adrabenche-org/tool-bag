# What 
Here you will find ansible scripts to deploy the following apps on a **standalone linux box** setting up **a new user named operator** on the cases where non-root users does not exists to run a cardano node with certain tools. With box we mean, depending on which cloud provider will use a different name (i.e Droplet, Instance, etc...)

## Apps

Each app is implemented into a separate container providing the ability to decide which app is installed and which not. Each app is attached to a role. You can find more information about how to setup each role inside [role folder](./roles).

- [x] Setup node: Setup basic stuff on the node.
- [x] Cardano node: Install the Cardano node.
    - [x] Support for Digital Ocean: By default we will use the Digital ocean droplets.
    - [ ] Support for AWS: Add the features to support deploy on AWS instances
- [x] Cardano cli: Install the cardano cli by pulling the docker image or building from this [github repo](https://github.com/adrabenche-org/yacc-builder.git)
- [ ] [Oura](https://github.com/txpipe/oura.git):  A implementation of a pipeline that connects to the tip of a Cardano node and submits Wto pluggable observers called "sinks".
- [ ] [Scrolls](https://github.com/txpipe/scrolls.git): A tool for building and maintaining read-optimized collections of Cardano's on-chain entities.

## Requirements

Before start

1) ssh access to the box, instance, droplet, etc you want to configure:
    * As root for **Digital Ocean**
    * As ubuntu fo **AWS**
2) ansible installed. Access [this link](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) for documentation.

## How to deploy

Access the directory matching the cloud and look for the `README.md` file:

* **do**: Digital Ocean
* **aws**: Amazon Web Services