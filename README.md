# Devops-Aws
Devops tools on Aws

 Step 1.  Launch an instance (Amazon Linux) 

Step 2.  Login to the instance, install and setup java environment 

sudo yum install -y git  java-1.8.0-openjdk-devel aws-cli

sudo alternatives --config java

In this command change version of java to the latest version.

Step 3. Install Apache Maven 

sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo

sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo

sudo yum install -y apache-maven

mvn –v

Step 4.  Install Jenkins 

sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo

sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key

sudo yum install jenkins

sudo service jenkins start

sudo chkconfig --add jenkins

That’s it! Now you can go to URL http://<instance ip>:8080

If you’re unable to see the Jenkins page, check security groups restrictions. You can also change the port for Jenkins manually if you want to run it on a different port.

Step 5. Setup Jenkins

This is the first screen you will after going to http://<instance ip>:8080

