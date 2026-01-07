
# TrivyProject
Testing trivy with python test module 


1. create one EC2 with t2.small 
2. install the Docker with the below commands
# Update package index
sudo apt update

# Install prerequisites
sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add Docker repository
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

INstall docker engine

# Update package index
sudo apt update

# Install Docker Engine, containerd, and Docker Compose
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Add user to docker group (avoid sudo for docker commands)
sudo usermod -aG docker $USER
newgrp docker

# Verify installation
docker --version
docker compose version

3. install trivy by downloading teh deb file from teh below link as per the latest version 
https://github.com/aquasecurity/trivy/releases

I used this file trivy_0.67.0_Linux-64bit.deb
use the command sudo dpkg -i trivy_0.67.0_Linux-64bit.deb

trivy image flask-vuln-app to get report on console

trivy image -f json -o flask-report.json flask-vuln-app

trivy config .  -- for the docker configuration check

trivy fs . -- filesystem issues like API_KEY etc...

trivy image --severity CRITICAL,HIGH flask-vuln-app  for filtering the severity

To get the HTML files you need to follow the below steps 
1. mkdir -p contrib
2. wget https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/html.tpl -O contrib/html.tpl
3. trivy image --format template --template "@contrib/html.tpl" -o reports/flask-report.html flask-vuln-app
 

run the below command to get the HTML file under reports folder

trivy image --format template --template "@contrib/html.tpl" -o reports/flask-report.html flask-vuln-app
