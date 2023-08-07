# Create new GitLab project

Login into GitLab and navigate to New project -> Create from template -> Pages/Plain HTML -> Use template. Give it a project name and hit Create project. This will create a simple plain html project.
![Snag_26f6ca](https://github.com/asiandevs/gitlab_cicd/assets/37457408/fbb8de35-4294-4187-9e90-fe62bd208a38)
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
