
## Add Command Information

Your bot listens for a specific set of commands to act on.  These are stored in a dictionary called `commands`.

* Add new commands to the command dictionary in bot/bot.py 

```
# The list of commands the bot listens for
# Each key in the dictionary is a command
# The value is the help message sent for the command
commands = {
    "/echo": "Reply back with the same message sent.",
    "/help": "Get help.", 
    "/chuck": "Get a random Chuck Norris Joke."
}
```

**Don't forget to add a comma after the entry for `help`**

