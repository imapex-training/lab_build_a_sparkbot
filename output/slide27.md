
* Build the base bot

```
# Set a couple environment variables to make commands easier
# Replace the <NAME> with your data
export BOT_REPO=<GITHUB REPO>
export BOT_NAME=<YOUR BOT NAME>
export DOCKER_USER=<DOCKER HUB USERNAME>
    
# If you aren't in your new Git Repository directory, change into it 
cd $BOT_REPO
    
# Build a Docker image
docker build -t $DOCKER_USER/$BOT_REPO:latest .
```

