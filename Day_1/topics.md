# Day 1 — Creating Your Own AI Chatbot

## Project Overview

Build a basic bakery customer-support chatbot using **Python, LangChain, Groq API, and an existing Large Language Model (LLM)**.

The chatbot is configured to act as the assistant for **Sweet Crumbs Home Bakery**. It receives a customer question, combines it with the chatbot's system instructions, sends the messages to an LLM, and displays the generated response.

> This project connects to an existing model. It does not train an LLM from scratch.

## Topics Covered

### 1. Installing the Required Library
- Installing `langchain_groq` in Google Colab.
- Understanding why an integration package is needed.

### 2. Importing LangChain-Groq
- Importing `ChatGroq` from `langchain_groq`.
- Using `ChatGroq` to connect a LangChain application to a Groq chat model.

### 3. API Key Management
- Importing Python's `os` module.
- Importing `userdata` from `google.colab`.
- Retrieving `GROQ_API_KEY` from Google Colab Secrets.
- Setting the API key as an environment variable.
- Keeping API credentials out of publicly shared code.

### 4. Initializing the LLM
- Creating an LLM client with `ChatGroq`.
- Selecting the model: `openai/gpt-oss-120b`.
- Setting the `temperature` parameter to `0`.

### 5. Temperature
- Understanding temperature as a generation setting.
- Using a low temperature for more predictable responses.
- Recognizing that temperature does not guarantee identical answers.

### 6. System Prompt
- Defining the chatbot's role as the assistant for Sweet Crumbs Home Bakery.
- Providing business facts:
  - The bakery bakes to order.
  - Orders require 24 hours' notice.
  - All cakes have eggless versions.
- Defining response rules:
  - Do not promise delivery times.
  - Say when the answer is not known.
- Defining the response format:
  - Reply politely.
  - Keep the response under 60 words.

### 7. Prompt Engineering
- Writing instructions that guide the LLM's role and behavior.
- Supplying relevant business information in the system prompt.
- Setting constraints for the chatbot's responses.

### 8. Creating the Chatbot Function
- Defining `ask(question)`.
- Accepting a customer question as function input.
- Sending system and human messages to the LLM.
- Returning the generated response text.

### 9. LangChain `invoke()`
- Calling `llm.invoke()` to send messages to the model.
- Understanding that the call returns a model response.

### 10. Chat Message Roles
- `system`: provides the chatbot's instructions.
- `human`: contains the customer's question.

### 11. Extracting the Response
- Accessing `.content` to retrieve the text from the model response.

### 12. Testing the Chatbot
- Calling `ask()` with a sample customer question:
  - `can i get my order tommorrow`
- Displaying the generated answer with `print()`.

### 13. Prompt Injection Demonstration
- Examining an example of a user message that attempts to override previous instructions.
- Understanding the basic idea of a prompt-injection attempt.

### 14. Llama Prompt Guard Demonstration
- Importing `Groq`.
- Creating a Groq client.
- Calling the `meta-llama/llama-prompt-guard-2-22m` model.
- Sending an example suspicious prompt to the Prompt Guard model.
- Printing the model's returned output.

> **Important notebook note:** The Prompt Guard call is a separate demonstration. In this notebook, its result is not checked as a protective step before the bakery chatbot receives a customer's question.

## Technologies and Libraries Used

| Technology / Library | Purpose in this notebook |
|---|---|
| Python | Main programming language |
| Google Colab | Notebook environment |
| `langchain_groq` | LangChain integration for Groq chat models |
| `ChatGroq` | Creates the chat-model connection |
| Groq API | Provides access to the configured model |
| `openai/gpt-oss-120b` | Main chatbot model selected in the notebook |
| `meta-llama/llama-prompt-guard-2-22m` | Model used for the Prompt Guard demonstration |
| `os` | Sets the API key as an environment variable |
| `google.colab.userdata` | Retrieves the API key from Colab Secrets |
| `Groq` | Groq Python client used in the Prompt Guard example |

## Main Code Concepts

| Code | Purpose |
|---|---|
| `!pip install langchain_groq` | Installs the LangChain-Groq package |
| `from langchain_groq import ChatGroq` | Imports the chat-model integration |
| `userdata.get("GROQ_API_KEY")` | Retrieves the saved Colab secret |
| `os.environ["GROQ_API_KEY"]` | Sets the API key in the environment |
| `ChatGroq(model=..., temperature=0)` | Initializes the main chat model |
| `SYSTEM = """..."""` | Stores the chatbot's system instructions |
| `def ask(question):` | Defines the chatbot function |
| `llm.invoke([...])` | Sends the messages to the LLM |
| `.content` | Extracts the response text |
| `print(ask(...))` | Tests and displays a chatbot response |
| `client.chat.completions.create(...)` | Sends a chat-completion request to Prompt Guard |

## Notebook Flow

1. Install the LangChain-Groq package.
2. Import `ChatGroq`.
3. Retrieve the Groq API key from Colab Secrets.
4. Initialize the LLM with the selected model and temperature.
5. Write the bakery chatbot's system prompt.
6. Define the `ask()` function.
7. Test the chatbot with a customer question.
8. Run the separate Llama Prompt Guard demonstration.

## What This Notebook Does Not Implement

The following topics are **not implemented** in this Day 1 notebook:

- Conversation memory or persistent chat history.
- Tool calling or external business-system integration.
- Retrieval-Augmented Generation (RAG).
- Embeddings or vector databases.
- A chatbot frontend or web interface.
- Order creation, inventory checks, or database integration.
- An integrated Prompt Guard check before the main chatbot call.

These can be treated as possible future learning topics, not as completed Day 1 features.

## Day 1 Learning Checklist

- [ ] Install and import `langchain_groq`.
- [ ] Understand the role of `ChatGroq`.
- [ ] Configure the Groq API key using Colab Secrets.
- [ ] Understand the LLM initialization parameters.
- [ ] Understand temperature.
- [ ] Write and explain the system prompt.
- [ ] Understand the `system` and `human` message roles.
- [ ] Explain how `llm.invoke()` works.
- [ ] Explain why `.content` is used.
- [ ] Run and test the bakery chatbot.
- [ ] Understand the prompt-injection example.
- [ ] Explain what the separate Prompt Guard demonstration does and does not do.

## Day 1 Outcome

By the end of this notebook, you should be able to explain how a Python application connects to a Groq-hosted LLM through LangChain, guides its behavior with a system prompt, sends a customer message, and displays the generated response.
