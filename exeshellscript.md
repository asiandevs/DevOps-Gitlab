# CI Deploy to EC2 using SSH to Remote Server with GitLab CI/CD Pipeline.
# Run Script via SSH to remote server

Login into GitLab and navigate to New project -> Create from template -> Pages/Plain HTML -> Use template. Give it a project name and hit Create project. This will create a simple plain html project.

The template cretaed README.md file, initial .gitlab-ci.yml and public directory with index.html and style.css files.

 # GitLab Runner
 It has already been setup 

 # Create SSH key
I am using EC2 Linux and created key pair on that VM
To create new key run ssh-keygen -t ed25519 -C "GitLab SSH key". Text after -C option is a comment and you can change it.

# Add GitLab Variable
Navigate to Settings -> CI/CD -> Variables -> Expand -> Add Variable
```
SSH_PRIVATE_KEY - paste private key
SSH_USER — name of the user on the remote server
VM_IPADDRESS — IP address of remote server
```
Below is gitlab-ci.yml with explanation to deploy code to EC2 instance using ssh.

```
stages:
  - deploy
#In this we have only one stage deploy
Deploy: 
  stage: deploy
  before_script:
  - command -v ssh-agent >/dev/null || ( apk add --update openssh )' 
  #The ssh-agent command outputs commands to set ce - cp -r * .public
rtain environment variables in the shell
  - eval $(ssh-agent -s)
 #The eval command tells the shell to run the output of ssh-agent as shell commands
  - echo "$SSH_PRIVATE_KEY" | tr -d '\r' | ssh-add -
#"$SSH_PRIVATE_KEY" in this we added private key in variable
  - mkdir -p ~/.ssh
#create a directory
  - chmod 700 ~/.ssh
# usually the tools which use that directory will ask you to assign permissions to it:
  - ssh-keyscan $EC2_IPADDRESS >> ~/.ssh/known_hosts
 #"$EC2_IPADDRESS" in this we added our instance ip_address in variable
  - chmod 644 ~/.ssh/known_hosts
#this is key file permission

  script:
```


```
stages:
  - deploy

Deploy: 
  stage: deploy
  before_script:
  - 'command -v ssh-agent >/dev/null || ( apk add --update openssh )' 
  - eval $(ssh-agent -s)
  - echo "$SSH_PRIVATE_KEY" | tr -d '\r' | ssh-add -
  - mkdir -p ~/.ssh
  - chmod 700 ~/.ssh
  - ssh-keyscan $EC2_IPADDRESS >> ~/.ssh/known_hosts
  - chmod 644 ~/.ssh/known_hosts
  script:
  - |
    ssh $SSH_USER@$EC2_IPADDRESS /bin/bash -s << EOT                                                                 
    set -x -o verbose;
    cd /var/www/html
    mkdir mkdir .public
    cp -r * .public
    mv .public public
    set +x
    EOT

```

# Access Sample Website

! ip_address/public

![Snag_99a1a6](https://github.com/asiandevs/gitlab_cicd/assets/37457408/0bb5c85a-82ed-4afd-912a-d7bc1d89d1b8)

