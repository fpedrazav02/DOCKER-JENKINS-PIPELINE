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

