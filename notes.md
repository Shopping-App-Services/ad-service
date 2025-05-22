mkdir -p /home/jenkins/.gradle/wrapper/dists
chown -R jenkins:jenkins /home/jenkins/.gradle

When Sonarqube unable to create cache

sudo mkdir -p /home/jenkins/.sonar/cache
sudo chown -R jenkins:jenkins /home/jenkins/.sonar

sudo mkdir -p /home/jenkins/go
sudo chown -R jenkins:jenkins /home/jenkins/go