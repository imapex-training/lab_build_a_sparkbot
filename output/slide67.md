
* Build and Push a new Docker Image

```
# If you've opened a new terminal sense setting before
export BOT_REPO=<GITHUB REPO>
export BOT_NAME=<YOUR BOT NAME>
export DOCKER_USER=<DOCKER HUB USERNAME>

    
# Build a Docker image
docker build -t $DOCKER_USER/$BOT_REPO:latest .
docker push $DOCKER_USER/$BOT_REPO:latest
```

