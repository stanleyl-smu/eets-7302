# eets-7302

# Invoke playbook to dump running configuration to files in local directory:
ansible-playbook 01_get_config.yml -i netbox_inv.yml -vv -u admin -k

# Invoke playbook to update running configuration using Jinja2 template:
ansible-playbook 02_update_config.yml -i netbox_inv.yml -vvvv -u admin -k

# List netbox inventory:
ansible-inventory --list -i netbox_inv.yml -vvv

# Ansible modules installed:

ansible-galaxy collection list

Collection            Version
--------------------- -------
ansible.netcommon     5.2.0  
ansible.utils         2.11.0 
cisco.ios             5.0.0  
cisco.iosxr           6.0.1  
community.general     7.4.0  
juniper.device        1.0.2  
junipernetworks.junos 5.3.0  
netbox.netbox         3.14.0 

# Revert Junos router configuration with comment:
commit comment "Before applying ansible change"

# Revert IOS-XE router configuration with comment:
copy bootflash:pe2-before-applying-ansible.conf startup-config
copy bootflash:pe2-before-applying-ansible.conf running-config

copy bootflash:ce2-before-applying-ansible.conf startup-config
copy bootflash:ce2-before-applying-ansible.conf running-config

# commands used to install docker
sudo apt-get update && sudo apt-get install ca-certificates curl gnupg -y

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \

  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | 
  
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# commands used to pull and run netbox image on docker
git clone -b release https://github.com/netbox-community/netbox-docker.git

cd netbox-docker

tee docker-compose.override.yml <<EOF

version: '3.4'

services:

  netbox:
  
    ports:
    
      - 8000:8080
      
EOF

docker compose pull

docker compose up
