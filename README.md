# How to setup separate test and production environments by integrating github-jenkins-docker.

NOTE: This blog assumes you know how to or you have already installed jenkins and docker.

## SETUP

### First, we set up JOB1 to track changes to the developer branch in github.
Changes are downloaded to JOB1 workspace and a fresh test environment is set up using docker httpd image.
![Job1 config](/images/2.jpg)
![Job1 config](/images/3.jpg)
Initial Test Page:
![Dev server init](/images/1.jpg)


### Now we set up JOB2 - This job detects changes to master branch and downloads the files to its workspace. Then it transfers files to production server.
![Job1 config](/images/5.jpg)
![Job1 config](/images/6.jpg)


### Now we set up JOB3 - This job is triggered manually by the QA team after they find the test server environment is fit for production. 
![Job1 config](/images/7.jpg)
![Job1 config](/images/8.jpg)
![Job1 config](/images/9.jpg)
