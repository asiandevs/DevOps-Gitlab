# Docker Container Inside your GitLab CI pipeline

## create a Dockerfile
```
FROM python:3.10
RUN pip3 install pytest
```

## Build and Push the image @GitLab Container Registry
you can add below entry .gitlab-ci.yml, where your Dockerfile is:

##.gitlab-ci.yml
```
stages:
  - package

build_job:
  stage: package
  image: docker:latest
  services:
    - docker:dind
  script:
    - docker login -u $CI_REGISTRY_USER $CI_REGISTRY -p $DOCKER_SECRET
    - docker build -t $CI_REGISTRY_IMAGE .  
    - docker push $CI_REGISTRY_IMAGE
```
## Validate
![Snag_7a367ec](https://github.com/asiandevs/gitlab_cicd/assets/37457408/4dd57568-cbae-4855-b77b-462bc7d14d3e)

## Delete Image
![Snag_7a5059e](https://github.com/asiandevs/gitlab_cicd/assets/37457408/54e8bd7d-2c61-4383-90e4-f7b687c5cac6)

![Snag_7a6efda](https://github.com/asiandevs/gitlab_cicd/assets/37457408/e71738a5-b41f-4420-9fb7-380981907607)

## Issues:
GitLab CI fails with "dial tcp: lookup docker on x.x.x.x:53: no such host" when pulling docker:dind ....
To resolve this problem just add on /etc/gitlab-runner/config.toml a volume map to docker sock.
Solution :
```
 i. volumes = ["/var/run/docker.sock:/var/run/docker.sock", "/cache"]
ii. When building docker image in gitlab-ci, you must add this (dind is for "docker in docker"):
services:
  - docker:dind
```
