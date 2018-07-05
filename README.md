## Demo Walkthrough

This Spring app has a single REST endpoint for saying Hello. It uses an embedded Tomcat server via Spring Web to 
smoothly run in Docker. I also added the maven-resources plugin to make packaging easier.

1. Package the app 
`mvn package`
2. Navigate to target directory
`cd target`
3. Build docker image
`docker build . -t <demo`
4. Run locally
`docker run -p 8080:8080 demo:latest`

Create a Dockerhub account and make a demo repository. Login
```bash
docker login
```

Retag your image and push it
```bash
docker tag demo <your-username>/demo
docker push <your-username>/demo:latest
```

#### The following commands require an AWS access key and ID. 

Configure your credentials
`aws configure`

Create a remote docker host on aws
`docker-machine create --driver amazonec2 --amazonec2-open-port 8080 --amazonec2-region us-east-1 docker-demo`

Connect to the remote host
`docker-machine env docker-demo`
`eval $(docker-machine env docker-demo)`

Run the demo on the remote host
`docker run  -p 8080:8080 <your-username>/demo:latest`


Navigate to the public DNS of your EC2 instance on port 8080 and you should see HelloWorld