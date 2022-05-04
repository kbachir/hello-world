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

On our server, navigate to `/opt` dir and enter `wget <link>`: `wget https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz`

To extract this folder, run `tar -xvzf <package-name>`
ls

### Setup env vars

`cd`

`nano .bash_profile` to create an env var that only affects root user

Add the following env vars for maven and java: 

```
M2_HOME=/opt/maven
M2=/opt/maven/bin
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.13.0.8-1.amzn2.0.3.x86_64
```
** to find the java path, use `find / -name jvm` (or java-11*)

Then update the PATH line to load these values: `PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2`

We can now run `mvn -v` and execute the command outside of the /opt/maven/bin dir. 

### Install maven plugin on Jenkins and configure paths

- Install maven plugin - this will auto install jdk plugin as dependency also
- In configuration, untick "install automatically" as we've already installed these, and add the paths in the .bash_profile
- For maven, use /opt/maven without /bin

### Configure maven and java
- For the first maven job, use a `clean install` goal, which will run all previous goals without specifying them.
- For more on maven build lifecycle: https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html


