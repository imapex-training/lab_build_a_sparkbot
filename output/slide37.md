
## Stub in Code for New Feature

Each command has a corresponding function that is called.  Here is the function for the `/echo` command.  

```
def send_echo(incoming):
    # Get sent message
    message = incoming["text"]
    # Slice first 6 characters to remove command
    message = message[6:]
    return message	
```

* Function **must** return the text of the message to be sent
* Passing the `incoming` data is only required if your command needs it

