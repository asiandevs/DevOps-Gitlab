## Jobs with Stages of pipeline

GitHub/GitLab Jobs and Pipelines are concepts within GitHub/GitLab Actions, the continuous integration and continuous deployment (CI/CD) workflow system of GitHub.

A "Job" represents a defined set of steps that run as part of a workflow. Each job can perform specific tasks like building, testing, or deploying code. Jobs can run in parallel or sequentially, and their success or failure determines the overall status of the job.

A "Pipeline" is a series of jobs organized in a sequential or parallel manner.

- Stages are defined at the top using the stages keyword. 
- Each job is given a name (clean, build, test, and deploy) followed by a colon (:).
- The stage keyword is used to assign the job to a specific stage.

Within each job, you can define the set of commands to be executed under the script section. 

### example - configure jobs with stages in a .gitlab-ci.yml file:
```
# Define the stages in the pipeline
stages:
   - clean
   - build
   - test
   - deploy

# Job for cleaning the code or workspace
clean:
   stage: clean
   script:
      - echo "Cleaning the code"
      # Add other cleaning commands if needed

# Job for building the code
build:
   stage: build
   script:
      - echo "Building the code"
      # Add other build commands if needed

# Job for testing the code
test:
   stage: test
   script:
      - echo "Testing the code"
      # Add other testing commands if needed

# Job for deploying the code
deploy:
   stage: deploy
   script:
      - echo "Deploying the code"
      # Add other deployment commands if needed
```

TEST Output

![Snag_bdecd9](https://github.com/asiandevs/gitlab_cicd/assets/37457408/bdce157f-d180-43ab-9fd3-ca18905b8519)

#Test Stage - Parallel
```
# .gitlab-ci.yml
stages:
  - clean
  - build
  - test
  - deploy

clean:
  stage: clean
  script:
    - echo "Cleaning the code"
    # Add other cleaning commands if needed

build:
  stage: build
  script:
    - echo "Building the code"
    # Add other build commands if needed

test:
  stage: test
  script:
    - echo "Testing the code"
    # Add other testing commands if needed

parallel_test:
  stage: test
  script:
    - echo "Running parallel tests"
    # Add other testing commands for parallel testing
```

Test Output
![Snag_176d93e](https://github.com/asiandevs/gitlab_cicd/assets/37457408/8af58977-1b04-4b23-bb26-108388b57d2f)



