# E-commerce AI Agent – Day 5

## Memory, Embeddings, Vector Database & Retrieval-Augmented Generation (RAG)

**Project:** E-commerce Customer Support AI Agent
**Workshop:** One Person Company AI Agents Workshop – Level 2 (Single Agent)
**Day:** 5
**Case Study:** TechZone Store (Fictional Electronics E-commerce Store)
**Implementation:** Google Colab

---

## 1. Project Overview

The goal of Day 5 was to improve our AI agent by introducing **memory and Retrieval-Augmented Generation (RAG)**.

Previously, our AI agent could respond to customer questions using its instructions and tools. However, it had limitations:

- It could not reliably remember previous conversations.
- Keeping all business information inside the system prompt becomes expensive as the knowledge base grows.
- It could generate incorrect answers when business information was missing.

To address these problems, we learned about conversation memory, embeddings, vector databases, chunking, and RAG.

For our practical implementation, we adapted the workshop's PDF-based RAG pipeline into an **E-commerce Customer Support AI Agent** for a fictional electronics store called TechZone Store.

The agent retrieves relevant information from an e-commerce knowledge-base PDF and uses it to answer customer questions.

## 2. Objectives

- Understand short-term memory, long-term customer memory, and business knowledge.
- Understand conversation memory using `thread_id` and checkpointers.
- Learn why we should not put all business information inside the system prompt.
- Understand embeddings and semantic similarity.
- Learn how vector databases store and retrieve information.
- Understand document chunking and overlap.
- Implement a PDF-based RAG pipeline.
- Build an e-commerce question-answering prototype.
- Test whether the agent answers correctly without inventing missing information.

## 3. Technologies Used

| Technology            | Purpose                                 |
| --------------------- | --------------------------------------- |
| Python                | Main programming language               |
| Google Colab          | Development environment                 |
| Sentence Transformers | Convert text into embeddings            |
| all-MiniLM-L6-v2      | Generate 384-dimensional embeddings     |
| all-mpnet-base-v2     | Compare 768-dimensional embeddings      |
| FAISS                 | Store and retrieve vector embeddings    |
| PyMuPDF (fitz)        | Extract text from PDF files             |
| Tesseract OCR         | Extract text from image-based PDF pages |
| NumPy                 | Handle numerical vectors                |
| Groq API              | Generate natural-language answers       |
| openai/gpt-oss-20b    | LLM used for answering questions        |

**Workshop concept:** ChromaDB was introduced as a vector database in the main bakery implementation. Our PDF notebook uses FAISS instead. Both support similarity-based retrieval, but their APIs and storage approaches are different.

## 4. Three Types of Memory

### 4.1 Conversation Memory (Short-Term Memory)

Stores the messages exchanged during the current conversation.

**Example:**

- Customer: My name is Ravi.
- Customer: I need a wireless mouse.
- Customer: What is its price?

The agent can use earlier messages to understand the latest question.

### 4.2 Customer Memory (Long-Term Memory)

Stores useful customer information across different conversations.

**Example:**

- Customer name: Ravi
- Preferred products: Wireless accessories
- Previous purchases: Mechanical keyboard

This can help the business provide personalized customer support.

### 4.3 Business Knowledge

Stores information from business documents, such as:

- Product details
- Prices
- Shipping policies
- Return and refund policies
- Frequently asked questions

We implemented this concept using RAG.

## 5. Conversation Memory: Threads and Checkpointers

A checkpointer stores conversation history so that an agent can continue a conversation.

We learned about:

- `InMemorySaver`
- `thread_id`
- Conversation history management

**Example:**

```python
from langgraph.checkpoint.memory import InMemorySaver

agent = create_agent(
    model=llm,
    tools=[...],
    system_prompt=SYSTEM,
    checkpointer=InMemorySaver()
)

def chat(thread_id, text):
    config = {
        "configurable": {
            "thread_id": thread_id
        }
    }

    result = agent.invoke(
        {
            "messages": [
                {"role": "user", "content": text}
            ]
        },
        config
    )

    return result["messages"][-1].content
```

**Important points:**

- Same `thread_id` → continues the same conversation.
- Different `thread_id` → separate conversation history.
- `InMemorySaver` stores information in RAM.
- Restarting the Colab runtime removes the stored conversation history.

## 6. Why Do We Need RAG?

Putting all business information inside the system prompt creates problems:

1. More input tokens are sent with every model request.
2. It increases API costs.
3. It can increase response time.
4. Relevant information becomes harder to identify when documents grow.

**Solution:** Instead of sending the entire document to the LLM, retrieve only the most relevant information and provide it as context.

This approach is called **Retrieval-Augmented Generation (RAG)**.

## 7. Embeddings

An embedding converts text into a numerical vector that represents its semantic meaning.

**Example:**

- "What is the delivery charge?"
- "How much do I need to pay for shipping?"

These questions use different words but have similar meanings.

An embedding model converts them into vectors that can be compared using similarity.

### Embedding models tested

| Model             | Embedding Dimensions |
| ----------------- | -------------------: |
| all-MiniLM-L6-v2  |                  384 |
| all-mpnet-base-v2 |                  768 |

