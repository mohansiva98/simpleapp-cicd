apiVersion: apps/v1
kind: Deployment
metadata:
  name: simpleapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: simpleapp
  template:
    metadata:
      labels:
        app: simpleapp
    spec:
      containers:
      - name: simpleapp
        image: yourdockerhub/simpleapp:v1
        ports:
        - containerPort: 5000

