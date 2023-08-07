# Docker Container Inside your GitLab CI pipeline
## Create a project access token:

On the left sidebar, at the top, select Search GitLab () to find your project.
Select Settings > Access Tokens

## Add access token as a Variable
![Snag_87f5dbc](https://github.com/asiandevs/gitlab_cicd/assets/37457408/b9fe0b4c-0b16-4029-a24f-8514be0f4856)

## create a Dockerfile
```
FROM nginx
LABEL maintainer="NGINX Docker File"
RUN apt-get update && apt-get upgrade -y
COPY index.html /usr/share/nginx/html
``

## Build and Push the image @GitLab Container Registry
you can add below entry .gitlab-ci.yml, where your Dockerfile is:

##.gitlab-ci.yml

```
stages:
  - package
  - validate

build_job:
  stage: package
  image: docker:latest
  services:
    - docker:dind
  script:
    - docker login -u $CI_REGISTRY_USER $CI_REGISTRY -p $DOCKER_SECRET
    - docker build -t $CI_REGISTRY_IMAGE .  
    - docker push $CI_REGISTRY_IMAGE

image_validate:
  stage: validate
  image: docker:latest
  services:
    - docker:dind
  script:
    - docker login -u $CI_REGISTRY_USER $CI_REGISTRY -p $DOCKER_SECRET
    - docker run --name mynginx -p 80:80 -d $CI_REGISTRY_IMAGE
    - apk add curl 
    - echo docker ps --filter "name=mynginx" --filter "status=running" > imagestatus.txt
  artifacts:
    paths:
      - imagestatus.txt
```

## Validate
![Snag_7a367ec](https://github.com/asiandevs/gitlab_cicd/assets/37457408/4dd57568-cbae-4855-b77b-462bc7d14d3e)

![Snag_7c8621c](https://github.com/asiandevs/gitlab_cicd/assets/37457408/d702d1f5-f062-45ce-97ea-9f2280f4d2d3)

## Delete Image
![Snag_7a5059e](https://github.com/asiandevs/gitlab_cicd/assets/37457408/54e8bd7d-2c61-4383-90e4-f7b687c5cac6)

![Snag_7a6efda](https://github.com/asiandevs/gitlab_cicd/assets/37457408/e71738a5-b41f-4420-9fb7-380981907607)

![Snag_87d41f1](https://github.com/asiandevs/gitlab_cicd/assets/37457408/6eebe4d5-9550-4b6a-b358-1707e0569459)

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


