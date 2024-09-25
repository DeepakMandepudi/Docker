# Dockerizing Apache Web Server

This project demonstrates how to Dockerize an Apache Web Server. It uses Docker to isolate the web server and its dependencies from the host machine, providing a clean and consistent server environment.

## Dockerfile

The Dockerfile used to build this image includes the following steps:

1. **Base Image:**
   - Use the latest Ubuntu image as the base for the container.
   ```dockerfile
   FROM ubuntu:latest
#### Why Ubuntu?
- Stability: Ubuntu is a stable, secure, and widely supported operating system.
- Package Management: The extensive package management through apt-get makes it easy to install and manage Apache and its dependencies.


2. **Update packages and install Apache2 on Ubuntu base image:**
   - The RUN command executes a Shell command inside a docker container during the build process.
   ```dockerfile
   RUN apt-get update && apt-get install -y apache2

3. **Exposing the port. 80 is the default port for the Apache2 web server**
   - This tells Docker that the container will use port 80 for incoming HTTP connections.
   ```dockerfile
   EXPOSE 80
4. **Starting Apache in the Foreground**
   - apache2ctl -D FOREGROUND: Starts Apache in the foreground, ensuring the container doesn’t exit after execution. Without this, the container would immediately stop once Apache is started.
   - To ensure that the container stays active and continues running, Apache needs to be launched in the foreground.
   ```dockerfile
   CMD ["apache2ctl", "-D", "FOREGROUND"]
5. **Customization**
   - You can modify the command to run scripts or other processes on startup along with Apache.
   ```dockerfile
   CMD ["sh", "-c", "/path/to/your/script && apache2ctl -D FOREGROUND"]

## **Building and Running the Docker Image**

**Build and Run the Docker Image**

1. **Build the Image:**
    ```bash
    docker build -t apache-image .
2. **Run the Container:**
   ```bash
   docker run -p 80:80 apache-image
Explanation:
- **docker build -t apache-image .:** Builds a Docker image from the Dockerfile in the current directory and tags it as apache-image.
- **docker run -p 80:80 apache-image:** Runs a container from the apache-image and maps port 80 on the container to port 80 on the host machine.

## **Accessing the Apache Web Server:**
   - After running the container, open your browser and go to http://localhost to see the default Apache page.

1. **Running on EC2 and Accessing from Your Local Machine:**
   - If you want to access the Apache server from your local machine or browser, you'll need to ensure the following:
     - Open Port 80 (or your chosen port) in the EC2 Security Group
     - This will bind the container’s port 80 (where Apache is running) to your EC2 instance’s port 80 or 8080.
     - Run Docker on a Public Port
         ```bash
         docker run -p 80:80 apache-image
  
         docker run -p 8080:80 apache-image
2. **Access from Your Local Machine:**
   - To access the web server from your local machine, open your browser and go to:
     ```bash
     http://<EC2-Public-IP>:80
   - or if using port 8080:
     ```bash
     http://<EC2-Public-IP>:8080
3. **Running Locally on EC2 (Access from inside the EC2 instance):**
   - If you only need to access the Apache web server locally from the EC2 instance itself (inside the instance), you can use:
     ```bash
     docker run -p 127.0.0.1:8080:80 apache-image
   - This binds the container’s port 80 to the EC2 instance’s local port 8080, and you can curl from the EC2 instance itself to check if it's running:
     ```bash
     curl http://localhost:8080 
## **Troubleshooting**

#### **If another service or container is already using port 80 on your host machine:**

- **Option 1: Stop the Service/Container Using Port 80**
   - You can check which process or container is using port 80 and stop it.
   - Find the process using port 80: Run the following command to check which process is using port 80:
     ```bash
     sudo lsof -i :80
   - If it's an existing Docker container, you'll see an entry with its container ID. Otherwise, it might be a web service like Nginx or Apache running directly on your host.
   - Stop the process: If it's a Docker container, stop it using:
     ```bash
     docker ps
   - Find the container ID of the container using port 80, then stop it:
     ```bash
     docker stop <container_id>
   - If it's a service like Apache or Nginx running on the host, stop it:
     ```bash
     sudo systemctl stop apache2   # If Apache is running
     sudo systemctl stop nginx     # If Nginx is running
- **Option 2: Use a Different Port**
  - If you don't want to stop the existing service on port 80, you can map your Docker container to a different port on the host, for example, port 8080.
  - Run the container with a different host port:
    ```bash
    docker run -p 8080:80 apache-image
  - This command maps port 80 of the container to port 8080 of your host machine, avoiding any conflict with the existing process on port 80.
  - Now, you should be able to access your Apache server on [(http://your-server-ip:8080)]

## Output Screenshot

<img width="1283" alt="Apache-Server-Output" src="https://github.com/user-attachments/assets/fa31f1b5-48ac-44e1-a1aa-fced728a3f85">

