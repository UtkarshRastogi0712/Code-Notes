#Python 
### datetime library

The library datetime is a standard library of python that provides standard date, time, timestamp and combines datetime support in python via specialised objects.
#### Usecase:

```python
from datetime import datetime, date, time, timestamp, timedelta, timezone
DateTime = datetime(year, month, day, hour, minute, second)
Date = date(year, month, day)
Time = time(hour, minute, second)

Current_datetime = datetime.now()
Current_date = date.today()
Current_time = time.localtime()
Current_utc_1 = datetime.utcnow() 
Current_utc_2 = datetime.now(timezone.utc) 

format_datetime = strftime(sample_date, "%Y-%d-%m %H:%M:%S")
parse_datetime = strptime('2019-08-09 01:01:01', "%Y-%m-%d %H:%M:%S")

timestamp_in_seconds = datetime.timestamp(Current_datetime)
datetime_from_timestamp = datetime.fromtimestamp(timestamp_in_seconds)

time_math = Current_datetime - timedelta(years=1)
total_seconds = time_math.total_seconds()

day_of_week = Current_datetime.weekday()

datetime_use = datetime.combine(Current_datetime.date(), Current_datetime.time())

```
_________________________

### pytz library

Python timezone support is extended by pytz to convert between timezones

#### Usecase:

```python
def convert_timezone(timestamp, timezone):
    target_timezone = None
    try:
        target_timezone = pytz.timezone(timezone)
    except:
        target_timezone = pytz.timezone('UTC')
    source_timezone = pytz.timezone('UTC')
    target_date = source_timezone.localize(timestamp).astimezone(target_timezone)
    return target_date
```
_______
