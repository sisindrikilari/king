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
---

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: petapp-ingress
  namespace: petapp
  annotations:
    kubernetes.io/ingress.class: ALB  # Use ALB Ingress class
    # alb.ingress.kubernetes.io/scheme: internet-facing  # Can be internal or internet-facing
    # alb.ingress.kubernetes.io/target-type: ip  # Use IP-based routing for ALB
    # alb.ingress.kubernetes.io/listen-ports: '[{"HTTP": 80}]'  # Define ALB listener
spec:
  rules:
    - http:
        paths:
          - path: /  # Root path for accessing your service
            pathType: Prefix
            backend:
              service:
                name: mysvc  # Name of the Kubernetes service
                port:
                  number: 3000
