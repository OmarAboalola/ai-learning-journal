# Vector Databases

There are two types of vector databases:

- **Engine-based** — you need to install and run an engine for it to work.
- **File-based** — once the app closes, the stored data just sits as a file on disk. No URL involved, unlike MongoDB.

Qdrant is file-based, but during initialization you still get a URL. That URL isn't for an engine — it's just used for Docker, so don't let it trick you into thinking Qdrant needs one running in the background.

in the Qdrant DB provider file, why do we iterate through the metadata even when it's `None`?
-Because insert_many zips texts, vectors, metadata, and record_ids together positionally (line 160–165) to build one Record per item. zip() needs all four to be the same length and iterable — a bare None isn't iterable and would break the zip (or misalign items if handled some other way).
