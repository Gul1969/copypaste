# SAST Testing

docker network create sonarqube-tutorial
sudo docker run -d -p 9000:9000 --name sonarqube --network sonarqube-tutorial sonarqube
sudo docker run -d -p 8080:8080 -- name jenkins --network sonarqube-tutorial jenkins/jenkins

must be unique in a given SonarQube instance

sonar.projectKey=first-project

--- optional properties ---

 defaults to project key
sonar.projectName=My project
 defaults to 'not provided'
sonar.projectVersion=1.0

 Path is relative to the sonar-project.properties file. Defaults to.
sonar.sources=.

 Encoding of the source code. Default is default system encoding
sonar.sourceEncoding=UTF-8

sonar-scanner \
  -Dsonar.projectKey=first-project \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=2b015a98b7b5898c48974457a9e1f88027a4f232




https://gitlab.com/qacdevops/flask-stages/-/blob/master/sonar-project.properties


sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose


git clone https://gitlab.com/qacdevops/chaperootodo_client chaperoo && cd $_

export DB_PASSWORD=[enter your own password here]

sudo docker-compose pull && sudo docker-compose up -d

sudo docker run -d --name zap -u zap -p 8080:8080 -p 8090:8090 -i owasp/zap2docker-stable zap-webswing.sh



# Jenkins Install

#!/bin/bash
if type apt > /dev/null; then
    pkg_mgr=apt
    java="openjdk-8-jre"
elif type yum /dev/null; then
    pkg_mgr=yum
    java="java"
fi
echo "updating and installing dependencies"
sudo ${pkg_mgr} update
sudo ${pkg_mgr} install -y ${java} wget git > /dev/null
echo "configuring jenkins user"
sudo useradd -m -s /bin/bash jenkins
echo "downloading latest jenkins WAR"
sudo su - jenkins -c "curl -L https://updates.jenkins-ci.org/latest/jenkins.war --output jenkins.war"
echo "setting up jenkins service"
sudo tee /etc/systemd/system/jenkins.service << EOF > /dev/null
[Unit]
Description=Jenkins Server

[Service]
User=jenkins
WorkingDirectory=/home/jenkins
ExecStart=/usr/bin/java -jar /home/jenkins/jenkins.war

[Install]
WantedBy=multi-user.target
EOF
sudo systemctl daemon-reload
sudo systemctl enable jenkins
sudo systemctl restart jenkins
sudo su - jenkins << EOF
until [ -f .jenkins/secrets/initialAdminPassword ]; do
    sleep 1
    echo "waiting for initial admin password"
done
until [[ -n "\$(cat  .jenkins/secrets/initialAdminPassword)" ]]; do
    sleep 1
    echo "waiting for initial admin password"
done
echo "initial admin password: \$(cat .jenkins/secrets/initialAdminPassword)"
EOF

# or:

Git clone https://github.com/bob-crutchley/installers.git

# Use ansible to install Docker

- hosts: 127.0.0.1
  connection: local
  become: true
  vars:
    ansible_python_interpreter: "/usr/bin/env python3"

  tasks:
  - name: "APT - Add Docker GPG key"
    apt_key:
      url: https://download.docker.com/linux/ubuntu/gpg
      state: present

  - name: "APT - Add Docker repository"
    apt_repository:
      repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
      state: present
      filename: docker

  - name: "APT - install misc packages"
    apt:
      name: "{{ item }}"
      update_cache: yes
    with_items:
      - "aptitude"
      - "apt-transport-https"
      - "ca-certificates"
      - "curl"
      - "software-properties-common"

  - name: "APT - install 'docker-ce'"
    apt:
      name: "docker-ce"
      update_cache: yes


# Install docker on VM

curl https://get.docker.com | sudo bash

sudo usermod -aG docker $(whoami)

