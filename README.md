docker network create sonarqube-tutorial
docker run -d -p 9000:9000 --name sonarqube --network sonarqube-tutorial sonarqube
docker run -d -p 8080:8080 -- name jenkins --network sonarqube-tutorial jenkins/jenkins


# must be unique in a given SonarQube instance
sonar.projectKey=first-project

# --- optional properties ---

# defaults to project key
#sonar.projectName=My project
# defaults to 'not provided'
#sonar.projectVersion=1.0

# Path is relative to the sonar-project.properties file. Defaults to.
#sonar.sources=.

# Encoding of the source code. Default is default system encoding
#sonar.sourceEncoding=UTF-8
