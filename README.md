sqp_40c3edf2d96b59b7f61fc7b7cee2075e2684e73d

![Blank diagram](https://github.com/user-attachments/assets/56b90bb2-4a5c-433e-b9ed-3e70952d0300)
Prerequisite tools for creating the Jenkins project
•	Linux machine
•	Maven
•	Git Hub
•	Jenkins
•	Docker

Step-1: Jenkins Server Setup in Linux VM
1.	Create Ubuntu VM using AWS EC2 (t2.medium)
2.	**Enable 8080** Port Number in Security Group Inbound Rules TCP
3.	Connect to VM using git bash
4.	Install Java
           Good practice Update the machine
                -> sudo apt-get update
  	       Install the java now
                -> sudo apt-get install openjdk-17-jre      or   sudo yum install openjdk-17-jre 

6.	Install Jenkins
           * Jenkins to be installed

  	    sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \ https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \ https://pkg.jenkins.io/debian-stable binary/ | sudo tee \ /etc/apt/sources.list.d/jenkins.list > /dev/null

               sudo apt-get update
               sudo apt-get install jenkins 

            * start Jenkins
                 sudo systemctl enable jenkins
                 sudo systemctl start jenkins

             * verify Jenkins
                  sudo systemctl status jenkins
  	
  	         * access Jenkins server in browser using VM public ip 
                 http://public-ip:8080/
                 http://15.206.209.14:8080/

  	         * copy Jenkins admin pwd, Create Admin Account & Install Required Plugins in Jenkins
                  **sudo more /var/lib/jenkins/secrets/initialAdminPassword** or **sudo cat /var/lib/jenkins/secrets/initialAdminPassword**
                  password: 618d55d61e0840e2b113cd953d6916eb
  	
8. Create Admin Account & Install Required Plugins in Jenkins
**Note: **I have created this job using the pipeline option.  not the freestyle. The freestyle-only beginner will also use very simple project. we can go with freestyle**

 <b> ** There are Two ways to create or write the pipeline.
          1, Declarative approach 2, Scripted approach****</br>

**Interview notes: To identify the script -> starting with pipeline is called the Declarative approach and the script starting with None is called the Scripted approach.**
    **
I am doing this job with a Declarative approach **

<be>**again** **because this is very important** 
**Interview notes: To identify the script -> starting with pipeline is called the Declarative approach and the script starting with None is called the Scripted approach.**
    **
I am doing this job with a Declarative approach **</br>

**Four stages required to create the Jenkins pipeline**
![Blank board](https://github.com/user-attachments/assets/5e501a69-39ae-42a8-a297-ab56a851ac0a)
   **<ul>stage-1: Get the code from the Git Hub
     stage-2: Have to do the maven Build
     stage-3: Build a docker image
     stage-4: create the docker container</ul>
**
pipeline {
    agent any
    
    tools{
        maven 'M3'
    }
    stages {
        stage('Git Clone') {
            steps {
                git 'https://github.com/ashokitschool/maven-web-app'
            }
        }
        stage('MVN Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Image') {
            steps {
                sh 'docker build -t santhosh .'
            }
        }
        stage('Deployment') {
            steps {
                sh 'docker run -d -p 9090:8080 --name santhuc santhosh'
            }
        }
    }
}



Step 2: Configure Maven as a Global Tool in Jenkins
**Manage Jenkins -> Tools -> Maven Installation -> Add maven**

Step-3: Setup Docker in Jenkins
**curl -fsSL get.docker.com | /bin/bash
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu
sudo systemctl restart jenkins
sudo docker version**

To list the docker image -> docket images
To list the docker container -> docket ps -a

Step 4: Create a Jenkins Job

Step - 5: Trigger Jenkins Job

Step 6: Enable host port in security group inbound rules

Step - 7: Access Application in Browser
![Jenkins pipeline ](https://github.com/user-attachments/assets/43f04981-b7c1-44bc-bd80-17fd9f39feee)


![output](https://github.com/user-attachments/assets/b528175e-73eb-46f6-b99b-fcd4eb955c66)


Step 8: After your practice, delete resources we have used in AWS Cloud to avoid billing

J.peEhrdQqZh9%bQ.ea2jtvvpU5$@F?z
