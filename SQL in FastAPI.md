#### Create all the tables (app.py):

```python
models.Base.metadata.drop_all(bind=engine, checkfirst=True) #Removes all previously made tables. Only necessary for frequent schema changes
models.Base.metadata.create_all(bind=engine) #Creates all the tables based on their metadata

def get_db(): #Func to return local session of DB as dependency and close after use
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```
________________________________
#### Declare tables (models.py):

```python 
from sqlalchemy import Column, ForeignKey, Integer, String, DateTime, BigInteger, Time #Datatypes supported
from sqlalchemy.orm import relationship #Builds ORM models for tables (. notation)
from database import Base #Base table

class Data(Base): #Make table class extending Base table
    __tablename__ = "Data" #Table name in the SQL Server
    obj_id = Column(Integer, primary_key=True, autoincrement=True) #Auto increasing primary key
    row = Column(String(64), nullable=False, ForeignKey("<tablename>.<column>")) #Row with properties and foreign key
```
________
#### Simple CRUD (crud.py):

```python
from sqlalchemy.orm import Session #Get the DB session as dependency
import models, schema #Import table structure and pydantic models

def get_all(db: Session, table: str): #Get request
    return db.query(table).all()

def create_report(db: Session, data: schema.Data):
    db_data = models.Data(obj_id = data.obj_id, row = data.row) #Create table row
    db.add(db_data) #Add row to DB
    db.commit() #Commit row to DB and finalise changes
    db.refresh(db_data) #Refresh DB instance with the added row
```
___________________________
