> These notes document the project's original MongoDB/Motor implementation, before I migrated to PostgreSQL/SQLAlchemy. Kept here as a record of what I learned at that stage.

# ChunkModel.py

---

## Comment 1

### Comment

```python
# used to convert the project_id from a string into an ObjectId for MongoDB queries
```

### Code

```python
from bson.objectid import ObjectId
```

---

## Comment 2

### Comment

```python
# inherit all the shared database helper functions from BaseDataModel
```

### Code

```python
class DataChunkModel(BaseDataModel):
    def __init__(self, db_client):
        super().__init__(db_client=db_client)
```

---

## Comment 3

### Comment

```python
# connect to the chunks collection
```

### Code

```python
self.collection = self.db_client[
    COLLECTION_CHUNK_NAME.value
]
```

---

## Comment 4

### Comment

```python
# insert a single chunk into the database
```

### Code

```python
def create_chunk(self, chunk: DataChunk):
    result = self.collection.insert_one(chunk.dict())
    chunk._id = result.inserted_id
    return chunk
```

---

## Comment 5

### Comment

```python
# convert the chunk object into a dictionary before inserting
```

### Code

```python
chunk.dict()
```

---

## Comment 6

### Comment

```python
# save the generated MongoDB id back onto the object
```

### Code

```python
chunk._id = result.inserted_id
```

---

## Comment 7

### Comment

```python
# insert multiple chunks at once
```

### Code

```python
async def create_chunks(self, chunks: DataChunk):
    result = await self.collection.insert_many(chunk.dict())
    chunk._id = result.inserted_id
    return chunks
```

---

## Comment 8

### Comment

```python
# get all chunks that belong to a project
```

### Code

```python
def get_chunks_by_project_id(self, project_id: str):
```

---

## Comment 9

### Comment

```python
# this chunk belongs to a specific project, so we store the
# project_id as a foreign key pointing to the project table
```

### Code

```python
chunk_project_id: ObjectId
```
