
## Update Bot Logic

* Update the `if ...elif` section of the `process_incoming_message` function for your new command.  

```
# Some of function removed below
def process_incoming_message(post_data):
    # Take action based on command
    # If no command found, send help
    if command in ["","/help"]:
        reply = send_help(post_data)
    elif command in ["/echo"]:
        reply = send_echo(message)
    elif command in ["/chuck"]: 
        reply = chuck_joke()
	
    send_message_to_room(room_id, reply)	
```

