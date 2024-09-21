###########################################
# BASE IMAGE
###########################################

FROM ubuntu AS build

# We can use a CentOS or Red Hat flavored UBI/UBI-Minimal or even a Golang base image as well.
# However, we cannot reduce the size of the image in the same way that multi-stage builds do.

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

############################################
# HERE STARTS THE BEAUTY OF MULTI STAGE BUILD
############################################

FROM scratch

# Copy the compiled binary from the build stage
COPY --from=build /app /app

# Set the entrypoint for the container to run the binary
ENTRYPOINT ["/app"]
