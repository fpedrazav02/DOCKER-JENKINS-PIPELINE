# Docker-Jenkins-Pipeline

## Objective:
Demonstrate the continuous integration and delivery by building a Docker Jenkins Pipeline.

---
### Used Technology:
| **Name** |
| ----------- |
| Jenkins |
| GitHub |
|   a  |
|  b  |
---

## 1) Start the lab and log into Jenkins

First, we check services. If **Jenkins** is down, we start it. 

> Use **root** as needed

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
service jenkins start
```

#### Open Jenkins
