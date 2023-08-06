#GitLab artifacts to store and access files generated during the CI/CD pipeline execution
## Topics 
- Prerequisite
- Add Artifacts in Pipeline
- Access Artifacts
- Delete Job Artifacts
 
## Prerequisite  
- GitLab Account

## Add Artifacts in Pipeline 
These artifacts is useful for sharing build outputs, test results, and other generated files between different stages or jobs in your pipeline.

To specify artifacts for a job, you use the artifacts keyword in the .gitlab-ci.yml configuration.

```
stages:
  - build
  - test

build:
  stage: build
  script:
    - echo "This is a sample text file." > sample.txt
  artifacts:
    paths:
      - sample.txt

test:
  stage: test
  script:
    - echo "Running tests..."
    # Your testing commands go here
```
!Note: 
In this example, we have two stages: "build" and "test," each containing a single job. The "build" job creates a sample text file called sample.txt, and the "test" job runs some testing commands (replace the comment with actual test commands).

## Access Artifacts
1.	Once the pipeline finishes successfully, go to the pipeline's page by clicking on the "CI/CD > Pipelines" menu.
2.	Find the pipeline that ran the "build" and "test" jobs and click on it to open the details.
3.	In the job details, you will see an "Artifacts" section for each job.
4.	Click on the "Download" button to download the artifacts (in this case, the sample.txt file for the "build" job).

![Snag_1a9e849](https://github.com/asiandevs/gitlab_cicd/assets/37457408/7c61deea-4535-43b5-9b52-da7a4e2da2e7)

## Delete Job Artifacts

On the job details page, scroll down to the "Artifacts" section.
Click the "Browse" button next to "Artifacts" to access the artifacts for the job.
In the artifacts browser, review the list of files and directories.
To delete specific artifacts, click the trash can icon next to the desired item.

![Snag_1ae8002](https://github.com/asiandevs/gitlab_cicd/assets/37457408/ef1b992e-a39f-486b-9cd1-f9e897a744a0)

By following these sorted steps, users can safely manage job artifacts in their GitLab project through the web interface. Careful attention should be given to avoid accidental deletions as this action cannot be undone.






