# Docker-Jenkins-Pipeline

## Objective:
Demonstrate the continuous integration and delivery by building a Docker Jenkins Pipeline.

---
### Used Technology:
| **Name** | 
| ----------- 
| [Jenkins](https://www.jenkins.io/) |
| [GitHub](https://github.com/) |
|   a  | 
|  b  |
---

## 1) Start the lab and log into Jenkins

First, we check services. If **Jenkins** is down, we start it. 

> Use **root** as needed and give permisions to **jenkins** to execute **docker** commands.

```bash
chmod 777 /var/run/docker.sock

```

#### Check Jenkins
---
```sh
service --status-all
```
![alt text](../imgs/jenkinsdown.png)

As we can see, **Jenkins** is down. We need to start the service and see where is running. 

---
#### Start Jenkins

We can inicialize it with the *service* cmd utility.

```sh
service jenkins start
```
#### Check Jenkins Service Status

Next we can explore its basic running status.

```sh
service jenkins status
```
![alt text](../imgs/jenkinsup.png)

> We can then access it locally on port **8080**
#### Open Jenkins in the browser
![alt text](../imgs/jenkinsupportal.png)
---

## 2) Create the pipeline

> Since we want to create a Pipeline that both has ***CI*** and ***CD*** integrations we need to install configuration tools needed.

- In this case we will ***Maven*** as the build tool with a repo own by ***Sonal0409***

---

We enter Jenkins Dashboard directly to Manage Jenkins and Global Tool Configuration

- ***Dashboard*** > ***Global Tool Configuration***

Scroll down to ***Maven*** and install it.
![alt text](../imgs/maveninstall.png)

---
### Create Job

Since we need a ***CI***/***CD*** project we will choose the pipeline option.

![alt text](../imgs/pipeline.png)

Since we have some requisites, we will go with a jenkins script, located on ***/src/jenkinsfile*** on the project folder.

```
pipeline {

	tools{

	}
	agent any

	stages {
	}
	
}
```
We will also be using the simple ***dockerfile*** in the GitHub repository.
```docker
FROM tomcat:9
ADD addressbook.war /usr/local/tomcat/webapps
CMD ["catalina.sh", "run"]
EXPOSE 8080
```

Since we need to complete these next requirements: 
- Create a Docker Jenkins Pipeline that will create a Docker image from the Dockerfile and host it on Docker Hub

- It should also pull the Docker image and run it as a Docker container

- Build the Docker Jenkins Pipeline to demonstrate the continuous integration and continuous delivery workflow

We will add some stages in our Jenkins Pipeline script

```
			stage('Clone Github repository')
			{
				steps{
				    echo 'Cloning repository...'
                    git 'https://github.com/Sonal0409/DevOpsClassCodes.git'
				}
			}
			stage('Build Project'){
				steps{
                    echo 'Building the project'
                    sh 'mvn package'
				}
			}
            stage('Build image'){
				steps{
                    echo 'Copying artifact to workspace'
                    sh 'cp /var/lib/jenkins/workspace/project-pipeline/target/addressbook.war .'
                    echo 'Building image from docker file'
                    sh 'docker build -t addressbook:$BUILD_NUMBER .'
				}
			}
			
			stage('Push image to DockerHub'){
            steps{
 
                sh 'docker login -u "fpedrazav02" -p "" docker.io'
			
                sh 'docker tag addressbook:$BUILD_NUMBER fpedrazav02/myaddressbook'
                sh 'docker push fpedrazav02/myaddressbook'
                sh 'docker rmi fpedrazav02/myaddressbook'
            }
        }

            stage('Deploy container'){
				steps{
                    echo 'Deploying container'
                    sh 'docker run -d -P fpedrazav02/myaddressbook'
				}
			}
	}
```

We aim for an image with a build Jenkins build number. This image is then tagged as our final image name, which we will then deploy to Docker Hub.

Finally, we can check if this works deploying the container. 

## 3) Run the Pipeline

We first check we have nothing running.

```
docker ps -a
```

![alt text](../imgs/nocontainerup.png)

We then build the JOB

![alt text](../imgs/jenkinsbuild.png)


If everythin has compiled correctly, we can see our image running with an open port.

![alt text](../imgs/containerup.png)

We can also access it via our localhost on the port mentioned.

>**http://127.0.0.1:49159/addressbook**

![alt text](../imgs/appup.png)

The app is working as expected.