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



# run on all hosts
- hosts: all
  # run as the root user on the remote machine
  become: true
  # declare some variables that can be used throughout the playbook
  vars:
  - install_directory: /opt/static-website-example
  # list of tasks to run on the remote machine
  tasks:
  - name: 'download and install git & nginx using apt'
    apt:
      pkg:
      - nginx
      - git
      state: latest
      # run an apt update before installing the packages
      update_cache: true
  - name: 'make sure that the nginx service is started'
    service:
      name: nginx
      state: started
  - name: 'update website from the git repository'
    git:
      repo: 'https://gitlab.com/qacdevops/static-website-example'
      # use the variable defined at the top of the play for the install directory
      dest: "{{ install_directory }}"
  - name: 'install the nginx.conf file on to the remote machine'
    template:
      src: ./nginx.conf
      dest: /etc/nginx/nginx.conf
    # register a variable for this templated file, we can check attributes of this in later steps
    register: nginx_config
  - name: 'reload nginx'
    service:
      name: nginx
      state: reloaded
    # only run this task if the /etc/nginx/nginx.conf file on the remote machine changed
    when: nginx_config.changed


