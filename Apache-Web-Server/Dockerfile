# Selecting Ubuntu as Base Image for building docker img
FROM ubuntu:latest

# Update packages and Install apache2 on top of Ubuntu base img.
# RUN command executes a Shell command inside a docker container during the build process. 
RUN apt-get update && apt-get install -y apache2

# Exposing the port. 80 is the default port for Apache web server.
EXPOSE 80

# wkt CMD specifies the default command to run when the docker container starts.
# This  command starts the Apache web server in the foreground and allows container to run as the main process.
# It ensures that container does not exit immediately after starting and that it continues to run untill it's manually stopped/terminated. 
CMD ["apache2ctl", "-D", "FOREGROUND"]
