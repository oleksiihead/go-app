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
| app-livenessProbe.yaml | Create pod with name "app" for image gcr.io/kbot-385713/demo:v1.0.0, metadata's name app-livenessprobe and namespace demo, with livenessProbe on port 8000, containerPort named http and port 8080, timeoutSeconds = 1, periodSeconds: 10, failureThreshold = 3, initialDelaySeconds = 5 | This is a manifest for creating a pod with livenessProvbe | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-livenessProbe.yaml) | 
| app-readinessProbe.yaml | Create pod with name "app" for image gcr.io/kbot-385713/demo:v1.0.0, metadata's name readinessProbe, with livenessProbe on port 8000, containerPort named http and port 8000, includes timeoutSeconds, periodSeconds, failureThreshold, initialDelaySeconds, with readinessProbe and values: path = /ready, port = 8000, periodSeconds = 2, initialDelaySeconds = 0, failureThreshold = 3, successThreshold = 1 | This is a manifest for creating a pod with livenessProvbe and readinessProbe | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-readinessProbe.yaml) |
| app-volumeMounts.yaml |Create pod with name "app" for image gcr.io/kbot-385713/demo:v1.0.0, metadata's name readinessProbe, with livenessProbe on port 8000, containerPort named http and port 8000, includes timeoutSeconds, periodSeconds, failureThreshold, initialDelaySeconds, with readinessProbe and values: path = /ready, port = 8000, periodSeconds = 2, initialDelaySeconds = 0, failureThreshold = 3, successThreshold = 1. And data volumes with hostPath = var/lib/app | This is a manifest for creating a pod with livenessProvbe, readinessProbe and volume | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-volumeMounts.yaml) |
| app-cronjob.yaml | Create manifest for CronJob which every 5 minutes executes bash command 'echo Hello world' with restartPolicy OnFailure | This manifest creates cronjob | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-cronjob.yaml) |
| app-job-rsync.yaml | Create manifest for Job which can copy files from gcePersistentDisk to volume data/input with ext4 file system with gsutil rsync, mountPath = /data/input, restartPolicy Never and backoffLimit = 0 | Manifest creates Job wich do rsync from gcePersistentDisk to host | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-job-rsync.yaml) |
| app-multicontainer.yaml | Create Pod for multi-container app. First image - nginx, second one - debian. Let debian executes script which records current date every 1 second to index.html and brings it to the front, where nginx displays the result. Nginx and debian must read and write to the same volume emptyDir | Manifwst for multi-container app with nginx and debian | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-multicontainer.yaml) |
| app-resources.yaml | Create pod with name "app" for image gcr.io/kbot-385713/demo:v1.0.0, metadata's name readinessProbe, with livenessProbe on port 8000, containerPort named http and port 8000, includes timeoutSeconds, periodSeconds, failureThreshold, initialDelaySeconds, with readinessProbe and values: path = /ready, port = 8000, periodSeconds = 2, initialDelaySeconds = 0, failureThreshold = 3, successThreshold = 1. Also pod must include resources: request cpu 100m, memory 128Mi, limits cpu 100m and memory 256Mi | Manifest allow create a pod with livenessProvbe, readinessProbe and resources  | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-resources.yaml) |
| app-secret-env.yaml | Create pod with name "app", metadata name - app-secret-env, image container redis and 2 secrets from secretKeyRef. First env SECRET_USERNAME, second SECRET_PASSWORD. restartPolicy Never | Manifest which creates environment variables from a secret  | [Example](https://github.com/oleksiihead/go-demo-app/blob/main/yaml/app-secret-env.yaml) |
