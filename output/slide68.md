
## Sample Function

```
def chuck_joke():
    # Use urllib to get a random joke
    import urllib2
    
    response = urllib2.urlopen('http://api.icndb.com/jokes/random')
    joke = json.loads(response.read())["value"]["joke"]

    # Return the text of the joke
    return joke
```

