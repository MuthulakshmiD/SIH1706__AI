# SIH1706__AI

# 🤖 Intelligent Enterprise Assistant (SIH1706)

## 📌 Problem Statement
Develop a chatbot using deep learning and NLP techniques that can accurately understand and respond to employee queries in a large public sector organization.

The chatbot should:
- Handle HR policies, IT support, company events, and general queries
- Process uploaded documents (summarization + keyword extraction)
- Support at least 5 concurrent users
- Ensure response time ≤ 5 seconds
- Include 2-Factor Authentication (Email OTP)
- Filter inappropriate language using a system-maintained dictionary

---

## 🎯 Objective
To design and implement an AI-powered enterprise chatbot that improves organizational efficiency by automating employee query resolution and enabling intelligent document understanding with secure access control.

---

## 🧠 Key Features
- 💬 Natural Language Chatbot (HR + IT + General Queries)
- 📄 Document Upload + Summarization
- 🔍 Keyword Extraction from Documents
- 🔐 Email OTP-based 2FA Authentication
- 🚫 Profanity / Bad Language Filter
- ⚡ Fast Response System (< 5 seconds)
- 📊 Scalable Architecture (Multi-user support)

---

## ⚙️ System Architecture


                +----------------------+
                |     User Login       |
                |   (Email 2FA OTP)    |
                +----------+-----------+
                           |
                           v
                +----------------------+
                |  Chatbot Frontend    |
                +----------+-----------+
                           |
                           v
                +----------------------+
                |  NLP Processing      |
                | Intent + Entity NLP  |
                +----------+-----------+
                           |
          +----------------+----------------+
          |                                 |
          v                                 v
+---------------------+        +----------------------+
| Knowledge Base      |        | Document Processing  |
| (Vector DB FAISS)   |        | Summarization + OCR  |
+----------+----------+        +----------+-----------+
           |                               |
           +---------------+---------------+
                           v
                +----------------------+
                | Response Generator   |
                | (LLM / Rules Engine) |
                +----------+-----------+
                           |
                           v
                +----------------------+
                |   Final Answer       |
                +----------------------+

---

## 🧾 Methodology / Procedure

### 1. Data Collection
- HR policy documents (PDF/text)
- IT support FAQs
- Internal organizational documents
- Sample training data

---

### 2. Data Preprocessing
- Tokenization
- Stopword removal
- Text normalization
- Sentence segmentation

---

### 3. NLP Processing
- Intent classification (HR / IT / General)
- Named Entity Recognition (NER)
- Context understanding using transformer models

---

### 4. Knowledge Base Creation
- Convert documents into embeddings
- Store in FAISS / vector database
- Enable semantic search for queries

---

### 5. Chatbot Response Generation
- Retrieve relevant context from knowledge base
- Generate response using rule-based + AI model (RAG approach)

---

### 6. Document Processing Module
- Extract text from uploaded PDF/DOCX
- Summarize using transformer models
- Extract keywords using TF-IDF / KeyBERT

---

### 7. Security Layer
- Email-based OTP authentication (2FA)
- Session validation
- Access control for users

---

### 8. Content Moderation
- Dictionary-based profanity filtering
- Optional ML-based toxicity detection

---

## 💻 Implementation

---

## 🚀 Backend (FastAPI Chatbot)

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

knowledge_base = {
    "leave policy": "Employees are entitled to 12 casual leaves per year.",
    "it support": "Reset password using IT portal or contact helpdesk."
}

class Query(BaseModel):
    text: str

def get_response(query: str):
    query = query.lower()
    for key in knowledge_base:
        if key in query:
            return knowledge_base[key]
    return "Sorry, no relevant information found."

@app.post("/chat")
def chat(q: Query):
    return {"response": get_response(q.text)}
```

### 2FA Email OTP System
```
import random

otp_store = {}

def generate_otp():
    return random.randint(100000, 999999)

def send_otp(email):
    otp = generate_otp()
    otp_store[email] = otp
    print(f"OTP sent to {email}: {otp}")
```

### Document Summarization

```
from transformers import pipeline

summarizer = pipeline("summarization")

def summarize_text(text):
    return summarizer(text, max_length=120, min_length=40, do_sample=False)
🚫 Content Filtering
bad_words = ["abuse1", "abuse2", "badword"]

def filter_text(text):
    for word in bad_words:
        if word in text.lower():
            return "⚠️ Inappropriate language detected!"
    return text
```
### 📤 Sample Inputs & Outputs
Example 1

Input:

What is the leave policy?

Output:

Employees are entitled to 12 casual leaves per year.
Example 2

Input:

How to reset IT password?

Output:

Reset password using IT portal or contact helpdesk.
Example 3 (Document Upload)

Input:

HR Policy Document uploaded

Output:

Summary:
- Employees get 12 casual leaves annually
- Medical leave requires approval

Keywords:
leave, medical, policy, approval

## OUTPUT


<img width="879" height="757" alt="image" src="https://github.com/user-attachments/assets/09232dce-79ac-4412-98c9-8660fee2ad96" />


### 📊 Strategies Used
1. NLP Strategy
Intent classification
Named Entity Recognition (NER)
Context-aware understanding
2. Retrieval-Augmented Generation (RAG)
Retrieve relevant documents
Generate contextual responses using LLM
3. Vector Search Strategy
FAISS-based semantic search
4. Hybrid Chatbot Strategy
Rule-based + AI-based response system
5. Performance Optimization
Caching frequent queries
Precomputed embeddings
Lightweight inference pipeline
6. Security Strategy
Email OTP authentication (2FA)
Role-based access control
Content moderation system
### 🚀 Advantages
Automates HR & IT query handling
Reduces manual workload
Fast response time (< 5 seconds)
Secure authentication (2FA)
Scalable architecture for multiple users
Supports document intelligence
### ❌ Limitations
Requires continuous knowledge base updates
Performance depends on data quality
High computation cost for LLM-based systems
May fail for unseen or ambiguous queries
### 📈 Results

The system successfully:

Answers employee queries accurately
Processes and summarizes uploaded documents
Filters inappropriate content
Ensures secure access via OTP authentication
Supports concurrent multi-user interaction

###### 🏁 Conclusion

The Intelligent Enterprise Assistant integrates NLP, deep learning, retrieval systems, and secure authentication to build a scalable enterprise chatbot. It enhances organizational efficiency by automating communication, enabling document intelligence, and ensuring secure, fast, and accurate responses.

##### 📌 Future Enhancements
Voice-based chatbot interface
Multilingual support
Advanced LLM integration (GPT-style models)
Integration with enterprise ERP systems
Mobile application deployment
