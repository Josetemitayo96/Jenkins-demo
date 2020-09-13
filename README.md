# Jenkins-demo
using Jenkins for a node application
This is a repo for building a node project using jenkins without code
follow the following instructions
Using jenkins with a nodeapp without code

- add nodejs plugin to the jenkins

	- Go to manage jenkins

	- Click manage plugins install nodejs plugin

	- click on global tool config to config the plugin

- click on New item

- Enter name and choose freestyle project and then OK

- Click on GIT and add the repo

- under the build environment

	- click on provide Node & npm bin/folder to PATH

	- Add the nodejs plugin

- click on the build step

- click on Execute shell

- add shell script like -npm install

- click on save

- click on build now

For building and pushing docker image to docker hub without code using the following guidelines


Using Docker with jenkins pipeline without code

- Install docker

- $ sudo mkdir -p /var/jenkins_home

- $ sudo chown -R 1000:1000 /var/jenkins_home/

- Create a dockerfile to run jenkins container with docker installed inside. you can find the dockerfile here   (https://github.com/Josetemitayo96/jenkins-docker)

- build the image ** docker build -t jenkins-docker .

- Run the image 

	docker run -p 8080:8080 -p 50000:50000 -v /var/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins -d jenkins-docker

	-v /var/run/docker.sock:/var/run/docker.sock   -- to connect the docker volume in the server to the one in the container to solve permission error

- ssh into the container as root 

	 docker exec -u root -it jenkins bash

- usermod -a -G docker jenkins

- chmod 666 /var/run/docker.sock

- On the jenkins dashboard

- Install the plugin CloudBees Docker Build and Publish plugin

	- Go to manage jenkins

	- Click manage plugins CloudBees Docker Build and Publish plugin

- click on New item

- Enter name and choose freestyle project and then OK

- select build step

- Click on docker build and publish input your docker repo, put your docker hub credentials

- click save

- build now


######################
#jenkinspipeline for a node app and also to build and publish docker image
######################

-  Node: Influence on what jenkins worker node the job will be ran (here: any node, since we dont have a worker node or slave node)

- def: to declare variable

- stage: defines a building stage  preparation, test and docker build and publish stage

- checkout scm : To clone our git repo

- sh "git rev-parse --short HEAD > .git/commit-id": to give us the commit id and store it in a file (.git/commit-id)

- nodejs(nodeJSInstallationName: 'nodejs'): allow us to run npm, using the tool 'nodejs' in our jenkins

- docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') : Means doing something in docker with a standard registry 'https://index.docker.io/v1/' and login with 'dockerhub' credentials in our jenkins

- Go to your jenkins dashboard and install the docker pipeline plugin



