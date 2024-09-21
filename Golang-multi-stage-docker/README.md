# Multi-Stage Docker Build with Go

This project demonstrates the use of multi-stage Docker builds with a Go (simple calculator) application. 
Go is an ideal choice for this demonstration because it compiles to a single, statically-linked binary that doesn’t require an external runtime environment.

## Why Go?

Go (Golang) is a statically-typed programming language that compiles directly to machine code. 
This means it does not rely on a runtime environment like dynamically-typed languages such as Python, Ruby, or JavaScript. 
The compiled Go binary can be executed directly by the operating system, which makes it particularly suitable for creating minimal Docker images.

## Benefits of Multi-Stage Docker Builds

Multi-stage Docker builds allow us to separate the build and runtime environments, leading to:

- **Smaller Image Size**: By excluding build dependencies and only including the final compiled binary, the resulting image is significantly smaller.
- **Enhanced Security**: A smaller attack surface due to fewer packages (minimalist) and dependencies.
- **Improved Performance**: Smaller images are quicker to pull, transfer, and deploy.

## Why Distroless Images?

Using distroless images further reduces the image size by excluding unnecessary components like package managers and shells. 

This results in:
- **Drastic Reduction in Image Size**: Only the essential files and the Go binary are included in the final image.
- **Increased Security**: Fewer components mean fewer potential vulnerabilities.

## Verify Images on Docker Hub

You can check the size of both images (`golang-calculator-with-multistage` and `golang-calculator-without-multistage`) by pulling them from Docker Hub.

### Pull Images

- **With Multi-stage Build**:
   
  ```bash
  docker pull deepscripts/golang-calculator-with-multistage:latest

- **Without Multi-stage Build**:
   
  ```bash
  docker pull deepscripts/golang-calculator-without-multistage:latest

## Conclusion

With Go’s static compilation and the power of multi-stage Docker builds, we can achieve lightweight, secure, and performant container images.
