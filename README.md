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

# Tomcat Server

### Installing Tomcat:

Same process as maven: 

In /opt dir: `wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.62/bin/apache-tomcat-9.0.62.tar.gz`

Extract in the same way as before. 

Install java: `amazon-linux-extras install java-openjdk11 -y`

Navigate to /opt/tomcat/bin and run the startup.sh script. Once server is launched, go to the manager app on port 8080. 

First, we need to update the context.xml file. To find this file, use `find / -name context.xml` and update the host-manager and manager files. In host-manager and manager.xml files, comment out the 'allow=127' by adding `<!--` at the start and `-->` at the end. This is how we comment things out in .xml files. I.e:

```
<!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
```

Navigate to /opt/tomcat/bin and run the shutdown.sh script to stop the tomcat service. Restart using startup.sh 

- We can create a link for an executable so that we don't have to specify the entire path every time. I.e, where we have to navigate to `/opt/tomcat/bin/startup.sh` to start tomcat, we can create a an executable in the `/usr/local/bin` dir called tomcatup. This will allow us to execute the startup.sh script by only using the tomcatup command and not having to specify the entire path. This is because the `/usr/local/bin` dir is already specified in the $PATH environment variable, and we are creating a link between the `/opt/tomcat/bin/startup.sh` and `/usr/local/bin/tomcatup`, meaning 'tomcatup' is linked to the path of the startup.sh script. 

The following commands are creating links for the startup and shutdown scripts: 
`
ln -s /opt/tomcat/bin/shutdown.sh /usr/local/bin/tomcatdown
ln -s /opt/tomcat/bin/startup.sh /usr/local/bin/tomcatup
`
