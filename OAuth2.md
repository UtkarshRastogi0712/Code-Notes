OAuth2PasswordBearer is an authorization library that can be used to authorize users to perform certain actions based on a JWT bearer token.

### Basic flow:
- User sends Username and Password to a designated URL for authorization
- The URL verifies the credentials and responds back with a JWT token 
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

### Authenticate user:
Steps:
- Check for username supplied in DB
- Verify hashed password with context/hashing key
- Return status
```python
def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)
    
async def get_user(username: str):
    db = await user_db.get_users()
    for user in db:
        if user["username"] == username:
            user_dict = user
            return UserSchema(**user_dict)

async def authenticate_user(username: str, password: str):
    user= await get_user(username)
    if not user:
        return False
    if not verify_password(password, user.hashed_password):
        return False
    return user
```
### Generate Access Token:
Steps:
- Validate user credentials submitted
- Set Data payload to username and set token expiration time
- Encode token using jwt encode
- Define access token type as bearer and return
```python
@app.post("/token", response_model=Token)
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    user = await authenticate_user(form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
        )
    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    access_token = create_access_token(
        data={"sub": user.username},expires_delta=access_token_expires
    )
    return {"access_token": access_token, "token_type": "bearer"}
```

```python
def create_access_token(data: dict, expires_delta: Union[timedelta, None] = None):
    to_encode = data.copy()
    if expires_delta:
        expire = datetime.utcnow() + expires_delta
    else:
        expire = datetime.utcnow() + timedelta(minutes=15)
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt
```

### Get currently active user:
```python
@app.get("/user/me", response_model=UserSchema)
async def read_user(current_user: UserSchema = Depends(get_current_active_user)):
    return current_user
```
- Decode the payload with the context/secret key using the desired cryptography algorithm
- Extract the username from the "sub" data key
- Check for the username in the Database
- Raise credentials exception if credentials dont match Database
- Return "Inactive " if the user is marked as such
```python
async def get_current_user(token: str = Depends(oauth2_scheme)):
    credentials_exception = HTTPException(
            status_code = status.HTTP_401_UNAUTHORIZED,
            detail="Could not validate credentials",
            headers={"WWW-Authenticate":"Bearer"},
        )
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise credentials_exception
        token_data = TokenData(username=username)
    except JWTError:
        raise credentials_exception
    user = await get_user(username=token_data.username)
    if user is None:
        raise credentials_exception
    return user

async def get_current_active_user(current_user: UserSchema = Depends(get_current_user)):
    if current_user.disabled:
        raise HTTPException(status_code=400, detail="Inactive user")
    return current_user
```