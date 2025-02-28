
# PRODUCTION GRADE DEVSECOPS CICD Pipeline

## Prereq: Create 3 EC2 servers
- [ ] Build server with 15GB storage - t2.mirco
- [ ] Sonarqube server with 4 GB memory - t2.medium
- [ ] Jenkins Server (master)
###  Jenkins Server
- install jenkins on Master
## Step 1: Ensure all the necessary plugins are installed in Jenkins Master
- [ ] Parameterized trigger plugin
- [ ] Github plugin
- [ ] Docker Pipeline
- [ ] Pipeline: AWS steps
- [ ] SonarQube Scanner
- [ ] Quality Gates
- [ ] AWS Credentials
- [ ] kubernetes
- [ ] Amazon ECR
## On the build Server

## Step 2: Install Docker, Java8, Java11 & Trivy on Build Server
        ## Make the file executable
        $ chmod +x setup.sh 

        ```
        $ sudo ./setup.sh
        ```
        or 
        ...........
                # Ensure script is run with root privileges
                if [ "$EUID" -ne 0 ]; then
                echo "Please run this script as root or sudo privileges "
                exit 1
                fi


                # Install Java 8, Java 11 & Docker
                apt update
                apt install -y openjdk-8-jdk openjdk-11-jdk docker.io maven
                usermod -a -G docker ubuntu

                # Install Trivy
                wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
                echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
                apt update
                apt install -y trivy
                .......

## Step 3: Install Sonrqube on the t2.medium server
```
$ sudo apt update
$ sudo apt install -y docker.io
$ sudo usermod -a -G docker ubuntu
$ sudo docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```

## Step 4: Add necessary credentials
- [ ] Generate Sonarqube token of type "global analysis token" and add it as Jenkins credential of type "secret text"
- [ ] Add dockerhub credentials as username/password type
- [ ] Add AWS credentials if you want to used ECR
- [ ] Add Gitlab credentials 
- [ ] Add Build server credentials for Jenkins master to connect
- [ ] Check if the buid server is successfully connected 
## use the latest java version for the build server
    sudo apt update
    sudo apt install openjdk-17-jdk -y
    Restart the server.


## Step 5: Enable Sonarqube webhook for Quality Gates & Install dependency-check plugin
- [ ] Generate webhook & add the Jenkins URL as follows - http://URL:8080/sonarqube-webhook/
- [ ] Add Dependency-CheckIntegration from the marketplace in sonarqube



