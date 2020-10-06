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

- hosts: test
  tasks:
  - name: "Ping"
    ping:
    
    
    events {}
http {
    server {
        root {{install_directory}};
        index index.html;
        include /etc/nginx/mime.types; 
        proxy_read_timeout  90;
        proxy_set_header X-Forwarded-Host $host:$server_port;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;

        location / {
            try_files $uri /index.html;
        }
    }
}
