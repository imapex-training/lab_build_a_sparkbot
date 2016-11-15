
## Flask

The boilerplate code uses the Flask module as the API application.  Flask is a common and easy to use microframework for creating APIs in Python.  

```
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
```

**More Info: [flask.pocoo.org](http://flask.pocoo.org)**

