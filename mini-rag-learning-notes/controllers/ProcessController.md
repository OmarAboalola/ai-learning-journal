# ProcessController.py

---

## Comment 1

### Comment

```python
# according to the documentation, TextLoader needs a file path to work
```

### Code

```python
if file_ext == ProcessingEnum.TXT.value:
    return TextLoader(file_path, encoding="utf-8")
```

---

## Comment 2

### Comment

```python
# returns a list of Document objects,
# each containing the content of the file
```

### Code

```python
def get_file_content(self, file_id: str):
    file_loader = self.get_file_loader(file_id=file_id)
    return file_loader.load()
```

---

## Comment 3

### Comment

```python
# split the document into smaller chunks
```

### Code

```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=chunk_size,
    chunk_overlap=chunk_overlap,
    length_function=len,
)
```

---

## Comment 4

### Comment

```python
# extract only the text from each document
```

### Code

```python
file_content_texts = [
    record.page_content
    for record in file_content
]
```

---

## Comment 5

### Comment

```python
# keep the metadata for every document
```

### Code

```python
file_content_metadata = [
    record.metadata
    for record in file_content
]
```

---

## Comment 6

### Comment

```python
# returns a list of documents, each containing one chunk.
# the size of each chunk is set by chunk_size,
# and the overlap between chunks by chunk_overlap
```

### Code

```python
chunks = text_splitter.create_documents(
    file_content_texts,
    metadatas=file_content_metadata
)

return chunks
```
