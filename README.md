# KG-pipe: Building Knowledge Graphs with neo4j-graphrag

A hands-on workshop for building knowledge graphs from unstructured data using the [`neo4j-graphrag`](https://github.com/neo4j/neo4j-graphrag-python) Python package.

## Prerequisites

- Python 3.10+
- A [Neo4j Aura](https://console.neo4j.io) instance (free tier works)
- An [OpenAI API key](https://platform.openai.com/api-keys)

## Setup

1. **Clone and create a virtual environment:**
   ```bash
   git clone https://github.com/henrardo/KG-pipe.git
   cd KG-pipe
   python -m venv .venv
   source .venv/bin/activate
   ```

2. **Install dependencies:**
   ```bash
   pip install "neo4j-graphrag[openai]" python-dotenv jupyterlab aiohttp beautifulsoup4 requests pymupdf
   ```

3. **Create a `.env` file** in the project root:
   ```
   NEO4J_URI=neo4j+s://your-instance.databases.neo4j.io
   NEO4J_USERNAME=neo4j
   NEO4J_PASSWORD=your-password
   NEO4J_DATABASE=neo4j
   OPENAI_API_KEY=sk-your-key
   ```

4. **Add PDFs** to a `data/` folder in the project root (for Notebook 3).

5. **(Optional) Install Tesseract** for OCR support on scanned PDFs:
   ```bash
   brew install tesseract        # macOS
   sudo apt install tesseract-ocr  # Linux
   ```

6. **Launch Jupyter:**
   ```bash
   jupyter lab
   ```

## Notebooks

| # | Notebook | What you'll learn |
|---|----------|-------------------|
| 1 | [Setup & Connection](notebooks/01_setup_and_connection.ipynb) | Install deps, connect to Neo4j & OpenAI |
| 2 | [KG from Text](notebooks/02_kg_from_text.ipynb) | Define a schema, extract entities from plain text |
| 3 | [KG from PDFs](notebooks/03_kg_from_pdf.ipynb) | Extract text with PyMuPDF (+ OCR fallback), build KG |
| 4 | [KG from Web](notebooks/04_kg_from_web.ipynb) | Load remote PDFs, build a custom `DataLoader` for web pages |
| 5 | [Batch API](notebooks/05_kg_batch_api.ipynb) | Use OpenAI Batch API for 50% cheaper KG extraction |

Work through them in order. Each notebook builds on concepts from the previous one.

## Schema Options

Each notebook lets you toggle between two approaches:

- **`USE_MANUAL_SCHEMA = True`** — You define the entity types, relationship types, and patterns. Produces cleaner, more targeted graphs.
- **`USE_MANUAL_SCHEMA = False`** — The LLM reads a sample and proposes its own schema automatically. Useful when you don't know what's in the data.
