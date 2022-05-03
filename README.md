## DevOps Project for Beginners   

[![Image](https://github.com/yankils/Simple-DevOps-Project/blob/master/Devops_course.PNG "DevOps Project - CI/CD with Jenkins Ansible Docker Kubernetes ")](https://www.udemy.com/course/valaxy-devops/?referralCode=8147A5CF4C8C7D9E253F)


## Install Jenkins
https://pkg.jenkins.io/redhat-stable/

- Install Git: `yum install git`

- Add Github plugin to Jenkins

- Configure Github plugin to use `git` path executable. If this doesn't work, run the `whereis git` command and use that path instead. 


## Integrate Maven with Jenkins

### Setup Maven on Jenkins Server
To install Maven, navigate to the Maven website and locate the download folder:
https://maven.apache.org/download.cgi

Copy the link address of the file we want - in this case, its the tar.gz link for linux. 

On our server, navigate to /opt dir and enter `wget <link>`: `wget https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz`

To extract this folder, run `tar -xvzf <package-name>`

- Setup env vars

- Install maven plugin

- Configure maven and java
- 
