# Day 3 – Building Conversational E-commerce AI with LangChain

**One Person Company – AI Agents Workshop 2026**  
**Project:** EcomAgent AI  
**Focus:** LangChain, Prompt Templates, Conversation Memory, Automated Testing & AI Agents

---

## 📌 Overview

Day 3 focused on building conversational AI applications using LangChain and Large Language Models (LLMs).

As part of this learning journey, I continued developing **EcomAgent AI**, an AI-powered shopping assistant designed to help small e-commerce businesses automate repetitive customer enquiries.

The implementation uses LangChain to structure prompts, maintain conversation history, generate product-related responses, evaluate AI outputs, and initialize an AI agent.

## 🎯 Learning Objectives

- Understand LangChain architecture and its components.
- Connect Groq LLMs using `ChatGroq`.
- Create structured prompts using `ChatPromptTemplate`.
- Understand `MessagesPlaceholder` for conversation history.
- Maintain conversational context using chat history.
- Build LangChain chains using the LCEL pipe operator.
- Convert LLM responses into strings using `StrOutputParser`.
- Perform basic automated testing using CSV files.
- Initialize AI agents using `create_agent()`.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Google Colab | Development environment |
| LangChain | LLM application framework |
| LangChain-Groq | Groq integration |
| GPT-OSS-120B | Language model |
| CSV | Test case storage |
| JSON | Product catalogue representation |

## 🏗️ Project Architecture

```text
                 Customer
                    |
                    v
              EcomAgent AI
                    |
                    v
             Customer Question
                    |
                    v
             ChatPromptTemplate
                    |
                    v
             Conversation History
                    |
                    v
                LangChain
                    |
                    v
              Groq LLM
                    |
                    v
             AI-generated Answer
                    |
                    v
                 Customer
```

## ⚙️ Core Implementations

### 1. Groq LLM Integration

Connected the Groq API using LangChain's `ChatGroq` class and configured GPT-OSS-120B as the language model.

### 2. Prompt Engineering

Created a structured system prompt defining the EcomAgent AI assistant's role, product catalogue, business rules, and response format.

### 3. ChatPromptTemplate

Used `ChatPromptTemplate.from_messages()` to organize system instructions, conversation history, and customer questions.

### 4. Conversation Memory

Implemented a conversation history mechanism using `MessagesPlaceholder` and a Python list.

The assistant can use previous messages to maintain conversational context, such as remembering a customer's name.

### 5. LangChain Expression Language (LCEL)

Created an LLM processing chain using:

```python
chain = prompt | llm | StrOutputParser()
```

This connects the prompt, language model, and output parser into a single execution pipeline.

### 6. Automated Testing

Created a CSV-based testing mechanism to evaluate chatbot responses.

The testing function checks whether generated answers contain expected keywords.

Implemented:

- CSV test case creation.
- Reading test questions.
- Generating AI responses.
- Checking expected keywords.
- Calculating the test pass percentage.

### 7. AI Agent Initialization

Initialized an AI agent using LangChain's `create_agent()`.

At this stage, the agent uses an empty tools list (`tools=[]`). Tool integration is a future development step.

## 📂 Project Structure

```text
EcomAgent-AI/
│
├── Day-02/
│   ├── README.md
│   └── EcomAgent_Day2.ipynb
│
├── Day-03/
│   ├── README.md
│   └── EcomAgent_Day3.ipynb
│
└── README.md
```

## 🧠 Key Concepts Learned

| Concept | Application |
|---|---|
| ChatGroq | Connect to Groq LLM |
| ChatPromptTemplate | Structure prompts |
| MessagesPlaceholder | Insert conversation history |
| StrOutputParser | Extract text responses |
| LCEL | Connect LangChain components |
| Conversation History | Maintain context |
| CSV Testing | Evaluate chatbot responses |
| create_agent() | Initialize an AI agent |

## 🚀 Future Improvements

- Integrate Python product-search functions as AI tools.
- Implement order-status tracking.
- Add customer-support automation.
- Introduce persistent conversation memory.
- Implement tool calling and decision-making.
- Connect multiple specialized AI agents.
- Integrate with real e-commerce platforms.

## 📖 Key Takeaway

Day 3 helped me understand how LangChain simplifies the development of conversational AI applications.

I learned how to combine prompt templates, conversation history, LLMs, output parsers, and automated testing to build a structured AI-powered e-commerce assistant.

**The ultimate goal is to evolve EcomAgent AI into an intelligent automation solution that helps small e-commerce businesses reduce repetitive customer-support tasks and improve customer experiences.**

---

**Project:** EcomAgent AI  
**Workshop:** One Person Company – AI Agents Workshop 2026  
**Developer:** Venkat Lalisetti
