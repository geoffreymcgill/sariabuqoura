---
icon: workflow
order:1
lable:
---

## Write simple HTTP Get code

- Code
    
    ```python
    from fastapi import FastAPI
    import uvicorn
    import os
    
    app = FastAPI()
    
    @app.get("/hello")
    async def hello(message='test'):
    
        configMapMessage=os.getenv('helloMessage')
        return {configMapMessage:message}
    
    if __name__ == "__main__":
    
        uvicorn.run(app, host="127.0.0.1", port=8080)
    ```
    

## Create Dockerfile

- Requirements.txt
    - File
    
    ```
    fastapi[all]==0.109.0
    uvicorn[standard]==0.27.0
    ```
    
    - Simple Dockerfile
    
    ```docker
    # For more information, please refer to https://aka.ms/vscode-docker-python
    FROM python:3-slim
    
    EXPOSE 8080
    
    # Keeps Python from generating .pyc files in the container
    ENV PYTHONDONTWRITEBYTECODE=1
    
    # Turns off buffering for easier container logging
    ENV PYTHONUNBUFFERED=1
    
    ENV helloMessage="defualt from docker file"
    
    # Install pip requirements
    COPY requirements.txt .
    RUN python -m pip install -r requirements.txt
    
    WORKDIR /app
    COPY . /app
    
    # Creates a non-root user with an explicit UID and adds permission to access the /app folder
    # For more info, please refer to https://aka.ms/vscode-docker-python-configure-containers
    RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
    USER appuser
    
    # During debugging, this entry point will be overridden. For more information, please refer to https://aka.ms/vscode-docker-python-debug
    CMD ["uvicorn","main:app","--host" ,"0.0.0.0", "--port","8080" ]
    
    ```
    
    ## Build the code and dockerfile into docker (Image)
    
    - Command line
        - `docker build -t http_get:v1 .`

## Ymal files

- Deployment
    
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: http-get-simple-deployment-configmap
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: http-get-configmap
      template:
        metadata:
          labels:
            app: http-get-configmap
        spec:
          containers:
            - name: http-get-python-get-configmap
              image: http_get_configmap:v1
              ports:
                - containerPort: 8080
              env:
                - name: helloMessage
                  valueFrom:
                    configMapKeyRef:
                      name: config-http-get
                      key: helloMessage
    ```
    
- Service
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: http-get-simple-service-configmap
    spec:
      selector:
        app: http-get-configmap
      type: LoadBalancer
      ports:
        - port: 8080
          targetPort: 8080
          protocol: TCP
    
    ```
    
- Service
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: http-get-simple-service-configmap
    spec:
      selector:
        app: http-get-configmap
      type: LoadBalancer
      ports:
        - port: 8080
          targetPort: 8080
          protocol: TCP
    
    ```
    

- Config map
    
    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: config-http-get
    data:
      helloMessage : hellllllo from config map 
    ```
    

# Verify

- Command
    - `kubectl get service -o wide`
    - Expected result
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/021f0fb0-2f31-4ac2-91a3-a2d19c9d1319/image.png)
        
- Web Browser
    - `http://localhost:8080/hello`
    - Expected result
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/10312a2b-1fa2-49ed-acdd-32a92cd6099a/image.png)
        

Resources 

- https://hub.docker.com/layers/sariabuqoura/kube_http_get_configmap/v1/images/sha256-7386db9d631062b958f9f6640b19e4bf2b5ac639d9a97499ceaa69daefc15e7d?context=repo
