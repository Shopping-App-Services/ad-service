sudo mkdir -p /var/lib/jenkins/.gradle/wrapper/dists
sudo chown -R jenkins:jenkins /var/lib/jenkins/.gradle

When Sonarqube unable to create cache

sudo mkdir -p /var/lib/jenkins/.sonar/cache
sudo chown -R jenkins:jenkins /var/lib/jenkins/.sonar

sudo mkdir -p /var/lib/jenkins/go
sudo chown -R jenkins:jenkins /var/lib/jenkins/go


Nodejs
sudo chown -R jenkins:jenkins /var/lib/jenkins/workspace/payment-service-ci/node_modules/pprof
 sudo apt-get install -y build-essential
