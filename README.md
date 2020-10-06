
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
      
      
mkdir -p ~/projects/ansible-roles-tutorial && cd $_
mkdir -p roles/{common/tasks,webserver/{tasks,templates}}
touch playbook.yaml roles/{common/tasks/main.yaml,webserver/{tasks/main.yaml,templates/nginx.conf}}

- name: 'zsh installed'
  apt:
    name: zsh
    state: latest
    update_cache: yes
- name: 'developer group'
  group:
    name: developer
    state: present
- name: 'bill user'
  user:
    name: bill
    comment: Developer Bill
    shell: /bin/zsh
    groups: developer
    append: yes
- name: 'jenkins user'
  user:
    name: jenkins
    comment: Jenkins Automation User
    shell: /bin/bash
    
    
    - name: 'download and install git & nginx using apt'
  apt:
    pkg:
    - nginx
    - git
    state: latest
    update_cache: true
- name: 'make sure that the nginx service is started'
  service:
    name: nginx
    state: started
- name: 'update website from the git repository'
  git:
    repo: "{{ git_repository }}"
    dest: "{{ install_directory }}"
- name: 'install the nginx.conf file on to the remote machine'
  template:
    src: nginx.conf
    dest: /etc/nginx/nginx.conf
  register: nginx_config
- name: 'reload nginx'
  service:
    name: nginx
    state: reloaded
  when: nginx_config.changed
  
  
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


- hosts: all
  become: yes
  roles:
  - common
  - role: webserver
    vars:
      install_directory: /opt/static-website-example
      git_repository: https://gitlab.com/qacdevops/static-website-example
      
      
      
      ansible-playbook -i '127.0.0.1,' playbook.yaml


