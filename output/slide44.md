
## bot.py Manages WebHooks Automatically

```
# Function to Setup the WebHook for the bot
def setup_webhook(name, targeturl):
    # Get a list of current webhooks
    webhooks = spark.webhooks.list()

    # Look for a Webhook for this bot_name
    try:
        for h in webhooks:  # Efficiently iterates through returned objects
            if h.name == name:
                sys.stderr.write("Found existing webhook.  Updating it.\n")
                wh = spark.webhooks.update(webhookId=h.id, 
                                           name=name, 
                                           targetUrl=targeturl)
                # Stop searching
                break
        # If there wasn't a Webhook found
        if wh is None:
            sys.stderr.write("Creating new webhook.\n")
            wh = spark.webhooks.create(name=name, 
                                       targetUrl=targeturl, 
                                       resource="messages", 
                                       event="created")
    except:
        sys.stderr.write("Creating new webhook.\n")
        wh = spark.webhooks.create(name=name, 
                                   targetUrl=targeturl, 
                                   resource="messages", 
                                   event="created")

    return wh
```

