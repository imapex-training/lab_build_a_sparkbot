
**Windows Version**

`bot_install_sandbox.ps1`

```
# Part of the Install Script
Write-Output "Installing the Bot as  $docker_username/$bot_name"
Invoke-RestMethod -Method Post \
  -Uri "https://$control_address`:8080/v2/apps" \
  -ContentType "application/json" \
  -InFile "$docker_username-$bot_name-sandbox.json" \
  -Credential $mantl_credential
```

