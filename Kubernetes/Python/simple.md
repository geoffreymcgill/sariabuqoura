
icon: static/images/k8.webp


# Write simple HTTP Get code

- Code
    
    ```python
    from fastapi import FastAPI, HTTPException
    import uvicorn
    
    app = FastAPI()
    
    @app.get("/hello")
    async def hello(message='test'):
       
        return {"Hello ":message}
    
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
      name: http-get-simple-deployment
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: http-get
      template:
        metadata:
          labels:
            app: http-get
        spec:
          containers:
            - name: http-get-python-get
              image: http_get:v1
              ports:
                - containerPort: 8080
    
    ```
    
- Service
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: http-get-simple-service
    spec:
      selector:
        app: http-get
      type: LoadBalancer
      ports:
        - port: 8080
          targetPort: 8080
          protocol: TCP
    
    ```
    

# Verify

- Command
    - `kubectl get service -o wide`
    - Expected result
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/f105e080-2d9f-4a49-bef4-19d921a37364/image.png)
        
- Web Browser
    - `http://localhost:8080/hello`
    - Expected result
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/7b30c098-5958-4470-9fb1-da24a75cd1d0/image.png)
