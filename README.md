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
 

       #  sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

3. Install jenkins key:


       #  sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

4. Install java: (This command is different for different os)


       #  yum install java-17-amazon-corretto-devel

5. Install Jenkins


       #  yum install jenkins -y

6. Start Jenkins service:


       #  systemctl start jenkins

Now Jenkins is installed successfully, connet jenkins by webUI:

For this we use EC2 instance public IP and Jenkins work on port no. 8080,

On Browser:--  " http://Public_IP : 8080 "

Note: 

  AWS EC2 have Firewall , for connect to EC2 we need allow security Group:

   In security group >> edit inbound rule >> "Custom TCP  8080  myIP "

![Screenshot 2024-04-13 150813](https://github.com/Pratikshinde55/Jenkins/assets/145910708/05ad7d9f-e63e-49cf-95bb-448dfb4a1916)

Now Jenkins InterFace occur:

![Screenshot 2024-04-13 151042](https://github.com/Pratikshinde55/Jenkins/assets/145910708/1e827615-2005-46ef-8390-427624c5bb78)

For Login jenkins Password is neccessary & Jenkins kept password at location "/var/lib/jenkins/secrets/initialAdminPassword" , Go Jenkins OS  and view password 


    #cat /var/lib/jenkins/secrets/initialAdminPassword

Copy password and paste on WebUI , now Select 'Install suggested plugins' Plugins start downloading:

![Screenshot 2024-04-13 151514](https://github.com/Pratikshinde55/Jenkins/assets/145910708/42353e64-69da-493d-9816-85153ec7e479)


Create First Admin User Username Interface appers: Fill info and start jenkins:

![Screenshot 2024-04-13 152143](https://github.com/Pratikshinde55/Jenkins/assets/145910708/6765f294-f394-4223-8881-4755699dc96d)



# ❄️ProJecT:

About Infrasturcture:

Developer create code and upload code on SCM GitHub , that code(webpage) will deploy webserver and this webserver can access by Client from google.

By Using jenkins i do this set-up automatic:

❄️Step-1:

I use Git Bash on local laptop for create code as developer. This code is push to gitHub.

Here i use Hooks which make automation that is whenever i change code and commit that code it automatically update on GitHub.

      $ cd documents
      $ mkdir jenkins-2024
      $ cd jenkins-2024
      $ mkdir myproject
      $ cd myproject
      $ git init myproject
      $ notepad index.html
      $ git add index.html
      $ git commit index.html -m "mychange"


Now, we create empty repo on GitHub for push local code . Don't use README file.

On GitHub there commands give for push code locally.

      $ git remote add origin https://-----------
      $ git branch -M main
      $ git push -u origin main

Now 1st time we push then need login we use command for login

      $ git config --global user.email "____" <<--  email GitHub
      $  git config --global user.name "______" <<--   password GitHub

....
Now Developer set-up done :

Note:--

  Pushing code is manual but we make this automatic by using Git "Hook" , In Hooks folder create new post-commit file for automation.
  as soon we commit the new code that code automatically push to GitHub this done by post-commit Hooks. (Below screenshot refer)

![Screenshot 2024-04-13 174200](https://github.com/Pratikshinde55/Jenkins/assets/145910708/c41d2ed1-3aec-4dfd-b86a-a187ec5001b6)

Now code change & need to only commit that code file:

   $ git commit index.html -m "hooksactivate"

 ![Screenshot 2024-04-13 174650](https://github.com/Pratikshinde55/Jenkins/assets/145910708/3dd4d2ef-485e-401c-9eac-f5c6b8621580)

Note:-

Whenever i change code and commit this code automatically updated on GitHub.


❄️Step-2:  (On Jenkins)

Now on jenkins i created two Jobs 
- 1st job (gitHubjob1) that pull code from gitHub and deploy that Code on webserver location /var/www/html .
- 2nd job (webserver) that create websever setup by using jenkins.


1st create webserver job :

   on GitHub create new job named as webserver using freestyle & in Build step put below screenshot steps.

![Screenshot 2024-04-13 175659](https://github.com/Pratikshinde55/Jenkins/assets/145910708/423f0348-6220-4f4a-9e7f-93612c46e603)





    





