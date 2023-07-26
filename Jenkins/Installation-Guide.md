## JENKINS INSTALLATION
## Prerequisites
### 1. Install Java of Version 17
   ```
   sudo apt update
   sudo apt install openjdk-17-jre
   java -version
   ```
## Install Jenkins On Debian Based Linux Operating System
   ```
   curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
   https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
   sudo apt-get update
   sudo apt-get install jenkins
   ```
## Start Jenkins
Enable the Jenkins service to start at boot with the command
```
sudo systemctl enable jenkins
```
Start the Jenkins service with the command
```
sudo systemctl start jenkins
```
Check the status of the Jenkins service using the command:
```
sudo systemctl status jenkins
```
