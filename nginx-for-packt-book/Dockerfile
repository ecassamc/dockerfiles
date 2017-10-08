#We use the the Alpine linux distribution, that serves as base fs layer
FROM alpine:latest

# metadata of the image
LABEL maintainer="Russ McKendrick <russ@mckendrick.io>"
LABEL description="This example Dockerfile installs NGINX."

# here we run commands that add the nginx software, and creates/deletes related directories.
RUN apk add --update nginx && \
        rm -rf /var/cache/apk/* && \
        mkdir -p /tmp/nginx/

#copy files from the host into the image. This creates two new FS layers
COPY files/nginx.conf /etc/nginx/nginx.conf
COPY files/default.conf /etc/nginx/conf.d/default.conf

#decompress the html.tar.gz archive, and place its content into the image.
#a new new FS layer is created for thsi
ADD files/html.tar.gz /usr/share/nginx/

# indicates to Docker that a process of our container is listening on the 80 port.
EXPOSE 80/tcp

# these two instructions are used in conjunction, so as to run 'nginx -g daemon off;'
ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]