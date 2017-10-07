# MIT license

# our base image is the centos one
FROM jboss/wildfly:latest

LABEL Wildfly 10 with console enabled

# Expose the ports we're interested in
EXPOSE 9990

RUN /opt/jboss/wildfly/bin/add-user.sh admin admin --silent

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
