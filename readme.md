# Flask Kubernetes

Read the related blog post: [Running Flask frontend and backend in Kubernetes](https://mikaelahonen.com/en/blog/running-flask-frontend-and-backend-in-kubernetes/).

## Preparation

[Install docker](https://dev.solita.fi/2021/12/21/docker-on-wsl2-without-docker-desktop.html)

[Install minikube](https://minikube.sigs.k8s.io/docs/start/)

## Deploy

Run the following commands in shell 1.

Start Kubernetes:
```
minikube start
```

Make current environment available in Kubernetes:
```
eval $(minikube docker-env)
```

Build Docker images
```
docker build -t flask-frontend -f frontend/Dockerfile ./frontend
docker build -t flask-backend -f backend/Dockerfile ./backend
#docker image prune -f
```

Load Docker images to Kubernetes
```
minikube image load flask-frontend:latest
minikube image load flask-backend:latest
```

Deploy the Flask applications:
```
kubectl delete deploy flask-deployment
kubectl create -f ./k8s_deployment.yml
```

Publish the Flask applications:
```
kubectl delete service flask-services
kubectl create -f ./k8s_service.yml
```

Confirm that services exist:
```
kubectl get services
```

Expose services to the host:
```
minikube tunnel
```

## Review the app

Open minikube dashboard and see if deployments succeeded. Run in shell 2:
```
minikube dashboard
```

Check the frontend in browser: `http://localhost:5100`

Check the backend in browser: `http://localhost:5200/msg/`
