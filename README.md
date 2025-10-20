apiVersion: apps/v1
kind: Deployment
metadata:
  name: zomotoa  
spec:
  replicas: 1
  selector:
    matchLabels:
      app: zomoto
  template:
    metadata:
      labels:
        app: zomoto
    spec:
      containers:
      - name: Zomoto-1
        image: sisi1234/zomota-project:latest
        ports:
        - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: eks 
spec:
  type: LoadBalancer
  ports:
  - port: 3000
    targetPort: 3000
  selector:
    app: zomoto
