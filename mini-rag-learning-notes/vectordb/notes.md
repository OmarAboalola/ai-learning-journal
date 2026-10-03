# Vector Databases

There are two types of vector databases:

- **Engine-based:** you need to install and run an engine for it to work.
- **File-based:** once the app closes, the stored data just sits as a file on disk. No URL involved, unlike MongoDB.

Qdrant supports both modes. In local mode it stores data in a folder on disk and needs no running server. In server mode it runs as a separate engine (for example in Docker) and is reached through a URL. This project uses local mode: the client is created with `QdrantClient(path=...)`.

### Why does the Qdrant provider iterate over metadata even when it is `None`?

`insert_many` zips `texts`, `vectors`, `metadata`, and `record_ids` together by position to build one record per item. `zip()` needs all four to be iterables of the same length, and a bare `None` isn't iterable. So when no metadata is passed, the code replaces it with a list of `None` values, one per text, so the items stay aligned.
