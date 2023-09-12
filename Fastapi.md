## Quick setup steps

#### Virtual environment:

```shell
pipenv --python 3.9 #create project

pipenv install #install dependencies 

pipenv shell #start virtual env

pipenv install -r requirements.txt #install dependencies from requirements.txt

python main.py #To run FastAPI server
```

[List of usual packages](Fastapi%20Packages.md)
[Git setup](Git%20cheatsheet.md)
_____
#### App.py boilerplate:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}

```
____
#### Main.py boilerplate:

```python
import uvicorn

if __name__ == "__main__":

    uvicorn.run("app:app", host="127.0.0.1", port=8000, reload=True) #Reload app automatically and run with python main.py
```
_________________________

## Database
#### SQL Database.py boilerplate:

```python
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

SQLALCHEMY_DATABASE_URL = "mysql+pymysql//root@localhost:3306/db" #database URL, for sqlite its current directory

engine = create_engine(SQLALCHEMY_DATABASE_URL) #connect_args only for sqlite and make sure no cross thread info sharing

SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine) #db instance
conn = engine.connect()
Base = declarative_base() #exports DB Base class
```

[Detailed SQL operations](SQL%20in%20FastAPI)

#### MongoDB Database.py boilerplate:
```python
from pymongo import MongoClient

CONNECTION_STRING = <mongoURL>
client = MongoClient(CONNECTION_STRING)
db = client['db_name']
collection = db['db_collection']
```

[Detailed MongoDB operations](MongoDB%20with%20mongoose.md)
______________

### Other essential features and libraries:

[OAuth2](OAuth2)
[Pydantic](Pydantic%20Models)
[Dotenv](Dotenv)
[Date Time](Date%20and%20Time%20in%20Python.md)
[Pandas](Pandas.md)
