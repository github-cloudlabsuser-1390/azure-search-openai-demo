# Backend Requirements Documentation

This document lists the Python package dependencies required by the backend service, as specified in `requirements.txt`.

## How to Use
- Install all dependencies with:
  ```sh
  pip install -r requirements.txt
  ```
- This ensures your environment matches the backend's requirements for development or production.

## Requirements List

Below are the main packages and their pinned versions:

| Package                        | Version     | Notes/Transitive Dependencies                |
|--------------------------------|-------------|----------------------------------------------|
| aiofiles                       | 24.1.0      | Used by prompty, quart                      |
| aiohappyeyeballs               | 2.4.4       | Used by aiohttp                             |
| aiohttp                        | 3.10.11     | Used directly and by msal, kiota-auth, etc. |
| aiosignal                      | 1.3.1       | Used by aiohttp                             |
| annotated-types                | 0.7.0       | Used by pydantic                            |
| anyio                          | 4.4.0       | Used by httpx, openai                       |
| asgiref                        | 3.8.1       | Used by opentelemetry-instrumentation-asgi   |
| attrs                          | 24.2.0      | Used by aiohttp                             |
| azure-ai-documentintelligence  | 1.0.0b4     |                                            |
| azure-cognitiveservices-speech | 1.40.0      |                                            |
| azure-common                   | 1.1.28      | Used by azure-search-documents               |
| azure-core                     | 1.30.2      | Used by many Azure SDKs                      |
| azure-core-tracing-opentelemetry | 1.0.0b11  | Used by azure-monitor-opentelemetry          |
| azure-cosmos                   | 4.9.0       |                                            |
| azure-identity                 | 1.17.1      | Used by msgraph-sdk, etc.                    |
| azure-monitor-opentelemetry    | 1.6.1       |                                            |
| azure-monitor-opentelemetry-exporter | 1.0.0b32 | Used by azure-monitor-opentelemetry        |
| azure-search-documents         | 11.6.0b12   |                                            |
| azure-storage-blob             | 12.22.0     | Used by azure-storage-file-datalake          |
| azure-storage-file-datalake    | 12.16.0     |                                            |
| beautifulsoup4                 | 4.12.3      |                                            |
| blinker                        | 1.8.2       | Used by flask, quart                        |
| certifi                        | 2024.7.4    | Used by httpcore, httpx, requests, etc.      |
| cffi                           | 1.17.0      | Used by cryptography                        |
| charset-normalizer             | 3.3.2       | Used by requests                            |
| click                          | 8.1.7       | Used by flask, prompty, quart, uvicorn      |
| cryptography                   | 44.0.1      | Used by azure-identity, msal, pyjwt, etc.    |
| ...                            | ...         | ... (see full requirements.txt for all)      |

> **Note:** This is a partial list for brevity. The full list, including all transitive dependencies and their usage, is in `requirements.txt`.

## Regenerating requirements.txt
- The file is auto-generated from `requirements.in` using:
  ```sh
  uv pip compile requirements.in -o requirements.txt
  ```
- Do not edit `requirements.txt` directly; update `requirements.in` and recompile.

---
For more details, see the comments in the `requirements.txt` file itself.
