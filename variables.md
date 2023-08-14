# Create a variable in the project settings and use it in the pipeline.

## Topics  
- Prerequisite
## Prerequisite   
- GitLab Account
  - Add Credit or Debit Card in the GitLab Account
- A Project in GitLab  
    GitLab project with a .gitlab-ci.yml configuration file 

## What is GitLab CI/CD Variable?
GitLab variables provide developers with the ability to configure values in their code.    

## GitLab CI/CD Basic Variable Types 
Step 1: Setting up the Variable
* Setting up the Variable
    1. Go to your GitLab project.
    2. Navigate to Settings > CI/CD > Variables.
    3. Click on "Add Variable."
    4. Set the variable key as TEST_VARIABLE and the value as test_value.
![variable01](https://github.com/asiandevs/gitlab_cicd/assets/37457408/67bdc0af-6de5-4e8e-9ae3-d74944a346e5)

## Use Variable in a .gitlab-ci.yml file:
  ```
stages:
  - test

my_job:
  stage: test
  script:
    - echo "The value of TEST_VARIABLE is ${TEST_VARIABLE}"
  ```
## Use Variable in Pipeline ~ .gitlab-ci.yml file?
 
  ```
run_unit_test:
  stage: test
  before_script:
    - echo "Preparing test data..."
  script:
    - echo "Running unit tests for microservice $Jangla ..."
  after_script:
    - echo "Cleaning up temporary files.."
    - rm -r test-data
    - ls
  ```
## How to Print All Variables in Pipeline?
Add below two lines to get the variables
  ```
    - echo "GitLab CI/CD | Print all environment variables"
    - env
  ```
