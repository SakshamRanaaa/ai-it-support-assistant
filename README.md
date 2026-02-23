🧠 Internal IT Support Assistant (RAG)

An internal AI-powered IT support assistant built using Retrieval-Augmented Generation (RAG).
The assistant answers IT, onboarding, warehouse, and security questions only from approved internal documentation, provides citations, and refuses to guess when information is unavailable.

🔍 Problem Statement

IT and operations teams frequently handle:

Repetitive support questions

Manual onboarding queries

Warehouse device troubleshooting

Security-related guidance

Traditional chatbots often hallucinate answers, lack traceability, and create security risks.

✅ Solution Overview

This project implements a safe, ops-ready AI assistant that:

Uses RAG (Retrieval-Augmented Generation) to answer questions strictly from internal knowledge

Provides document-level citations for every response

Explicitly responds with “I don’t know” when information is missing

Logs interactions for AI quality control and auditing

Is designed to support IT, warehouse, onboarding, and security operations

🧩 Key Features

🔒 No Hallucinations
Answers only from indexed internal documents

📚 Source Citations
Every answer includes references like:
[warehouse_sop.md#2]

🚫 Refusal to Guess
Unknown questions are safely rejected

🧾 Audit Logging
All interactions are logged for review

🧠 LLM + Vector Search
OpenAI embeddings + FAISS vector index

ai-it-assistant/
│
├── app/
│   ├── streamlit_app.py     # Chat UI
│   ├── rag.py               # RAG pipeline (chunking, retrieval)
│   ├── prompts.py           # System prompt + safety rules
│   └── logger.py            # Interaction logging
│
├── data/                    # Knowledge base (Markdown)
│   ├── it_faq.md
│   ├── onboarding.md
│   ├── warehouse_sop.md
│   └── security_basics.md
│
├── scripts/
│   └── build_index.py       # Builds FAISS index
│
├── store/                   # Vector index (generated)
├── logs/                    # Chat logs (generated)
│
├── requirements.txt
├── .env.example
└── README.md


📖 Knowledge Base Coverage

The assistant is trained on internal markdown documents covering:

IT FAQ (passwords, VPN, printers, Wi-Fi)

New employee onboarding procedures

Warehouse device & scanner SOPs

Security best practices (phishing, MFA, access control)


⚙️ How It Works (High Level)

Internal documents are chunked and embedded using OpenAI embeddings

Embeddings are stored in a FAISS vector index

User questions are embedded and matched against the index

Relevant document chunks are injected into the LLM prompt

The assistant responds only using retrieved context

Answers include citations and are logged for review


🚀 How to Run

1️⃣ Install dependencies

pip install -r requirements.txt

2️⃣ Configure environment

Create a .env file (see .env.example):
OPENAI_API_KEY=api_key_here
MODEL_CHAT=gpt-4o-mini
MODEL_EMBED=text-embedding-3-small

3️⃣ Build the vector index

python scripts/build_index.py


4️⃣ Run the chatbot

cd app
streamlit run streamlit_app.py


🧪 Example Questions to Try

Supported (with citations):

How do I fix a scanner that is not syncing?

What are the Day 1 onboarding steps?

What should I do if I receive a phishing email?

Unsupported (safe refusal):

What is our company VPN URL?

Can you share an admin password?


🔐 Safety & Design Decisions

No credentials or sensitive data are ever generated

The assistant refuses to answer out-of-scope questions

All responses are traceable to source documents

Logs enable future monitoring for hallucinations or misuse


📈 Future Improvements

Confidence scoring for retrieved answers

Admin dashboard for reviewing AI logs

Automated document re-indexing

Role-based access control for responses

Integration with ticketing systems (Zendesk / Intercom)

Screenshots:


![Chat_ui](/docs/image.png)

![alt text](/docs/nohallucination.png)