# mini-RAG — Learning Notes

Notes I took while building [mini-rag](https://github.com/OmarAboalola/mini-rag), a production-style RAG backend built on top of the mini-RAG course. Each file breaks a source file down comment by comment — not just what a line does, but why it's there.

This isn't a copy of the course material. It's my own understanding, written up as I worked through the code.

## Structure

- `controllers/` — the request-handling layer: file validation, chunking, project paths.
- `models/` — the original data layer, from the MongoDB/Motor version of the project.
- `vectordb/` — vector database concepts (engine-based vs file-based, Qdrant specifics).
- `llms/` — the Factory pattern used to abstract LLM providers, plus general RAG/LLM notes from later lectures (SQLAlchemy, indexing, migrations, JSONB).

**Heads up:** the `models/` notes document the project's original MongoDB implementation. I later migrated the whole thing to PostgreSQL/SQLAlchemy, so treat those as a snapshot of an earlier version, not the current schema.
