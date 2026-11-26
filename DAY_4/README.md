# Day 4 – Tools, Structured Output and Google Sheets

**AI Agents Workshop | Level 2 – Single Agent | Day 4**

## 📌 Overview

Day 4 focuses on giving AI agents the ability to interact with external systems using tools, validate structured information using Pydantic, and store business data in Google Sheets.

In the previous session, the AI assistant could only respond using the information available in its prompt. On Day 4, the assistant becomes more capable by using Python functions to retrieve product information, check order status, access store policies, and save customer support requests.

**Case Study:** E-commerce Customer Support Agent

**Environment:** Google Colab

**LLM Provider:** Groq

**Model:** `openai/gpt-oss-20b`

## 🎯 Learning Objectives

By completing Day 4, I learned:

- Why AI agents need tools to interact with external systems.
- How function calling works in an AI agent.
- How to create tools using LangChain's `@tool` decorator.
- How to build agents using `create_agent()`.
- How to handle API rate limits and errors.
- How to validate structured data using Pydantic.
- How to integrate Google Sheets using `gspread`.
- How to save customer support requests automatically.

## 📚 Topics Covered

### 1. Why Agents Need Tools

An LLM can generate responses using its learned knowledge and provided context, but it cannot independently access live business information or perform external actions.

Tools allow agents to:
- Retrieve current product prices and stock.
- Check order status.
- Access business policies.
- Save customer support requests.

### 2. How Function Calling Works

Function calling allows an LLM to request the execution of a particular Python function.

**Workflow:**

1. The user sends a query.
2. The model identifies the required tool.
3. The model generates a tool call with arguments.
4. Python executes the requested function.
5. The tool result is returned to the model.
6. The model generates the final response.

### 3. Writing Good Tools with `@tool`

LangChain provides the `@tool` decorator to convert normal Python functions into tools that an AI agent can use.

Important practices:
- Use meaningful snake_case function names.
- Add type hints to function parameters.
- Write clear docstrings.
- Give each tool one responsibility.
- Handle invalid inputs with helpful messages.

### 4. Building an Agent with `create_agent()`

The `create_agent()` function combines:
- An LLM.
- A collection of tools.
- A system prompt.

The agent decides which tools to call based on the user's request.

Agent execution can be inspected using `pretty_print()` to understand the tool calls, tool results and final response.

### 5. Rate Limits and Tool Errors

API providers impose request and token limits.

**HTTP 429 – Too Many Requests**

Methods to handle rate limits:
- Use individual API keys.
- Reduce unnecessary model calls.
- Configure `max_retries`.
- Use try-except blocks.
- Return polite error messages.

### 6. Structured Output with Pydantic

Pydantic helps define and validate structured data.

In this project, a `SupportRequest` model validates customer support information.

Fields include:
- Customer name
- Email
- Issue type
- Message
- Order ID
- Priority

Pydantic ensures that the extracted information follows the expected structure and data types.

### 7. Google Sheets Integration

Google Sheets is used as a simple database for the e-commerce business.

Libraries and methods:
- `gspread`
- `google.colab.auth`
- `google.auth.default()`
- `gspread.authorize()`
- `append_row()`

The workbook contains four worksheets:

| Worksheet | Purpose |
|---|---|
| Products | Product details, prices and stock |
| Orders | Customer order information |
| Policies | Store policies |
| Support Requests | Customer support tickets |

### 8. Putting Everything Together

The final agent combines tools, structured data validation and Google Sheets integration.

**Workflow:**

Customer Message → AI Agent → Tool Selection → Data Retrieval / Validation → Google Sheets → Customer Response

## 🛠️ Project Implementation

### Project: E-commerce Customer Support Agent

The agent is designed to assist customers with product enquiries, order tracking, store policies and support requests.

**Tools Implemented:**

| Tool | Responsibility |
|---|---|
| `get_product_info()` | Retrieves product price, stock, description and warranty |
| `check_order_status()` | Checks order details using order ID and registered email |
| `get_store_policy()` | Retrieves delivery, return, refund, payment and support policies |
| `log_support_request()` | Validates and saves customer support requests to Google Sheets |

### Technology Stack

- Python
- LangChain
- LangChain Groq
- Groq LLM
- Pydantic
- Google Colab
- Google Sheets
- gspread

## 🧪 Testing

The agent was tested with the following customer queries:

1. What is the price of a wireless mouse?
2. Is the mechanical keyboard available?
3. My order ID is ORD1001 and my email is ravi@gmail.com. Where is my order?
4. What is your refund policy?
5. My name is Ravi, my email is ravi@gmail.com. My order ORD1001 has a delivery problem. Please connect me with customer support.

**Expected Results:**
- Retrieve accurate product information.
- Check order status using both order ID and email.
- Retrieve the correct store policy.
- Create and save customer support tickets.
- Handle missing or invalid information politely.

## 💡 Key Learnings

1. Tools extend the capabilities of LLMs beyond text generation.
2. Function calling connects AI models with Python functions.
3. Clear tool names and docstrings improve tool selection.
4. Agent traces help understand and debug agent execution.
5. Pydantic validates structured information before processing.
6. Google Sheets can act as a simple business database.
7. Tool-based automation reduces repetitive manual work.

## 🚀 Outcome

Successfully developed an AI-powered e-commerce customer support agent that can retrieve product information, track orders, explain store policies and automatically record customer support requests in Google Sheets.

Day 4 helped me understand how to connect an AI agent with external tools and business data, moving from a simple conversational assistant towards a practical business automation system.

---

**Next: Day 5 – Retrieval-Augmented Generation (RAG)**

The next session focuses on enabling agents to search business knowledge and retrieve relevant information instead of storing all business facts directly inside the system prompt.
