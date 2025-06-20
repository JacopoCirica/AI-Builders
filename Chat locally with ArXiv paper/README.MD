🧠 Local LLM + Web Retrieval Agent
This Jupyter notebook demonstrates how to combine local Large Language Models (LLMs) with external search tools to build a hybrid AI agent that can:

Run image and text understanding using models like gemma, llava, and qwen

Retrieve up-to-date research paper links from the web (e.g., from arXiv)

Automatically call tools (like get_url) from within the chat model

🔧 Requirements
The notebook installs the following Python packages:

ollama — run LLMs locally

tavily-python — search the web via Tavily API

requests, pydantic, pymupdf, PyPDF2, openai — supporting utilities

bash
Copy
Edit
pip install ollama tavily-python requests pydantic pymupdf PyPDF2 openai
🚀 Features
1. Local LLM Execution
Downloads and uses the following models with Ollama:

gemma3:4b

llava:latest (multimodal vision)

qwen3:4b

python
Copy
Edit
ollama.pull('gemma3:4b')
ollama.pull('llava:latest')
ollama.pull('qwen3:4b')
2. Image Understanding
LLMs are prompted with both text and local image files for visual description.

python
Copy
Edit
stream = ollama.chat(
    model='gemma3:4b',
    messages=[{
        'role': 'user',
        'content': "Can you describe this image?",
        'images': ['<path-to-image>.png']
    }],
    stream=True,
)
3. Web Tool Calling via Tavily
A function get_url() is defined that retrieves the top arXiv paper for a given topic using Tavily API:

python
Copy
Edit
def get_url(topic: str):
    ...
The LLM can automatically call this function when asked a relevant question thanks to tools=[] support in Ollama.

📂 Project Structure
css
Copy
Edit
ollama.ipynb    ← Main notebook
<images/>       ← Place image files you want to analyze
🧪 Example Use Case
Ask: “Can you tell me the main paper about this topic: Mamba Architecture?”

The LLM will:

Recognize this requires a web search

Call get_url("Mamba Architecture")

Return the top relevant arXiv URL

🔐 Notes
Make sure you have a valid Tavily API key

You must have Ollama installed and running

Let me know if you want a version with images or badges (e.g., Python version, Colab launch button). 










