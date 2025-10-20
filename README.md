apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: swiggy
  template:
    metadata:
      labels:
        app: swiggy
    spec:
      containers:
        - name: cont-1
          image: sisi1234/zomota-project:latest
          ports:
            - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: mysvc
spec:
  type: LoadBalancer
  selector:
    app: swiggy
  ports:
    - port: 3000
      targetPort: 3000
