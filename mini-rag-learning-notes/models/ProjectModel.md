> These notes document the project's original MongoDB/Motor implementation, before I migrated to PostgreSQL/SQLAlchemy. Kept here as a record of what I learned at that stage.

# ProjectModel.py

---

## Comment 1

### Comment

```python
# the logic for the project db table lives here.
# this class handles all the db operations related to the project table
```

### Code

```python
class ProjectModel(BaseDataModel):
```

---

## Comment 2

### Comment

```python
# connect to the project collection (table) in the database
```

### Code

```python
self.collection = self.db_client[
    COLLECTION_PROJECT_NAME.value
]
```

---

## Comment 3

### Comment

```python
# CRUD operations on the collection start here
```

### Code

```python
# CRUD methods below
```

---

## Comment 4

### Comment

```python
# insertion function
```

### Code

```python
async def create_project(self, project: Project):
```

---

## Comment 5

### Comment

```python
# async function to insert a project into the collection
```

### Code

```python
async def create_project(self, project: Project):
```

---

## Comment 6

### Comment

```python
# we defined a Project object in db_schemes.py
# (to keep the data shape consistent) and use it here
# to insert a project into the collection
```

### Code

```python
async def create_project(self, project: Project):
```

---

## Comment 7

### Comment

```python
# used Motor (the async MongoDB driver) to insert the project into the collection
```

### Code

```python
result = await self.collection.insert_one(
    project.dict()
)
```

---

## Comment 8

### Comment

```python
# convert the project object to a dictionary
# before inserting it into the collection
```

### Code

```python
project.dict()
```

---

## Comment 9

### Comment

```python
# async function to get a project by id, or create it if it doesn't exist
```

### Code

```python
async def get_project_or_create_one(
    self,
    project_id: str
):
```

---

## Comment 10

### Comment

```python
# convert from a dict (returned by the db) back into a Project object
```

### Code

```python
return Project(**record)
```

---

## Comment 11

### Comment

```python
# never call get_all without pagination
```

### Code

```python
async def get_all_projects(
    self,
    page: int,
    page_size: int
):
```

---

## Comment 12

### Comment

```python
# count all the documents in the collection
```

### Code

```python
total_documets = await self.collection.count_documents({})
```

---

## Comment 13

### Comment

```python
# calculate the total number of pages
```

### Code

```python
total_pages = (total_documets // page_size)
```

---

## Comment 14

### Comment

```python
# round up the total pages if there are remaining documents
```

### Code

```python
if total_documets % page_size > 0:
    total_pages += 1
```

---

## Comment 15

### Comment

```python
# skip the documents from the previous pages and limit the results to one page.
# this doesn't return the data directly — it returns a cursor (a pointer object)
# that you iterate over to get the actual data
```

### Code

```python
cursor = (
    self.collection.find()
    .skip((page - 1) * page_size)
    .limit(page_size)
)
```

---

## Comment 16

### Comment

```python
# the cursor is an async iterator, so we need async for to loop over it
```

### Code

```python
async for document in cursor:
```

---

## Comment 17

### Comment

```python
# convert from dict to a Project object (which requires an id) and append it to the list
```

### Code

```python
projects.append(Project(**document))
```
