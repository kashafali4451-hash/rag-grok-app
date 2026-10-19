# RAG Implementation Using Gemini

FastAPI web app with two modes:
- **Basic Chat**: talks directly to Gemini.
- **RAG Chat**: upload PDF/TXT/MD files, they are chunked, embedded and stored in ChromaDB,
  and Gemini answers using the most relevant chunks.

## Tech
FastAPI, ChromaDB (all-MiniLM-L6-v2 embeddings), Gemini API, HTML/JS UI,
Firebase Hosting + Cloud Run for deployment.

## Run locally
```
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```
Copy `.env.example` to `.env` and add your Gemini key (GEMINI_API_KEY), then:
```
uvicorn main:app --reload
```
Open http://127.0.0.1:8000

## API
- `POST /api/chat`: basic chat
- `POST /api/upload`: upload a document for RAG
- `POST /api/rag-chat`: ask questions about uploaded documents
- `GET /api/status`, `DELETE /api/documents`

## Deploy (Firebase Hosting + Cloud Run)
```
gcloud run deploy rag-grok --source . --region us-central1 --allow-unauthenticated --memory 1Gi --set-env-vars GEMINI_API_KEY=YOUR_KEY
firebase deploy --only hosting
```
