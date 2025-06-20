# 🧠 Local LLM + Web Retrieval Agent

This project demonstrates how to combine **local Large Language Models (LLMs)** with **external web search tools** to build a hybrid AI agent that can:

- Run image and text understanding using local models (via Ollama)
- Retrieve relevant research papers from the web (e.g., from arXiv)
- Automatically call tools from within the LLM using function calling

![Chat with Academic Paper](Chat%20locally%20with%20ArXiv%20paper/image_test/Chat_with_academic_paper.png)

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

## 🔗 Web Tool Calling via Tavily
A custom tool (get_url) retrieves the top arXiv research paper for a given topic using the Tavily API:

``` python
def get_url(topic: str):
    tavily_client = TavilyClient(api_key="your-api-key")
    response = tavily_client.search(
        query=f"Tell me the main paper about this topic: {topic}",
        include_domains=["arxiv.org/abs/"],
        search_depth="advanced"
    )
    return response['results'][0]['url']
```

This function is registered as a callable tool and can be automatically triggered by the LLM when using the tools argument.

---

## 🔐 Notes

- You need a valid Tavily API key for search integration.

- Ensure Ollama is installed and running locally to use LLMs.

