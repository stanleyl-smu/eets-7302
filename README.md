# eets-7302

# Invoke playbook:

ansible-playbook 01_get_config.yml -i netbox_inv.yml -vv -u admin -k

# Ansible modules installed:

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
