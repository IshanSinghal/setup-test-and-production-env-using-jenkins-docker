# How to setup separate test and production environments by integrating github-jenkins-docker.

NOTE: This blog assumes you know how to or you have already installed jenkins and docker.

#SETUP
First, we set up JOB1 to track changes to the developer branch in github.
Changes are downloaded to JOB1 workspace and a fresh test environment is set up using docker httpd image.
