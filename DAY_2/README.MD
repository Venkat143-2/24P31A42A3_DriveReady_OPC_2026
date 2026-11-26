# Day 2 – Building an E-commerce AI Assistant

**One Person Company – AI Agents Workshop 2026**  
**Project:** EcomAgent AI  
**Focus:** Python Functions, Product Catalogue, LLM Integration, Prompt Engineering & Logging

---

## 📌 Overview

Day 2 focused on applying Python fundamentals and Large Language Models (LLMs) to build an AI-powered e-commerce assistant.

As part of this learning journey, I implemented **EcomAgent AI**, a prototype designed to help small e-commerce businesses automate product-related customer enquiries.

The assistant retrieves product information, answers customer questions, checks size availability, and provides relevant product details using Python functions and an LLM.

## 🎯 Learning Objectives

- Understand how to connect Python applications with Groq API.
- Integrate Large Language Models using LangChain.
- Store and manage product information using Python data structures.
- Implement reusable Python functions.
- Understand decorators and function logging.
- Design effective system prompts.
- Retrieve product information dynamically.
- Validate product size and stock availability.
- Generate AI responses using retrieved product information.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Google Colab | Development environment |
| Groq API | LLM inference |
| GPT-OSS-120B | Language model |
| LangChain | LLM integration |
| JSON / Python dictionaries | Product data management |

## 🏗️ Project Architecture

```text
                 Customer
                    |
                    v
             EcomAgent AI
                    |
                    v
             Customer Query
                    |
                    v
            Product Search
                    |
                    v
             Product Catalogue
                    |
                    v
           Product Information
                    |
                    v
             Groq LLM (GPT-OSS)
                    |
                    v
             AI-generated Answer
                    |
                    v
                Customer
```

## ⚙️ Core Functionalities

### 1. Product Catalogue

Created a product catalogue using a list of Python dictionaries.

Each product contains:

- Product ID
- Product name
- Category
- Color
- Price
- Available sizes
- Stock quantity

### 2. Product Search

Implemented `search_product()` to retrieve products using their names.

### 3. Product Information Formatting

Implemented `format_product()` to convert product dictionary data into readable information.

### 4. AI Product Enquiries

Implemented `ask_product()` to send customer questions and retrieved product information to the LLM.

The assistant generates responses based on the supplied catalogue information.

### 5. Size Availability

Implemented `check_size()` to verify whether a requested size is available for a product.

### 6. Logging Decorator

Implemented `log_call()` using Python decorators to monitor function execution and display function results.

## 📂 Project Structure

```text
EcomAgent-AI/
│
├── Day-02/
│   ├── README.md
│   └── EcomAgent_Day2.ipynb
│
└── README.md
```

## 🧠 Key Concepts Learned

| Concept | Application |
|---|---|
| Lists and Dictionaries | Product catalogue |
| Functions | Product operations |
| Decorators | Function logging |
| String Formatting | Product information display |
| Prompt Engineering | AI response instructions |
| Groq API | LLM communication |
| LangChain | Model integration |
| Conditional Statements | Size and stock validation |

## 🚀 Future Improvements

- Integrate a real e-commerce product database.
- Implement order enquiry and order tracking.
- Add customer conversation memory.
- Introduce customer support automation.
- Implement AI tool calling.
- Connect multiple specialized AI agents.
- Integrate the assistant with e-commerce platforms.

## 📖 Key Takeaway

Day 2 helped me understand how Python functions, product data, logging, prompt engineering, and LLM integration can work together to build a practical AI-powered e-commerce assistant.

**The goal is to evolve EcomAgent AI into an intelligent automation solution that helps small e-commerce businesses reduce repetitive customer-support work.**

---

**Project:** EcomAgent AI  
**Workshop:** One Person Company – AI Agents Workshop 2026  
**Developer:** Venkat Lalisetti
