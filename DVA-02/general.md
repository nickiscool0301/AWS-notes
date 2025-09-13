# CodeDeploy - CodeBuild - Code Pipeline


- CodeDeploy: 
    - deployment service
    - deploy to EC2 instances, on-premises instances, serverless 
    lambda

- 2 types of deployments:
    - in-place deployment
    - blue-green deployment: 
        -   enables user to verify a new deployment of service before sending production traffic to it
        - provision a new set of instances then reroute traffic

- CodeBuild: fully managed CI service that compiles the code, run tests and produces software packages


- CodePipeline: automates the build, test and deploy phases of release process everytime there is a code change