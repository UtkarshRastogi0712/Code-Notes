OAuth2PasswordBearer is an authorization library that can be used to authorize users to perform certain actions based on a JWT bearer token.

### Basic flow:
- User sends Username and Password to a designated URL for authorization
- The URL verifies the credentials and responds back a JWT token 
- The frontend can store the token with an expiration time
- Next time the frontend requires authorization, it can just use the token for the same

### User Model:
We need a pydantic user model to store in our database of choice and provide input validation for all user auth functions that need the specific input as part of a request body.

Example model:

```python
from typing import Optional, Union
from pydantic import BaseModel, EmailStr, Field

class UserSchema(BaseModel):
    username: str=Field(...)
    email: str=Field(...)
    full_name: str=Field(...)
    hashed_password: str=Field(...)
    disabled: bool
    
    class Config:
        orm_mode=True
        schema_example = {
            "example": {
                "username": "Valid username",
                "email": "Valid email of the user",
                "full_name": "Full Name of the User",
                "hashed_password": "Encoded password",
                "disabled": False,
            }
        }
```

### App.py boilerplate:

```python
from fastapi import Depends, FastAPI
from fastapi.security import OAuth2PasswordBearer

app = FastAPI()
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/")
async def root(token: str = Depends(oauth2_scheme)):
    return {"message": "Hello World", "token": token}
```