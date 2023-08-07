#  Docker Container Inside your GitLab CI pipeline

## Dockerfile
```
FROM python:3.10
RUN pip3 install pytest
```

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

![Snag_7a367ec](https://github.com/asiandevs/gitlab_cicd/assets/37457408/4dd57568-cbae-4855-b77b-462bc7d14d3e)

Validate:
![Snag_7a5059e](https://github.com/asiandevs/gitlab_cicd/assets/37457408/54e8bd7d-2c61-4383-90e4-f7b687c5cac6)

Delete Image:

![Snag_7a6efda](https://github.com/asiandevs/gitlab_cicd/assets/37457408/e71738a5-b41f-4420-9fb7-380981907607)
