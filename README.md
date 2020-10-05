# copypaste


---
- hosts: 127.0.0.1
  connection: local
  become: true
  tasks:
  - name: Install NGINX
    apt:
      name: nginx
      state: latest
      update_cache: true
  - name: Start NGINX Service
    service:
      name: nginx
      state: started


[test]
IP_ADDRESS_1
IP_ADDRESS_2

[test:vars]
ansible_user=USER
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
ansible_ssh_private_key_file=~/.ssh/ansible_id_rsa
