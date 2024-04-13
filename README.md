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

2. Install jenkins key:

    #sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

3. Install java: (This command is different for different os)

    #yum install java-17-amazon-corretto-devel

4. Install Jenkins

    #yum install jenkins -y


.
