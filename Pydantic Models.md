#Python 
Pydantic helps create schema/models for custom datatypes, request/response models and other object based uses. It helps establish seamless and standardised communication with APIs and Databases.

#### Usecase:

```python
from typing import Optional, Union
from pydantic import BaseModel, Field

class UserSchema(BaseModel):
    username: str=Field(..., max_length=40) #Required field with no default value
    full_name: str=Field(...)
    hashed_password: str=Field(...)
    disabled: bool
    description: Optional[str] #optional value of type str
    class Config:
        orm_mode=True #To allow for Object Relationalship Modelling 
        schema_example = { 
            "example": {
                "username": "Valid username",
                "email": "Valid email of the user",
                "full_name": "Full Name of the User",
                "hashed_password": "Encoded password",
                "disabled": False,
            }
        } #For endpoint documentation

```