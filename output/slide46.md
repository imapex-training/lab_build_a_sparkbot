
## Leveraging Cisco Spark in Code

Though we could call the REST APIs for Spark directly with Python, [ciscosparkapi](https://github.com/CiscoDevNet/ciscosparkapi) is a "Simple, lightweight, scalable Python API wrapper for the Cisco Spark APIs".  

### Example
```
from ciscosparkapi import CiscoSparkAPI

api = CiscoSparkAPI()

message = api.messages.create('<room_id>', text='<message_text>')

print("New message created, with ID:", message.id)
print(message.text)
```

