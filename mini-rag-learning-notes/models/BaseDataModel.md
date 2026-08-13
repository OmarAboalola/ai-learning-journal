> These notes document the project's original MongoDB/Motor implementation, before I migrated to PostgreSQL/SQLAlchemy. Kept here as a record of what I learned at that stage.

# BaseDataModel.py

---

## Comment 1

###  Comment

```python
# initialize the db client so every child class can use it
# without having to create a new instance
```

### Code

```python
class BaseDataModel:
    def __init__(self, db_client):
        self.db_client = db_client
        self.app_settings = get_settings()
```

---

## Comment 2

###  Comment

```python
# load the project settings once
```

### Code

```python
self.app_settings = get_settings()
```
