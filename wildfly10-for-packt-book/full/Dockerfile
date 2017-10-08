# DockerFile adapted from:
# https://github.com/jboss-dockerfiles/base/blob/master/Dockerfile
# https://github.com/jboss-dockerfiles/base-jdk
# https://github.com/jboss-dockerfiles/wildfly/blob/master/Dockerfile
# Copyright (c) 2014 Red Hat.
# All are governed by the MIT license

# our base image is the centos one
FROM centos:7

LABEL Custom image for centos7/openjdk8/wildfly10

# Install packages necessary to run EAP
RUN yum update -y && yum -y install xmlstarlet saxon augeas bsdtar unzip && yum clean all

# Create a user and group used to launch processes
# The user ID 1000 is the default for the first "regular" user on Fedora/RHEL,
# so there is a high chance that this ID will be equal to the current user
# making it easier to use volumes (no permission issues)
RUN groupadd -r jboss -g 1000 && useradd -u 1000 -r -g jboss -m -d /opt/jboss -s /sbin/nologin -c "JBoss user" jboss && \
    chmod 755 /opt/jboss

# Set the working directory to jboss' user home directory
WORKDIR /opt/jboss

# We use the root user to install openjdk
USER root

# We install the necessary packages with yum
RUN yum -y install java-1.8.0-openjdk-devel && yum clean all

# Switch back to jboss user
USER jboss

# Set the JAVA_HOME variable to make it clear where Java is located
ENV JAVA_HOME /usr/lib/jvm/java

# Set the WILDFLY_VERSION env variable
ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_SHA1 9ee3c0255e2e6007d502223916cefad2a1a5e333
ENV JBOSS_HOME /opt/jboss/wildfly

# We use the root user to install openjdk
USER root

# Add the WildFly distribution to /opt, and make wildfly the owner of the extracted tar content
# Make sure the distribution is available from a well-known place
RUN cd $HOME \
    && curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz \
    && sha1sum wildfly-$WILDFLY_VERSION.tar.gz | grep $WILDFLY_SHA1 \
    && tar xf wildfly-$WILDFLY_VERSION.tar.gz \
    && mv $HOME/wildfly-$WILDFLY_VERSION $JBOSS_HOME \
    && rm wildfly-$WILDFLY_VERSION.tar.gz \
    && chown -R jboss:0 ${JBOSS_HOME} \
    && chmod -R g+rw ${JBOSS_HOME}

# Ensure signals are forwarded to the JVM process correctly for graceful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true

# Switch back to jboss user
USER jboss

# Expose the ports we're interested in
EXPOSE 8080 9990

# Creates an administrative user for wildfly, which enables to log-in within the console
RUN /opt/jboss/wildfly/bin/add-user.sh -u admin -p admin --silent

# Set the default command to run when the conatiner is bootstrapped
# Tt starts WildFly in standalone mode and binds to all the network interfaces.
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
