## Go Demo App

### Requirements
go 1.20.3
docker 20.10.22
k3d 5.4.9

### How to check app

Run this command in a terminal from the project's folder

```
go build -o bin/app src/main.go
bin/app

```
open another tab in terminal and check app with curl or open in a browser url http://localhost:8080


``` 
curl localhost:8080                                                                                                                                                                                     <aws:DevelopmentCampaign_Administrator>
<!DOCTYPE html>
<html>
<!-- This should work everywhere -->
<head>
    <script type="text/javascript" src="vivus.min.js"></script>
    <script type="text/javascript">
...
```

### Create docker image 

``` 
docker build -t <dockerhub_username>/go-demo-app:v1.0.0 .
docker push <dockerhub_username>/go-demo-app:v1.0.0

```

### Run app in the K8s cluster

``` 
k3d cluster create demo
kubectl create deploy demo --image <dockerhub_username>/go-demo-app:v1.0.0
```
