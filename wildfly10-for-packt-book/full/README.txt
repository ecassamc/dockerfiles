 Custom DockerFile adapted from:
 https://github.com/jboss-dockerfiles/base/blob/master/Dockerfile
 https://github.com/jboss-dockerfiles/base-jdk
 https://github.com/jboss-dockerfiles/wildfly/blob/master/Dockerfile
 Copyright (c) 2014 Red Hat.
 All are governed by the MIT license
 
 1) to build the dockerFile (this lasts for about 15mniutes):
 docker build -t local/img-wildfly:10 .
 
 2) to create an run a container:
 docker run -d --name ctnr-wildfly10 -p8080:8080 -p9990:9990 local/img-wildfly:10

 3) to stop this container, we can use:
 docker stop ctnr-wildfly10

 4) to start our container again after it has been stopped, we can use:
 docker start ctnr-wildfly10

 5) to delete this container, we can use:
 docker rm ctnr-wildfly10
 
 5) to delete our image from the local cache, we can use:
 docker rmi local/img-wildfly:10