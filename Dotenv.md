
Dotenv is used to create environment variables that store private information/values that you do not want to upload to github or any other hosting location.

#### Create .env file:
```python
VAR_NAME = <value> #raw value without any quotes
```

#### Load .env files:
```python
from dotenv import load_dotenv
import os

load_dotenv()
var = os.getenv("VAR_NAME")
```
```Javascript
var = process.env.VAR_NAME;
```