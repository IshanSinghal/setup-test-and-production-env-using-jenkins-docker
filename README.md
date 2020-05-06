# How to setup separate test and production environments by integrating github-jenkins-docker.

NOTE: This blog assumes you know how to or you have already installed jenkins and docker.

## SETUP

### First, we set up JOB1 to track changes to the developer branch in github.
Changes are downloaded to JOB1 workspace and a fresh test environment is set up using docker httpd image.

![Job1 config](/images/2.jpg)
![Job1 config](/images/3.jpg)

to copy files to test folder linked to test server:
sudo cp -v -r -f * /devfiles

To remove old test environment if it exists:
if sudo docker ps -a | grep devserver
then
sudo docker rm -f devserver
else
echo "no devserver"
fi

To run new test server using httpd os image:
sudo docker run -d -t -i -p 8082:80 -v /devfiles:/usr/local/apache2/htdocs --name devserver httpd

Initial Test Page:
![Dev server init](/images/1.jpg)


### Now we set up JOB2 - This job detects changes to master branch and downloads the files to its workspace. Then it transfers files to production server. It is triggered by JOB3.
![Job1 config](/images/6.jpg)
![Job1 config](/images/5.jpg)



### Now we set up JOB3 - This job is triggered manually by the QA team after they find the test server environment is fit for production. This job merges the developer branch to master branch.
![Job1 config](/images/7.jpg)
![Job1 config](/images/8.jpg)
![Job1 config](/images/9.jpg)


## Now let us see the result.

When developer pushes a change.
![Job1 config](/images/11.jpg)
JOB1 creates a new test environment and launches test webserver.
![Job1 config](/images/12.jpg)

QA team triggers JOB3 if dev server is approved. This merges the changes to master branch and then JOB2 is triggered. Now jenkins downloads the changes and tranfers it to production webserver.
We can create a public IP with ngrok to make the page visible to the outside world.
![Job1 config](/images/14.jpg)

### Production server updated:
![Job1 config](/images/15.jpg)
