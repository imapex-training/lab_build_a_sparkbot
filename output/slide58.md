
## Deploying the Application Definition via API

`bot_install_sandbox.sh`

```
# Part of the Install Script
echo "Installing the Bot as  $docker_username/$bot_name"

curl -k -X POST \
    -u $mantl_user:$mantl_password \
    https://$control_address:8080/v2/apps \
    -H "Content-type: application/json" \
    -d @$docker_username-$bot_name-sandbox.json
```

