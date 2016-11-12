
## bot.py: Code for the WebHook

```
# Entry point for Spark Webhooks
@app.route('/', methods=["POST"])
def process_webhook():
    # Check if the Spark connection has been made
    if spark is None:
        sys.stderr.write("Bot not ready.  \n")
        return "Spark Bot not ready.  "

    post_data = request.get_json(force=True)

    # Take the posted data and send to the processing function
    process_incoming_message(post_data)
    return ""
```