### Code

```python
from sentence_transformers import SentenceTransformer

sentence = "My name is DSP"

Model_1 = SentenceTransformer("all-MiniLM-L6-v2")
Model_2 = SentenceTransformer("all-mpnet-base-v2")

vector_1 = Model_1.encode(sentence)
vector_2 = Model_2.encode(sentence)

print(vector_1.shape)
print(vector_2.shape)
```

**Output:**

```text
(384,)
(768,)
```

**What we understand from the output:**

- The first model represents the sentence using 384 numerical values.
- The second model represents the same sentence using 768 numerical values.
- Both vectors represent the meaning of the same input sentence, but their dimensions differ.

## 8. Vector Database

A vector database stores embeddings and helps retrieve information based on semantic similarity.

In our implementation, we used **FAISS (Facebook AI Similarity Search)**.

The FAISS index helps find the most relevant document chunks for a customer's question.

### Important concepts

- Embedding: numerical representation of text.
- Vector index: structure used to search vectors.
- Similarity search: finds vectors closest to the query vector.
- Top-K retrieval: returns the K most relevant chunks.

We used `IndexFlatIP` with normalized vectors. In this setup, inner product ranking is equivalent to cosine similarity ranking.

## 9. Chunking

Chunking is the process of dividing a large document into smaller text sections.

Why do we need chunking?

- Large documents are difficult to search efficiently.
- Smaller sections help retrieve relevant information.
- Overlap helps preserve context between neighbouring chunks.

### Our implementation

```python
def split_text(text, chunk_size=500, overlap=100):
    chunks = []

    start = 0

    while start < len(text):
        end = start + chunk_size

        chunks.append(text[start:end])

        start += chunk_size - overlap

    return chunks
```

**Parameters:**

- `chunk_size = 500`: Each chunk contains approximately 500 characters.
- `overlap = 100`: Neighbouring chunks share approximately 100 characters.
- Effective movement between chunks = 400 characters.

## 10. Project Implementation: TechZone Store

We replaced the workshop's story-based PDF with an e-commerce knowledge-base PDF.

**Knowledge Base:** TechZone Store – E-commerce Knowledge Base

The PDF contains fictional sample business information.

### Information included

**Business Information**

- Store details
- Customer support timings
- Contact information

**Product Information**

| Product ID | Product Name            | Sample Price |
| ---------- | ----------------------- | -----------: |
| TZ-P101    | Wireless Mouse          |         ₹599 |
| TZ-P102    | Mechanical Keyboard     |       ₹1,499 |
| TZ-P103    | USB-C Hub               |         ₹899 |
| TZ-P104    | Adjustable Laptop Stand |         ₹799 |
| TZ-P105    | 1080p Webcam            |       ₹1,299 |
| TZ-P106    | Bluetooth Headphones    |       ₹1,999 |
| TZ-P107    | Fast Charging Adapter   |         ₹699 |
| TZ-P108    | Braided USB-C Cable     |         ₹249 |

**Shipping Information**

- Shipping charges
- Free shipping conditions
- Estimated delivery time

**Return and Refund Information**

- Return eligibility
- Return conditions
- Refund processing time

**Frequently Asked Questions**

- Product-related questions
- Delivery questions
- Return and refund questions
- Customer support questions

*Note: All store details, product prices, stock figures, and contact information in this knowledge base are fictional sample data for learning purposes.*

## 11. PDF-Based RAG Pipeline

Our implementation follows these steps:

### Step 1: Install Required Libraries

```python
!pip install pymupdf sentence-transformers faiss-cpu openai numpy groq
```

We also installed OCR-related tools for extracting text from scanned PDF pages.

### Step 2: Upload and Read the PDF

We used Google Colab's file upload functionality to upload the e-commerce knowledge-base PDF.

PyMuPDF extracts selectable text from the document.

If a page does not contain a usable text layer, OCR can be used to extract text from its image.

### Step 3: Extract Text

The extracted text is stored in a Python variable for further processing.

We also print the total number of extracted characters and a preview of the document.

### Step 4: Split Text into Chunks

The extracted text is divided into smaller chunks using our `split_text()` function.

Configuration:

```python
chunk_size = 500
overlap = 100
```

### Step 5: Generate Embeddings

We use the `all-MiniLM-L6-v2` model to convert each chunk into a numerical vector.

```python
embeddings = model.encode(
    chunks,
    normalize_embeddings=True
)
```

The embeddings are converted into NumPy `float32` arrays for FAISS.

### Step 6: Store Embeddings in FAISS

```python
import faiss

dimension = embeddings.shape[1]

index = faiss.IndexFlatIP(dimension)

index.add(embeddings)
```

FAISS stores the vectors and allows similarity-based searching.

### Step 7: Retrieve Relevant Information

When a customer asks a question:

1. Convert the question into an embedding using the same model.
2. Search the FAISS index.
3. Retrieve the top 3 most relevant chunks.
4. Pass the retrieved context to the LLM.

### Step 8: Generate the Answer Using Groq

We used Groq with the model:

