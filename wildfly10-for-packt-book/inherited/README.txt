 Custom DockerFile that extends the official wildfly one
 the MIT license
 
 1) to build the dockerFile (this lasts about 15 minutes):
 docker build -t local/img-wildfly-official:10 .
 
 2) to create an run a container:
 docker run -d --name ctnr-wildfly-official -p8080:8080 -p9990:9990 local/img-wildfly-official:10

 3) to stop this container, we can use:
 docker stop ctnr-wildfly10-official

 4) to start our container again after it has been stopped, we can use:
 docker start ctnr-wildfly10-official

 5) to delete this container, we can use:
 docker rm ctnr-wildfly10-official
 
 5) to delete our image from the local cache, we can use:
 docker rmi local/img-wildfly-official:10