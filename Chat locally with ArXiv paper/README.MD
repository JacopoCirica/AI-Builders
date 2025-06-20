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
```

## 🚀 Features
### ✅ Local LLM Execution
Downloads and uses the following models with Ollama:

- gemma3:4b

- llava:latest (for vision tasks)

- qwen3:4b

``` python
ollama.pull('gemma3:4b')
ollama.pull('llava:latest')
ollama.pull('qwen3:4b')
```
---

## 🖼️ Image Understanding
### Uses LLMs to describe local image files:

``` python
stream = ollama.chat(
    model='gemma3:4b',
    messages=[{
        'role': 'user',
        'content': "Can you describe this image?",
        'images': ['<path-to-image>.png']
    }],
    stream=True,
)

for chunk in stream:
    print(chunk['message']['content'], end='', flush=True)
```

---
