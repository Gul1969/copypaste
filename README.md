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
