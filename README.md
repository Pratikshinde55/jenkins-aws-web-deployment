# Automated Web Deployment Pipeline with Jenkins on AWS 

- Set of jenkins on the AWS Cloud use this link to configure Set-up- [Jenkins-SetUp-onAWS](https://github.com/Pratikshinde55/Jenkins-Setup-onAWS.git)

WorkFlow Structure:

![hgjhgjhgyjhchjchjcv (1)](https://github.com/Pratikshinde55/jenkins-aws-web-deployment/assets/145910708/bea20297-b207-4658-a93c-c45d828ed175)

Streamlining web development workflows by automating code deployment from GitHub to an Apache web server using Jenkins on AWS,
ensuring seamless updates without manual intervention.

 - About Infrasturcture of this project(use case):

Developer create code and upload code on SCM GitHub , that code(webpage) will deploy webserver and this webserver can access by Client from google.

By Using jenkins i do this set-up automatic:

- Use following steps for do above set-up automatic by using 'Jenkins'

### Step-1: [Push Code from local to SCM GitHub]
I use Git Bash on local laptop for create code as developer. This code is push to gitHub.

- Hooks: **Here i use Hooks which make automation that is whenever i change code and commit that code it automatically update on GitHub.**

Create workspace/working area:

     cd documents
     mkdir jenkins-2024
     cd jenkins-2024
     mkdir myproject
     cd myproject
      
Initialize Git repo command:
     
     git init myproject
     
Create Webpage:
      
     notepad index.html
     
Addeds to tracking/stagging area of git:
     
     git add index.html

Commit the file/webpage:
 
     git commit index.html -m "mychange"

- Now, we create empty repo on GitHub for push local code . NOTE: Don't use README file.

On GitHub there commands give for push code locally.

     git remote add origin https://-----------
     git branch -M main
     git push -u origin main

Now 1st time we push then need login we use command for login:

Command for login to the GitHub from Local:

     git config --global user.email "____" <<--  email GitHub
     git config --global user.name "______" <<--   password GitHub

Now, Developer set-up done ( push local code to GitHub SCM ):

- Note:

Pushing code is manual but we make this automatic by using Git "Hook" , In Hooks folder create new post-commit file for automation.
as soon we commit the new code that code automatically push to GitHub this done by post-commit Hooks. (Below screenshot refer)

![Screenshot 2024-04-13 174200](https://github.com/Pratikshinde55/Jenkins/assets/145910708/c41d2ed1-3aec-4dfd-b86a-a187ec5001b6)

Now code change & need to only commit that code file ( Fully Automatic way to push code):
    
    git commit index.html -m "hooksactivate"

![Screenshot 2024-04-13 174650](https://github.com/Pratikshinde55/Jenkins/assets/145910708/3dd4d2ef-485e-401c-9eac-f5c6b8621580)

 - Note:- Whenever i change code and commit this code automatically updated on GitHub.

### Step-2: [On Jenkins webserver job]
Now on jenkins i created two Jobs 
- 1st job (webserver) that create websever setup by using jenkins.
- 2nd job (gitHubjob1) that pull code from gitHub and deploy that Code on webserver location /var/www/html .


#### 1st create webserver job :
on GitHub create new job named as webserver using freestyle & in Build step put below screenshot steps.

![Screenshot 2024-04-13 175659](https://github.com/Pratikshinde55/Jenkins/assets/145910708/423f0348-6220-4f4a-9e7f-93612c46e603)

- Note: 

**For this we need jenkins have root level or admin level power so we give power to jenkins then build webserver job, for this we go to Ec2 instance where jenkins 
installed or run and give ALL power.**
     
     vim /etc/sudoers

![Screenshot 2024-04-13 180236](https://github.com/Pratikshinde55/Jenkins/assets/145910708/3352d74f-0fde-4aa8-9990-95256bd4cbef)

Now, Build our webserver job, this jenkins job download Https webserver and start Httpd service. 

![Screenshot 2024-04-13 180534](https://github.com/Pratikshinde55/Jenkins/assets/145910708/6e9486b3-b0a2-4cfe-b6a7-34e7ac2ee9e0)

In webserver need webpage , we pull webpage from gitHub using new Job. 

### Step-3: [On Jenkins GitHubjob1]

#### 2nd Job: 
Now here i create new job which pull the code from GitHub and Deploy that code 'webpage' to apache webserver DocumetRoot location that is /var/www/html.

- Note:

Here use GitHub repo URL and "Branches to build" same where our code kept on GitHub in my case main is branch.

![Screenshot 2024-04-13 181522](https://github.com/Pratikshinde55/Jenkins/assets/145910708/5990ca24-38f8-46b2-ae85-f7295edfd731)

-Note:

But every time new code push on GitHub by developer then i need to Build my job again this is make slow or manual because of this i use "triggers"
Here use "Poll SCM" Schedule for every min. means this helps to automatically pull code from gitHub not need to manually Build job, Whenever new code on GitHub 
then **Poll SCM trigger** automatically download that code.

![Screenshot 2024-04-13 181820](https://github.com/Pratikshinde55/Jenkins/assets/145910708/3a90bd78-7997-452e-979f-7b5c3ac4ee53)

 - Note: 

That downloaded code is save in jenkins workspace of that job.(This save after when we 1st time Build job then automatically it updated by Poll SCM)

![Screenshot 2024-04-13 182315](https://github.com/Pratikshinde55/Jenkins/assets/145910708/ec01e703-05d4-46f6-a5d3-c04d2fa02f59)

Now, last step of job is to copy code or webpage which is downloaded from GitHub, This downloaded code copy to **/var/www/html**

![Screenshot 2024-04-13 182528](https://github.com/Pratikshinde55/Jenkins/assets/145910708/045d9773-c284-47a8-a4df-fd2e05a1e8a3)

Now apply & save job.

 - Note:
**This job run on jenkins and jenkins is on EC2 amazon linux, this job run only if in our host amazon linux2 EC2 have git so we need to install git on amazon 
linux2 where jenkins installed.**
     
     sudo yum install git -y

![Screenshot 2024-04-13 183152](https://github.com/Pratikshinde55/Jenkins/assets/145910708/ab9e56bb-0593-48ee-a313-d32a479a7a0e)


Now we need run 1st time manually job i my case name of job is GitHubjob1, after 1st time we run that job automatically run when new code updated on gitHub.

Click on Build now button of jenkins of Githubjob1

All set-up is done now i can change in code as developer from local laptop using Git Bash app and commit that code, After commit new code automatically push to 
gitHub by Hooks & whenever that new code go to GitHub, On jenkins Job2 named as GitHubjob1 is automatically run using Poll SCM trigger.

### Step-4: [On Browser]

Now check connect webserver from browser for view webpage or content:

Public Ip of instance in my case public ip of EC2 is - "http://52.66.237.252/"

 - Note :

  EC2 instance inbound rule must allow port no 80 that is http:

![Screenshot 2024-04-13 184308](https://github.com/Pratikshinde55/Jenkins/assets/145910708/90e71a4f-b593-4a2c-8246-cd6c69c2bade)

 - Note:

Whenever New webpage (code from developer to GitHub) comes then Jenkins job work and new webpage come by Fully Automation no need to manual update or Build job 
again and again:

![image](https://github.com/Pratikshinde55/Jenkins/assets/145910708/c726e158-b74f-451b-9413-c79644f805ac)