`openai/gpt-oss-20b`

The LLM receives:

- System instructions
- Retrieved PDF context
- Customer question

The system prompt instructs the LLM to answer only using the retrieved information and avoid inventing facts.

If the required information is unavailable, the agent should clearly say that it is not available in the PDF.

### Step 9: Interactive Question-Answering

We created an interactive loop to ask multiple questions.

The user can continue asking questions until entering:

```text
exit
```

## 12. Overall RAG Architecture

### Document Indexing Flow

```text
E-commerce Knowledge Base PDF
              |
              v
        Extract Text
              |
              v
           Chunking
              |
              v
          Embeddings
              |
              v
         FAISS Index
```

### Customer Query Flow

```text
Customer Question
        |
        v
Question Embedding
        |
        v
FAISS Similarity Search
        |
        v
Retrieve Top 3 Chunks
        |
        v
Combine Context + Question
        |
        v
       Groq LLM
        |
        v
   Generate Answer
        |
        v
 Customer Response
```

**RAG = Retrieval + Augmentation + Generation**

## 13. Testing the E-commerce Agent

We tested the agent with different categories of customer questions.

### Product Information

- What products do you sell?
- What is the price of the wireless mouse?
- What are the features of the USB-C Hub?
- Tell me about the mechanical keyboard.

### Pricing

- How much does a laptop stand cost?
- What is the price of Bluetooth headphones?
- Which product costs ₹899?
- Do you offer any discounts?

### Shipping

- Do you provide free delivery?
- How much is the shipping charge?
- How many days does delivery take?

### Returns and Refunds

- What is your return policy?
- How many days do I have to return a product?
- How long does a refund take?

### Customer Support

- What are your support timings?
- How can I contact customer support?
- What should I do if I receive a damaged product?

### Negative Testing

These questions help check whether the agent avoids hallucinations.

- What is the price of an iPhone 17?
- Do you sell gaming laptops?
- Where is my order ORD1025?
- Has my refund been processed?
- What is the warranty period of the keyboard?

The agent should not invent answers when the PDF does not contain the required information.

## 14. Limitations of the Current Implementation

Our current implementation is a PDF-based RAG question-answering prototype, not yet a complete production e-commerce agent.

| Feature                               | Current Status                       |
| ------------------------------------- | ------------------------------------ |
| Product information                   | Available from PDF                   |
| Sample product prices                 | Available from PDF                   |
| Shipping policies                     | Available from PDF                   |
| Return policies                       | Available from PDF                   |
| Semantic search                       | Implemented using FAISS              |
| PDF text extraction                   | Implemented                          |
| OCR fallback                          | Included                             |
| LLM-based answers                     | Implemented using Groq               |
| Separate customer conversation memory | Not implemented in this PDF notebook |
| Live product inventory                | Not connected                        |
| Live order tracking                   | Not connected                        |
| Order cancellation                    | Not connected                        |
| Real payment/refund status            | Not connected                        |

**Important:** The PDF may contain sample stock quantities, but they are not live inventory. Real order status, inventory, payments, and refunds require database or API integrations.

## 15. Future Improvements

Our long-term goal is to develop an AI automation agency that provides customer-support automation for small and medium-sized e-commerce businesses.

Planned improvements:

1. Integrate conversation memory using LangGraph checkpointers.
2. Assign a separate `thread_id` to every customer.
3. Add customer memory using a persistent database.
4. Connect product information to a live database.
5. Integrate order tracking APIs.
6. Add order enquiry and cancellation tools.
7. Connect the agent with WhatsApp or Telegram.
8. Add ChromaDB or persistent FAISS storage for knowledge retrieval.
9. Create automated evaluation tests and measure the pass rate.
10. Build a complete multi-agent workflow in Day 6 and beyond.

## 16. Key Learnings from Day 5

- Understood three types of memory.
- Learned conversation memory using checkpointers and `thread_id`.
- Understood why large business documents should not always be placed inside system prompts.
- Learned how embeddings represent semantic meaning.
- Compared MiniLM and MPNet embedding dimensions.
- Understood vector databases and similarity search.
- Learned chunking and overlapping techniques.
- Implemented PDF text extraction.
- Built a FAISS vector index.
- Implemented retrieval using the top 3 relevant chunks.
- Connected retrieved context with Groq LLM.
- Adapted a story-based RAG notebook into an e-commerce knowledge assistant.
- Tested the agent using product, shipping, refund, and unsupported questions.

## 17. Conclusion

Day 5 introduced memory and RAG, two important capabilities for building useful AI agents.

We moved from a simple question-answering approach to a system that can retrieve relevant business information before generating an answer.

By adapting the workshop's PDF RAG pipeline into the TechZone Store e-commerce assistant, we learned how these concepts can be applied to real business problems.

**Our next goal is to combine tools, memory, and RAG into a reliable e-commerce customer-support agent that can handle real customer enquiries.**

---

**Project Status:** Day 5 – PDF-based RAG prototype completed as a learning implementation.

**Next:** Day 6 – Level 3: Multi-Agent Systems and LangGraph Workflows.
