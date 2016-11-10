
## bot.py: Taking Action

```
# Function to take action on incoming message
def process_incoming_message(post_data):
    # Determine the Spark Room to send reply to
    room_id = post_data["data"]["roomId"]

    # Get the details about the message that was sent.
    message_id = post_data["data"]["id"]
    message = spark.messages.get(message_id)

    # First make sure not processing a message from the bot
    if message.personEmail in spark.people.me().emails:
        return ""

    # Log details on message
    sys.stderr.write("Message from: " + message.personEmail + "\n")

    # Find the command that was sent, if any
    command = ""
    for c in commands.items():
        if message.text.find(c[0]) != -1:
            command = c[0]
            sys.stderr.write("Found command: " + command + "\n")
            # If a command was found, stop looking for others
            break

    reply = ""
    # Take action based on command
    # If no command found, send help
    if command in ["", "/help"]:
        reply = send_help(post_data)
    elif command in ["/echo"]:
        reply = send_echo(message)

    spark.messages.create(roomId=room_id, markdown=reply)

```

