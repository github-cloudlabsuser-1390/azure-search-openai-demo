# Backend App Documentation

This document provides an overview and usage guide for the backend service of the RAG chat app with Azure OpenAI and Azure AI Search.

## Overview

The backend is a Python web service built with [Quart](https://pgjones.gitlab.io/quart/), designed to provide RESTful and streaming endpoints for chat, Q&A, file access, and configuration. It integrates with Azure OpenAI, Azure AI Search, Azure Blob Storage, Cosmos DB, and supports advanced features like authentication, CORS, and Application Insights monitoring.

## Architecture

- **Framework:** Quart (async Flask-compatible)
- **Entrypoint:** `main.py` (loads environment, creates app)
- **App Factory:** `create_app()` in `app.py`
- **Blueprints:** Main API routes and chat history CosmosDB routes
- **Workers:** Gunicorn with custom Uvicorn worker for async support
- **CORS:** Enabled via environment variable `ALLOWED_ORIGIN`
- **Logging:** Configurable via `APP_LOG_LEVEL` and Application Insights

## Key Endpoints

- `POST /ask` — Q&A endpoint (with/without vision)
- `POST /chat` — Chat endpoint (multi-turn, with/without vision)
- `POST /chat/stream` — Streaming chat endpoint
- `GET /config` — Returns backend feature/configuration flags
- `GET /auth_setup` — Returns MSAL.js authentication config
- `GET /content/<path>` — Serves files from blob storage (with access control)
- Static assets: `/assets/<path>`, `/favicon.ico`, `/`

## Features

- **Azure OpenAI**: Chat, Q&A, embeddings, vision (GPT-4V)
- **Azure AI Search**: Document retrieval, hybrid/vector search
- **Blob Storage**: File serving, user uploads
- **Cosmos DB**: Chat history (optional)
- **Authentication**: Azure AD/MSAL (optional)
- **CORS**: Configurable for alternate frontends
- **Application Insights**: Telemetry and logging
- **Speech**: Azure Speech Synthesis (optional)

## Configuration

Configuration is managed via environment variables and the `config.py` constants. Key environment variables:

- `APP_LOG_LEVEL` — Logging level (default: INFO)
- `ALLOWED_ORIGIN` — Semicolon-separated list of allowed CORS origins
- `APPLICATIONINSIGHTS_CONNECTION_STRING` — Enables Azure Monitor
- Azure resource connection strings and keys (see deployment docs)

## Dependencies

All dependencies are listed in `requirements.txt`. Major packages include:
- `quart`, `quart-cors`, `gunicorn`, `uvicorn`
- `azure-cognitiveservices-speech`, `azure-search-documents`, `azure-storage-blob`, `azure-identity`, `azure-cosmos`
- `openai`, `opentelemetry-instrumentation-*`

## Running Locally

1. Install Python 3.11+
2. Install dependencies:
   ```powershell
   pip install -r requirements.txt
   pip install gunicorn
   ```
3. Start the backend:
   ```powershell
   python -m gunicorn -b 0.0.0.0:8000 main:app
   ```
   Or use the provided `start.ps1` script from the root `app` directory.

## Deployment

- **Docker:** See `Dockerfile` for containerized deployment.
- **Azure App Service/Container Apps:** See project-level and `docs/` documentation for cloud deployment instructions.

## Error Handling

Errors are returned as JSON with a descriptive message. See `error.py` for details.

## Customization

- Add/modify endpoints in `app.py`
- Adjust authentication in `core/authentication.py`
- Update configuration in `config.py`

## License

This project is licensed under the MIT License. See the root `LICENSE` file for details.
