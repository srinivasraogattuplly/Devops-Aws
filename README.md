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

-----------------------------------------------------------------------------------------------------------------------------
STEP 1 :  CREATE GITHUB WEBHOOK
Webhooks allow you to build or set up integrations which subscribe to certain events on GitHub.com public or private repositories.

Inorder to configure webhook you will need three things :

A github account with a public or a private repository
A Payload URL – In this case IP address and port to your Jenkins server.
Proper security group port listening to 0.0.0.0/0 or ip address range of github – As the notification from Github are sent to payload url whenever there are change in repository code.
Step-by-step instruction:

To get started login to your github account and select a particular repository
Next navigate to Settings tab where you will find Webhook option of left side bar
Click on Create webhook, fill in the appropriate details such as Payload URL which is basically the DNS of your jenkins server.
Select Content Type as shown in image below


Leave the Secret field empty as it not relevant for this task 
Select Just push event option for which you would like to configure events for and save it
Once this is done, now you need to ensure that the push event notifications are delievered to Jenkins URL (Payload URL) successfully. You can test this by selecting the webhook we just created.

Scrolling down the webhook configuration you will find section named Recent Deliveries, this section will show all the recent payload which were triggered on a push event. 

If you see a green tick mark against the payload then the communication is successfull, if you get red icon then the github.com was unable to reach payload URL.

To troubleshoot this issue ensure your security ports are open especially port 8080 and the ip address is correct in payload url field.


At this step you’ve already configured 75% of things, other 25% things include creating a jenkins job and testing it.

 

STEP 2 : CONFIGURE JENKINS JOB TO BUILD ON PUSH EVENTS
Here you’ll configure a normal jenkins job which builds whenever webhook push event triggers are recieved.

You’ll need a git plugin installed on jenkins to configure this job.

Create a new job :



In SCM, select Git followed by the repository url and credentails. you can also specify a branch if you would want to build a specific version and not the master branch.



Your last step will be select GitHub hook trigger for GITScm polling option, this means that this job will be build whever it recieves a webhook trigger.



Further in other sections you can make changes in configuration as per your environment. Once all of this is done now your ready to test if the job is build via webhook trigger.

TESTING :
To test this fuctionality you need to do following tasks :

Push a new code to repository which will generate a push event webhook tirgger
Once the push event is done, switch to jenkins console and check if it triggered the build or not.
If it triggered then the job the you’ve succeeded in your mission, if it did not tirgger build then switch to github, go to webhook setting and check whether the webhook status shows green tick or not.


If it shows red sign than there is an issue as the github is not able to communicate with jenkins server. Ensure you’ve security groups ports open, make sure your payload url of webhook is correct (try to switch it to server ip address if domain name does not work).

This way you can Run Jenkins Job on Git Push Event Automatically, you can enhance the your job to send email on every failure which will give you automatic notifications about every build status. This surely will help developers to worry less about build and deployment.

sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo

sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key

sudo yum install jenkins

sudo service jenkins start

sudo chkconfig --add jenkins

That’s it! Now you can go to URL http://<instance ip>:8080

If you’re unable to see the Jenkins page, check security groups restrictions. You can also change the port for Jenkins manually if you want to run it on a different port.

Step 5. Setup Jenkins

This is the first screen you will after going to http://<instance ip>:8080

