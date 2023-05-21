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

---

## Prompts for creating manifests with kubectl ai

| NAME | PROMPT | DESCRIPTION | EXAMPLE |
| --- | --- | --- | --- |
| app.yaml | Create pod with name "app" for image gcr.io/kbot-385713/demo:v1.0.0, with 2 labels: app:demo and app:run, containerPort named http and port 8000 | This is a manifest for creating a pod | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app.yaml) |

| | | | | 
