# Setup a GitLab Runner in an AWS EC2
## Topics 
- Pre-request   
- What is GitLab Runner?
- What is the Executor of GitLab Runner?
- Install and Register GitLab Runner

## Pre-request
- GitLab Account
- A Linux Instance ( in my case AWS EC2)
  - Install Docker
  - Install NODEJS
  
## What is GitLab Runner?
GitLab Runner is an open-source continuous integration (CI) and continuous deployment (CD) tool that works in conjunction with GitLab. It facilitates the automation of building, testing, and deploying code changes to various environments.
GitLab Runner allows you to run jobs defined in .gitlab-ci.yml files and is an essential component of the GitLab CI/CD pipeline.

### Types
GitLab Runner comes in two main types:
- 1.	Shared Runners: These are runners provided by GitLab as a service. 
- 2.	Specific Project Runners: These are runners dedicated to a specific project.  

## Install and Register GitLab Runner
### Install a GitLab Runner
```   
# Download the binary for your system
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64

# Give it permission to execute
sudo chmod +x /usr/local/bin/gitlab-runner

# Create a GitLab Runner user
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

gitlab-runner --version
gitlab-runner list
``` 
### Register runner with Docker executor

```
sudo gitlab-runner register
```    
![Snag_196d0c6](https://github.com/asiandevs/gitlab_cicd/assets/37457408/931d6854-81f7-40c3-8c9f-74e6af11085d)

### Check Runner Status and verify
```
sudo gitlab-runner status
sudo gitlab-runner verify
```
![Snag_19a383c](https://github.com/asiandevs/gitlab_cicd/assets/37457408/83c5d844-aec1-4c15-99fd-5ea589f1df88)

### From Console - Check Runner Status and verify
GitLab => Project => Setting => CI/CD => Runners => Expand 
![Snag_19c2789](https://github.com/asiandevs/gitlab_cicd/assets/37457408/7a172113-c2b6-419b-bcdf-29a01e7ba95e)

    
