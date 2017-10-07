 Custom DockerFile 
 the MIT license
 
 1) to build the dockerFile:
 docker build -t local/img-hello-java:jdk8 .
 
 2) to create an run a container:
 docker run -it --name ctnr-hello-java-jdk8 local/img-hello-java:jdk8

 3) to stop this container, we can use:
 docker stop ctnr-hello-java-jdk8

 4) to start our container again after it has been stopped, we can use:
 docker start ctnr-hello-java-jdk8

 5) to delete this container, we can use:
 docker rm ctnr-hello-java-jdk8
 
 5) to delete our image from the local cache, we can use:
 docker rmi local/img-hello-java:jdk8