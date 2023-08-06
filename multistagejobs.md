

```

stages:
   - clean
   - build
   - test
   - deploy

StgCleaning:
   stage: clean
   script:
      - echo "Cleaning the code"

StgBuilding:
   stage: build
   script:
      - echo "Building the code"

StgTesting:
   stage: test
   script:
      - echo "Testing the code"

StgDeploying:
   stage: deploy
   script:
      - echo "Deploying the code"

```
