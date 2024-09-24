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

### 1. Pull the Ubuntu image from Docker Hub:
```bash
docker pull ubuntu
