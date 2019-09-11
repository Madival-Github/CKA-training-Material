## Exposing a deployment through service

1.  Use the following sample deployment:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: app1
    spec:
        replicas: 3
        selector:
            matchLabels:
                app: app1
    template:
        metadata:
        labels:
            app: app1
        spec:
            containers:
            - name: app1
                image: mahendrshinde/hostname:node
                resources:
                    limits:
                        memory: "128Mi"
                        cpu: "500m"
                    ports:
                - containerPort: 3000
    ```
2.  Deploy and verify the deployment.

    ```console
    $ kubectl apply -f deploy-app.yaml
    $ kubectl get deploy
    $ kubectl get rs -l app=app1
    ```
  
3.  Create a service definition for above deployment.

    ```console
    $ kubectl apply -f service-1.yaml
    # view the service
    $ kubectl get svc app1-svc
    # view the endpoints
    $ kubectl get ep app1-svc 
    ```

4.  try opening web browser and visiting url `http://localhost:8080`. If you open two diffrent browsers, you should get different hostname (pod name) as an output.