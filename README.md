# update_PR_status_with_jenkins_build_status
update_PR_status_with_jenkins_build_status

Steps:
=======
1. Install and configure Jenkins
2. Install GitHub plugin
3. Generate github Personal access tokens
4. create secret key with the PAT generated in step 3
5. Configure Jenkins to access the Github Repo using the secret key
6. Create Jenkins Job
7. create webhook in github repo to trigger jenkins job 


**1. Install and configure Jenkins**

a. Install Java 

    sudo amazon-linux-extras enable corretto8 -y
    sudo yum install java-1.8.0-amazon-corretto* -y
    sudo alternatives --config java
 
b. Install Jenkins 

    sudo wget -O /etc/yum.repos.d/jenkins.repo     https://pkg.jenkins.io/redhat-stable/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
    sudo yum upgrade
    sudo yum install jenkins -y
    sudo systemctl enable jenkins
    sudo systemctl start jenkins
    sudo systemctl status jenkins

Now you can access jenkins on http://host_ip:8080 address.
The initial admin password will be located at : "/var/lib/jenkins/secrets/initialAdminPassword"

Please proceed with the installed the suggested plugins.

**2. Install GitHub plugin**

IF you have proceed with the installed the suggested plugins during jenkins setup then it will be automatically there, else you need to goto Manage Jenkins --> Plugin Manager --> Available --> Search for GitHub plugin -->contnue with  "install without restart" option.

<img width="1007" alt="image" src="https://user-images.githubusercontent.com/74225291/184620382-a5342f42-0ef1-4cbc-b2b8-269ee2699756.png">


**3. Generate github Personal access tokens**


![image](https://user-images.githubusercontent.com/74225291/184621012-5a809495-4d7c-49d0-a74b-3c912706b444.png)

![image](https://user-images.githubusercontent.com/74225291/184621031-41429845-2eb4-4d9b-bed1-e1a1f1fe8b31.png)

![image](https://user-images.githubusercontent.com/74225291/184621097-89a131c4-bcd9-4029-b5a1-09b974ee71f0.png)

![image](https://user-images.githubusercontent.com/74225291/184621140-88af2d87-6a5a-4525-966e-274a95b216d8.png)

**4. create secret key with the PAT generated in step 3**

Goto Manage jenkins --> Manage Credentials --> Add credentials

![image](https://user-images.githubusercontent.com/74225291/184621981-ec42c363-0ff3-4cc6-b789-1e3cf118465e.png)


![image](https://user-images.githubusercontent.com/74225291/184622017-9dc64a2e-3dd6-44e4-9b29-ff90376e3f1e.png)


![image](https://user-images.githubusercontent.com/74225291/184622058-4a4b83dd-df95-4070-9903-9746c365ad68.png)


<img width="1410" alt="image" src="https://user-images.githubusercontent.com/74225291/184622826-93de7c16-cec7-4357-8cb8-7fa01f83c12c.png">


**5. Configure Jenkins to access the Github Repo using the secret key**

Goto Manage jenkins --> configure system

<img width="1424" alt="image" src="https://user-images.githubusercontent.com/74225291/184622545-878e0603-e756-43ba-b342-a34d08ca26ab.png">

**6. Create Jenkins Job**

New Iteam --> Give Job Name --> Select pipeline type

<img width="1337" alt="image" src="https://user-images.githubusercontent.com/74225291/184623018-70e7031b-1ee2-44ec-ab65-b904ab4b6a03.png">

In Build Triggers --> select "GitHub hook trigger for GITScm polling"

<img width="1016" alt="image" src="https://user-images.githubusercontent.com/74225291/184623297-a6f242be-1529-43b7-bc6e-1dfa68869868.png">

In Pipeline --> Select "Pipeline script from SCM" --> Select SCM as GIT. --> Repository URL --> Give your github repo path
 
<img width="1092" alt="image" src="https://user-images.githubusercontent.com/74225291/184623562-fc592dbd-94b7-4190-a963-52e9acdaf33a.png">

<img width="1173" alt="image" src="https://user-images.githubusercontent.com/74225291/184623818-b4e4ab8d-2807-459b-9199-83499fa59d7a.png">

Save and build the job once.


**7. create webhook in github repo to trigger jenkins job**

Goto github repo --> settings --> webhooks --> add webhooks

<img width="1340" alt="image" src="https://user-images.githubusercontent.com/74225291/184625897-fca116b6-79bd-473f-985a-5a37f4002439.png">

In Let me select individual events. --> select "Pull requests" and "Push" option.

<img width="1167" alt="image" src="https://user-images.githubusercontent.com/74225291/184626649-2440a8a0-cfb7-479e-819e-0e45e65c5985.png">


Now check the number of ran jobs in Jenkins before raising any new PR, For me it was 6.

<img width="1327" alt="image" src="https://user-images.githubusercontent.com/74225291/184626709-5fedbb69-a01b-4208-9478-8a06cb47f7da.png">

Now lets create new branch and raise Pull Request.

Now you can see one more job is triggered and PR has one more check which is passed.

<img width="1338" alt="image" src="https://user-images.githubusercontent.com/74225291/184628003-28214aca-8836-442a-aeba-6f38d03034d7.png">
