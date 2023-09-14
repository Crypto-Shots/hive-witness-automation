With this ansible scripts we are going to configure and install the someguy123 hive docker image on the ubuntu node

## Ansible
[Ansible](https://www.ansible.com/) playbooks to configure VMs.

## Prerequisites
- Ansible 2.14+ version installed in your workstation
- Node with Ubuntu 22.04 ssh access with ssh key
- Change the configuration of your host (ssh user and IP) on inventory/hivewitness/hosts

## Hive witness installation

### How to run ansible
With this ansible scripts we are going to configure and install the someguy123 hive docker image on the ubuntu node

- Please clone the github repo in your workstation.
- Enter the ansible directory
- If you want to change the default path for the witness (the default one is /opt/hive_witness/) you can do it by editing inventory/hivewitness/group_vars/all

Here you are the command that you need to run for the installation:
```
ansible-playbook --private-key <YOUR_SSH_KEY> -i inventory/hivewitness/hosts hivewitness.yml
```

### Configuration setup after the ansible running

Change the witness configuration here:
```
vi data/witness_node_data_dir/config.ini
```
Setup  witness name, private key, logging config, turn off p2p-endpoint etc. see the guide
https://peakd.com/hive-139531/@someguy123/how-to-set-up-a-hive-witness-or-seed-node-non-mira-upgrade-from-steem-docker-to-hive-docker

Generating a signing key
```
./run.sh remote_wallet

#Create a key pair for your witness.

suggest_brain_key

#Put the keys in Notepad or something similar for the moment so you don't lose them.

#Press CTRL-D to exit the wallet.
```

#### Start the node

```
./run.sh start
```
check the logs


#### Setup the wallet
```
./run.sh wallet
set_password "hunter2"
unlock "hunter2"
import_key 5somethingprivatekey
```

#### And finally update the witness
```
update_witness "YOURNAME" "https://hive.blog/witness-category/@YOURNAME/my-witness-thread" "STMxxxxxxx" {"account_creation_fee":"3.000 HIVE","maximum_block_size":65536,"sbd_interest_rate":0} true
```

you can check here
https://peakd.com/me/witnesses

You can refer to the someguy123 guide for the configuration details:
https://peakd.com/hive-139531/@someguy123/how-to-set-up-a-hive-witness-or-seed-node-non-mira-upgrade-from-steem-docker-to-hive-docker
