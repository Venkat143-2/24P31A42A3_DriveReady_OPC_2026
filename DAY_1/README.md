# EcomAgent AI – E-commerce Customer Support Assistant

## 📌 About the Project

**EcomAgent AI** is a basic AI-powered customer support assistant designed for small e-commerce businesses.

It uses a Large Language Model (LLM) through **Groq** and **LangChain** to respond to common customer enquiries about clothing and fashion products.

The assistant is designed to answer questions politely, use simple English, and avoid making up product information.

## 🎯 Project Objectives

- Build a simple AI customer support assistant.
- Understand how to connect an LLM using LangChain and Groq.
- Create a system prompt that defines the assistant's role and response rules.
- Test the assistant with common e-commerce customer enquiries.
- Explore the use of a prompt-guard model for detecting unsafe or manipulative prompts.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| LangChain | LLM integration and message handling |
| Groq | LLM inference API |
| GPT-OSS 120B | Model used for customer-support responses |
| Meta Llama Prompt Guard 2 22M | Prompt-guard model tested separately |
| Google Colab | Development environment and secret management |

## ⚙️ How It Works

1. Install the required LangChain packages.
2. Import `ChatGroq` and configure the Groq API key.
3. Initialize the `openai/gpt-oss-120b` model with temperature set to `0`.
4. Define a system prompt describing the assistant's role, facts, rules, and response format.
5. Create an `ask()` function to send system and customer messages to the model.
6. Test the assistant with sample product enquiries.
7. Run a separate Prompt Guard API example to explore prompt-injection detection.

## 🧠 Assistant Instructions

The system prompt defines the assistant as **EcomAgent AI**, an assistant for small e-commerce businesses selling clothing and fashion products.

Its main rules are:

- Never invent product prices.
- Never claim that a product is available without checking its stock.
- Never invent discounts or product specifications.
- Clearly communicate when information is unavailable.
- Respond politely in simple English.
- Keep responses under 60 words.
- Use bullet points when listing product details.

## 💬 Example Customer Enquiries

The notebook tests the assistant with these questions:

```text
Hi, what can you help me with?

Do you sell oversized t-shirts?

Can you tell me the price of a hoodie?

Is the black t-shirt available in size L?
```

The model generates responses based on its instructions and the information included in the conversation.

> **Important:** The current notebook does not connect to an actual product catalogue or inventory database. Therefore, it cannot verify real product prices, specifications, or stock availability. The system prompt describes the rules the assistant should follow, but the required catalogue lookup functionality still needs to be implemented.

## 🚀 Getting Started

### 1. Open the Notebook

Open `task1.ipynb` in [Google Colab](https://colab.research.google.com/) or run it in a compatible Python environment.

### 2. Install Dependencies

Run:

```python
!pip install -qU langchain-groq langchain-core groq
```

### 3. Configure the Groq API Key

For Google Colab:

1. Open the **Secrets** tab in the left sidebar.
2. Add a secret named `GROQ_API_KEY`.
3. Paste your Groq API key as its value.
4. Enable notebook access to the secret.

The notebook retrieves the key using:

```python
from google.colab import userdata
import os

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

Never commit your API key to GitHub.

### 4. Initialize the LLM

```python
from langchain_groq import ChatGroq

llm = ChatGroq(
    model="openai/gpt-oss-120b",
    temperature=0
)
```

### 5. Run the Notebook

Execute the notebook cells in order to initialize the model, define the assistant instructions, and test customer enquiries.

## 🛡️ Prompt Guard Experiment

The final notebook cell uses Groq's API with:

```text
meta-llama/llama-prompt-guard-2-22m
```

It submits a sample message that attempts to override previous instructions.

This is a **separate experiment** in the current notebook. Its result is not checked or used to filter messages before they reach the EcomAgent AI assistant.

## 🔮 Future Improvements

- Connect a product catalogue using CSV, JSON, or a database.
- Implement product search by name, category, size, and colour.
- Retrieve live prices and stock availability before responding.
- Add order-status enquiries using an order-management system.
- Integrate Prompt Guard into the customer-message processing workflow.
- Add a web-based chat interface.
- Add human support escalation for unresolved enquiries.
- Add conversation history and customer-context management.

## 📂 Project Structure

```text
EcomAgent-AI/
│
├── task1.ipynb
└── README.md
```

## 📚 Learning Outcomes

Through this project, the key concepts explored are:

- LLM integration with LangChain.
- Connecting to Groq-hosted language models.
- Secure API-key handling with Google Colab Secrets.
- System prompts and role-based AI behaviour.
- Sending user queries to an LLM.
- Testing customer-support use cases.
- Exploring prompt-injection protection with Prompt Guard.

---

**Project:** EcomAgent AI  
**Category:** AI Agents / E-commerce Automation  
**Environment:** Google Colab  
