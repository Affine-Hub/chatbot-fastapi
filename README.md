# PDF Chatbot - FastAPI Application with LangChain Integration

FastAPI app with LangChain for PDF upload, vector storage (Chroma), and WebSocket Q&A. Uses **Ollama** locally for embeddings and chat (`mistral`).

**Layout:** flat repo — `main_websocket.py` at the **repository root** (not under `Backend/`).

## Features

- **Upload PDF**: Upload PDF files to the server, which are processed and stored in a vector store.
- **WebSocket Chat**: Real-time question answering using a WebSocket endpoint.
- **Document Retrieval**: Retrieve source documents related to the answered questions.
- **Memory Integration**: Uses conversation history to improve response relevance.

## Requirements

- Python 3.10+ (3.11 recommended if installs fail on 3.12+)
- **[Ollama](https://ollama.com/)** running locally with the **`mistral`** model (`ollama pull mistral`)

## Project structure

```text
pdf-chatbot-fastapi/
├── main_websocket.py   # FastAPI app (run uvicorn from this directory)
├── requirements.txt
├── files/              # uploaded PDFs (created at runtime)
└── vectorstore_db/     # Chroma persistence (created at runtime)
```

## Local run (macOS / Linux)

From the **repo root**:

```bash
cd /path/to/pdf-chatbot-fastapi

python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -r requirements.txt

python -m uvicorn main_websocket:app --host 127.0.0.1 --port 8000 --reload
```

**Windows (PowerShell):**

```powershell
cd pdf-chatbot-fastapi
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -U pip
pip install -r requirements.txt
python -m uvicorn main_websocket:app --host 127.0.0.1 --port 8000 --reload
```

Alternative (no reload):

```bash
python main_websocket.py
```

### Verify

| URL | Purpose |
|-----|---------|
| `http://127.0.0.1:8000/docs` | Swagger UI |
| `http://127.0.0.1:8000/openapi.json` | OpenAPI schema (health checks) |

## Endpoints

- **GET /get_documents/**: Retrieve a list of uploaded documents.
- **POST /upload_pdf/**: Upload a PDF file for processing.
- **WebSocket /ws/chat**: WebSocket endpoint for real-time question answering.

## Example usage

1. Upload a PDF file using `/upload_pdf/`.
2. Connect to `/ws/chat` with a WebSocket client.
3. Send a text message to ask a question and receive streamed answers.

## Technologies used

- **FastAPI**: Web framework for building APIs.
- **LangChain**: Question answering and document retrieval.
- **Chroma**: Document embeddings storage.
- **Ollama**: Local LLM and embeddings (`mistral`).

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE).
