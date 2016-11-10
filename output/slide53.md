
## Reminder: Building and Publishing a Docker image

```
export BOT_REPO=<GITHUB REPO>
export DOCKER_USER=<DOCKER HUB USERNAME>

    
# Build a Docker image
docker build -t $DOCKER_USER/$BOT_REPO:latest .
docker push $DOCKER_USER/$BOT_REPO:latest
```

