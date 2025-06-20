# 🧠 Local LLM + Web Retrieval Agent

This project demonstrates how to combine **local Large Language Models (LLMs)** with **external web search tools** to build a hybrid AI agent that can:

- Run image and text understanding using local models (via Ollama)
- Retrieve relevant research papers from the web (e.g., from arXiv)
- Automatically call tools from within the LLM using function calling

---

## 🔧 Requirements

Install all required packages:

```bash
pip install ollama tavily-python requests pydantic pymupdf PyPDF2 openai
