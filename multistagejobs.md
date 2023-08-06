## Jobs with Stages

-  stages are defined at the top using the stages keyword. 
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
![Snag_bdecd9](https://github.com/asiandevs/gitlab_cicd/assets/37457408/bdce157f-d180-43ab-9fd3-ca18905b8519)

