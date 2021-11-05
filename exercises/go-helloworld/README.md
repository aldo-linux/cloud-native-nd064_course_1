# Go Hello World

This is a simple Go web application that prints a "Hello World" message.

## Run the application

This application listens on port `6111`

To run the application, use the following command:
```
go run main.go 
```

Access the application on: http://127.0.0.1:6111/

## Docker Commands

1. Build the docker image

- In the directory where the Dockerfile resides:
```
docker build -t go-helloworld .
```

2. Run and stop the docker image

```
docker run -d -p 6111:6111 go-helloworld
docker stop <CONTAINER ID>
```

3. Tag and push the docker image to DockerHub
```
docker tag go-helloworld aldolinux/go-helloworld:v1.0.0
docker push aldolinux/go-helloworld:v1.0.0
```

## Deploy into Kubernetes

We need to make sure the image is available in dockerhub.com for the command below to work

```
kubectl create deploy go-helloworld --image=aldolinux/go-helloworld:v1.0.0
kubectl port-forward pod/go-helloworld-5949c69669-l9g4s 6111:6111
kubectl expose deployment go-helloworld --port=6111 --target-port=6111
```

It is possible to edit the application configuration by typing:

```
kubectl edit deploy go-helloworld -o yaml
```

## Issues
1. Got an issue perfoming ```docker login```. Got the error: "Error saving credentials: error storing credentials - err: exit status 1, out: `Cannot create an item in a locked collection`"

SOLUTION: https://stackoverflow.com/questions/50151833/cannot-login-to-docker-account 

2. While deploying to K3S for the first time i got the ```Error: failed to create containerd container: get apparmor_parser version: exec: "apparmor_parser": executable file not found in $PATH``` error 

SOLUTION: run in the vagrant VM the command: ```zypper install apparmor-parser apparmor-utils```