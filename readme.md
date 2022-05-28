# Flask Kubernetes

## Preparation

[Install docker](https://dev.solita.fi/2021/12/21/docker-on-wsl2-without-docker-desktop.html)

[Install minikube](https://minikube.sigs.k8s.io/docs/start/)

Run
```
minikube start
```

## Flask containers

Run
```
eval $(minikube docker-env)
docker build -t flask-frontend -f frontend/Dockerfile ./frontend
docker build -t flask-backend -f backend/Dockerfile ./backend
docker image prune -f
minikube image load flask-frontend:latest
minikube image load flask-backend:latest
kubectl delete deploy flask-deployment
kubectl create -f ./k8s_deployment.yml
kubectl delete service flask-services
kubectl create -f ./k8s_service.yml
kubectl get services
minikube tunnel
```

## Review the app

Open minikube dashboard and see if deployments succeeded. Run in a new terminal:
```
minikube dashboard
```

Check the frontend in browser: `http://localhost:5100`

Check the backend in browser: `http://localhost:5200/msg/`