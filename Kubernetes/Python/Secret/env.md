---
icon: workflow
label: Env
order: 1
---
## Write simple HTTP Get code

- Code
    
    ```python
    from fastapi import FastAPI
    import uvicorn
    import os
    
    app = FastAPI()
    
    @app.get("/hello")
    async def hello():
    
        secret_key=os.getenv('secret_key')
        return {"key value:":secret_key}
    
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
    
    # Install pip requirements
    COPY requirements.txt .
    RUN python -m pip install -r requirements.txt
    
    WORKDIR /app
    COPY . /app
    
    # Creates a non-root user with an explicit UID and adds permission to access the /app folder
    # For more info, please refer to https://aka.ms/vscode-docker-python-configure-containers
    RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
    USER appuser
    
    ENV secret_key="defualt key value"
    
    # During debugging, this entry point will be overridden. For more information, please refer to https://aka.ms/vscode-docker-python-debug
    CMD ["uvicorn","main:app","--host" ,"0.0.0.0", "--port","8080" ]
    
    ```
    
    ## Build the code and dockerfile into docker (Image)
    
    - Command line
        - `docker build -t http_get_secret:v1 .`

## Ymal files

- Deployment
    
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: http-get-simple-deployment-secret
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: http-get-secret
      template:
        metadata:
          labels:
            app: http-get-secret
        spec:
          containers:
            - name: http-get-python-get-secret
              image: http_get_secret:v1
              ports:
                - containerPort: 8080
              env:
                - name: secret_key
                  valueFrom:
                    secretKeyRef:
                      name: secret-http-get
                      key: secret_key
    ```
    
- Service
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: http-get-simple-service-secret
    spec:
      selector:
        app: http-get-secret
      type: LoadBalancer
      ports:
        - port: 8080
          targetPort: 8080
          protocol: TCP
    
    ```
    
- Secret
    
    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: secret-http-get
    type: Opaque
    data:
      secret_key: c3VwZXJzZWNyZXRhcGlrZXk=  # base64-encoded value of 'supersecretapikey'
    ```
    

# Verify

- Command
    - `kubectl get service -o wide`
    - Expected result
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/feb6e463-18f9-4f92-962c-4fa381ecc75c/image.png)
        
- Web Browser
    - `http://localhost:8080/hello`
    - Expected result
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/7d42bd67-d6af-4ed8-9f72-2c83de395982/image.png)
        

## Resources

- https://hub.docker.com/layers/sariabuqoura/http_get_secret/v1/images/sha256-3bea92cc0af44ddc65f2a3aeda9372fdb4c1c68707f2f6dacab54c02fa110c3c?context=repo
