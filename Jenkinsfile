pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Service
        metadata:
          name: helloworld
          labels:
            app: helloworld
        spec:
          ports:
          - name: http
            port: 8000
            targetPort: 8000
          selector:
            app: helloworld
          type: LoadBalancer
---
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: helloworld
          labels:
            app: helloworld
        spec:
         replicas: 1
         selector:
           matchLabels:
             app: helloworld
         template:
           metadata:
             labels:
               app: helloworld
         spec:
           containers:
           - name: helloworld
             image: signalsciences/example-helloworld:latest
             imagePullPolicy: IfNotPresent
             args:
            # Address for the app to listen on
            - localhost:8000
            ports:
            - containerPort: 8000
