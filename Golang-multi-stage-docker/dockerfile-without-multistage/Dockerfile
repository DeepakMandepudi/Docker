###########################################
# BASE IMAGE
###########################################

FROM ubuntu AS build

# AS is alias with name build, to pass the binary if you have multiple stages

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

# Copy source code

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

ENTRYPOINT ["/app"]

