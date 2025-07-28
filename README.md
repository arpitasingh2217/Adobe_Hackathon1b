# Adobe_Hackathon1b
# Persona-Driven Document Intelligence System

## Overview
A sophisticated document analysis system that extracts and prioritizes content based on user personas and specific tasks. Processes multiple PDFs to deliver targeted, relevant information in structured JSON format.

## Technical Specifications

| Category          | Details                  |
|-------------------|-------------------------|
| Platform          | AMD64 (x86_64)          |
| Base Image        | Python 3.9-slim         |
| Architecture      | CPU-only                |
| Network           | Offline operation       |
| Model Size        | ≤1GB                   |
| Processing Time   | ≤60 seconds (3-5 docs)  |
| Max Documents     | 3-10 PDFs              |

## Docker Configuration

### Dockerfile
```dockerfile
FROM --platform=linux/amd64 python:3.9-slim ```

# Install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    libgl1 \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Install Python packages
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy source code
COPY src/ ./src/

# Entrypoint for Round 1B
CMD ["python", "-m", "src.persona_analyzer"]
