# How to use this repo ? #

## Prerequisites to use this repo ##

- Ansible >= 2.9

## Steps to deploy a PacketFence server ##

### Installing prerequisites on your Ansible controller ###

```bash
apt install python-pip git
git clone URL_OF_THIS_REPO
cd ansible-playbook-inverse-deployment/products/packetfence
pip install --user ansible
# update your PATH to have ~/.local/bin in it
ansible-galaxy role install -r requirements.yml
ansible-galaxy collection install -r requirements.yml
```

### Set up your inventory ###

- Define your inventory location
- Copy [example inventory](inventory) to your inventory location 
- Edit example inventory to fit your needs
  - Generate four passwords for Vault: `apg -m 22 -n 4`
  - Encrypt Vault

### Run playbooks ###

```bash
ansible pf1 -m ping -i YOUR_INVENTORY_LOCATION --vault-id @prompt

ansible-playbook site.yml -i YOUR_INVENTORY_LOCATION --tags time,network,install,postconfig --vault-id @prompt

ansible pf1 -m reboot -i YOUR_INVENTORY_LOCATION --vault-id @prompt

ansible-playbook site.yml -i YOUR_INVENTORY_LOCATION --tags maintenance --vault-id @prompt
ansible-playbook site.yml -i YOUR_INVENTORY_LOCATION --tags maintenance --skip-tags monit --vault-id @prompt
```
