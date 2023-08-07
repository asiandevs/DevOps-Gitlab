# GitLab CI Deploy to EC2 using SSH 
## Step 1:Validate Gitlab-Runner on EC2 Linux Instance


```
[root@ip-10-0-6-75 .ssh]# sudo gitlab-runner --version
Version:      16.2.0
Git revision: 782e15da
Git branch:   16-2-stable
GO version:   go1.20.5
Built:        2023-07-21T22:52:35+0000
OS/Arch:      linux/amd64
[root@ip-10-0-6-75 .ssh]# sudo gitlab-runner status
Runtime platform                                    arch=amd64 os=linux pid=62656 revision=782e15da version=16.2.0
gitlab-runner: Service is running
[root@ip-10-0-6-75 .ssh]#

```
#Step 2:Grant sudo Permission to GitLab Runner User
After install GitLab Runner you will see gitlab-runner user in /home directory
```
[root@ip-10-0-6-75 .ssh]# cd /home
[root@ip-10-0-6-75 home]# ls
ec2-user  gitlab-runner
```
#Step 3 Install Apache Web Server
```
sudo yum update -y
sudo yum install -y httpd.x86_64
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
```
##Step 4 : Create a Simple HTML Web Page
Before we can test Apache web server, we need to change the permissions of the /var/www/html directory:
```
sudo chmod 777 /var/www/html
```
Now, we can create a simple HTML web page:
```
sudo vi /var/www/html/index.html
<!DOCTYPE html>
<html>
  <head>
    <title>Apache Web Server</title>
  </head>
  <body>
    <h1>Apache Web Server</h1>
    <p>This is a simple HTML web page.</p>
  </body>
</html>
```
![Snag_324cd8a](https://github.com/asiandevs/gitlab_cicd/assets/37457408/a4967f2d-2eea-404d-addc-b03aad070e20)

#Step 5:Add SSH server details as GitLab Variable
Add EC2 instance or SSH server details like SSH Private key, EC2 IP Address and SSH in GitLab CI CD Variables. To add variables in GitLab follow below steps.

Go to settings<<CI/CD<<variables<<Expand it

#Add private key in $SSH_PRIVATE_KEY variable
#Add Server Ip in $EC2_IPADDRESS variable
#Add server user in $SSH_USER variable
Note : When creating variables you have to remove protect variable flag
![Snag_30b7571](https://github.com/asiandevs/gitlab_cicd/assets/37457408/9d4bb449-18b0-4610-a174-06def98ca0a2)


