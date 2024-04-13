# Jenkins

Following are the ways of connect to jenkins:

1. Web GUI 
2. CLI
3. API

Install and steup of jenkins bye Web GUI:
 
For this i use AWS Cloud EC2 instance amazon linux ami, In this instance i install jenkins.

Note:

For install jenkins need yum repository and key & Jenkins is made from Java , so jenkins work on java .
(Link:  https://pkg.jenkins.io/redhat-stable/ )

On Aws EC2 instance where install jenkins:

1. Install yum repo:
 

       #sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

3. Install jenkins key:


       #sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

4. Install java: (This command is different for different os)


       #yum install java-17-amazon-corretto-devel

5. Install Jenkins


       #yum install jenkins -y

6. Start Jenkins service:


       #systemctl start jenkins

Now Jenkins is installed successfully, connet jenkins by webUI:

For this we use EC2 instance public IP and Jenkins work on port no. 8080,

On Browser:--  " http://Public_IP : 8080 "

Note: 

  AWS EC2 have Firewall , for connect to EC2 we need allow security Group:

   In security group >> edit inbound rule >> "Custom TCP  8080  myIP "
