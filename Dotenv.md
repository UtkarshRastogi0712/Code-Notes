#Generic
Dotenv is used to create environment variables that store private information/values that you do not want to upload to github or any other hosting location.

#### Create .env file:
```python
VAR_NAME = <value> #raw value without any quotes
```

#### Load .env files:
##### Python:
```python
from dotenv import load_dotenv
import os

load_dotenv()
var = os.getenv("VAR_NAME")
```

##### JS:
```Javascript
require('dotenv').config()

var VAR_NAME = process.env.VAR_NAME
```
