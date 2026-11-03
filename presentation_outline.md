# Solstice Docs Q&A Assistant
## Presentation Outline

### 1. Problem statement

Solstice Learning administrators repeatedly ask Support questions about common tasks and policies, including password resets, report exports, billing, and API limits. The answers already exist in product documentation, but administrators want to ask questions in plain English.

The assistant retrieves answers from the documentation and abstains when it cannot find supporting information. For unsupported questions, it returns the exact response: **“I don't have an answer for that.”**

### 2. Features

- Ask documentation questions in natural language through a web interface, CLI, or REST API.
- Retrieve relevant passages with BM25 keyword search and optional Gemini semantic embeddings.
- Return concise, extractive answers with the source document, confidence score, and supporting excerpt.
- Reject unsupported questions using a query coverage check and confidence threshold.
- Optionally synthesize an answer with an LLM grounded in retrieved documentation.
- List, add, update, and delete documentation articles through the API; add articles through the web interface.
- Run a five-question benchmark evaluation from the CLI or web interface.

### 3. Tech stack

- **Language:** Python
- **Backend API:** FastAPI
- **Web interface:** Streamlit
- **Relational database:** SQLAlchemy with SQLite by default; PostgreSQL can be configured.
- **Retrieval:** BM25, query coverage gate, and optional Gemini embeddings with Qdrant vector search.
- **Optional answer synthesis:** LLM adapter using a strict grounding prompt.
- **Deployment:** Docker and Docker Compose.

### 4. Limitations

- Each question is processed independently; multi-turn conversation memory is not implemented.
- All documents share one index; role-based or permission-based retrieval filters are not implemented.
- Tables and images are ingested as plain text rather than parsed as structured content.
- Without a Gemini API key, retrieval falls back to BM25 keyword search only.
- The current Docker Compose configuration does not persist the SQLite database or Qdrant index in mounted volumes.

### 5. Future work

- Add an unanswered-question queue so documentation owners can identify missing topics.
- Automatically re-index content when documentation changes in sources such as GitHub or Notion.
- Add role-based access controls to document retrieval.
- Improve ingestion of tables and images.
- Configure persistent storage and HTTPS for production deployments.
- Expand the benchmark set and run regression evaluations as documentation or retrieval logic changes.
