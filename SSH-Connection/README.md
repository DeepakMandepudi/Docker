# Enabling SSH Connection Between Two Ubuntu Containers in Docker

This project demonstrates how to set up an SSH connection between two Ubuntu containers in Docker.

## Steps Involved:

1. **Install the Ubuntu image from Docker Hub**
2. **Create two containers from the Ubuntu image**
3. **Run container1 and configure SSH:**
   - Install the **openssh-server** package.
4. **Run container2 and configure SSH:**
   - Install **openssh-client** to initiate outgoing SSH connections.
5. **Set a password for the root user in container1** and obtain its IP address.
6. **Connect from container2 to container1 using SSH.**

## Key Takeaways:

1. **Improved Security:** Enabling SSH creates a secure, encrypted connection, ensuring confidentiality, integrity, and authenticity of data.
2. **Data Protection:** Helps protect applications and data from unauthorized access and breaches.
3. **Ease of Management:** Docker simplifies the deployment and management of containers, reducing complexity and improving infrastructure management.
4. **Better Collaboration:** Multiple team members can work on the same application simultaneously, using SSH to communicate between containers.
5. **Scalability:** Containers are lightweight and can be easily scaled up or down to meet application demands.
6. **Portability:** Containers can be moved across different environments and cloud providers without worrying about dependency or configuration issues.

## Commands

- **Pull the Ubuntu image from Docker Hub:**
   
  ```bash
  docker pull ubuntu

- **Verify the Images**
   
  ```bash
  docker images

- **Create a project directory and navigate to it:**
   
  ```bash
  mkdir Project && cd Project

- **Run container1:**
   
  ```bash
  docker run -it --name container1 ubuntu

- **Install SSH server in container1:**
   
  ```bash
  apt-get update && apt-get install openssh-server

- **Configure SSH in container1:**
   
  ```bash
  apt-get install vim -y && vim /etc/ssh/sshd_config

- In the config file, uncomment:

  - PermitRootLogin yes





- **Restart SSH server in container1:**
   
  ```bash
  service ssh start && service --status-all

- **Exit container1:**
   
  ```bash
  exit

- **Create container2 and install SSH client:**
   
  ```bash
  docker run -it --name container2 ubuntu
  apt-get update && apt-get install openssh-client
  exit

- **Set a new password for the root user in container1:**

    - Start container1 and access it:
      
  ```bash
  docker start container1 && docker exec -it container1 bash
- Set a new password:
  ```bash
  passwd root 

 - Exit container1:
      ```bash
   exit      
- **Retrieve the IP address of container1:**
   
  ```bash
  docker inspect container1 | grep IPAddress

- **Connect from container2 to container1:**
   
  ```bash
  docker start container2 && docker exec -it container2 bash

- **SSH into container1 using its IP address:**
   
  ```bash
  ssh root@<IPAddress_of_container1>

- **Troubleshoot if connection is refused:**
     - Ensure SSH service is running in container1:
       ```bash
       docker exec -it container1 bash
       service --status-all
       service ssh start
       exit

- **Retry SSH connection from container2:**
    ```bash
    docker exec -it container2 bash
    ssh root@<IPAddress_of_container1>


## Success! You have successfully enabled the SSH connection between two Docker containers.


#### The Below Image shows the successful SSH connection between Ubuntu Docker container1 and container2.
![Screenshot](https://github.com/DeepakMandepudi/Docker/blob/main/SSH-Connection/SSH-Connection-Screenshot.png)

