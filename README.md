# InfoRAG - AI Document Assistant

InfoRAG is a small Retrieval-Augmented Generation (RAG) demo built with Next.js and LangChain.js. Add text to the ingestion form, store its embeddings in Qdrant, then ask questions and retrieve relevant context for an AI-generated answer.

---

## ✨ Features

- Ingest text and split it into overlapping chunks
- 🧠 Generate embeddings for text chunks
- 🔎 Perform vector similarity search
- Ask natural-language questions about ingested text
- 🤖 Generate answers using an LLM
- 📌 Retrieve relevant document context before generating responses
- ⚡ Streaming AI responses
- 🌐 Next.js-based web interface

---

## 🏗️ How It Works

InfoRAG follows a simple RAG pipeline:

```text
                ┌─────────────────┐
                │    Text Input    │
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │  Text Preparation │
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │  Text Chunking   │
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │   Embeddings     │
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │   Vector Store   │
                └────────┬────────┘
                         │
                         │ User Query
                         ↓
                ┌─────────────────┐
                │ Query Embedding  │
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │ Similarity Search│
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │ Relevant Context │
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │       LLM        │
                └────────┬────────┘
                         ↓
                ┌─────────────────┐
                │  Generated Answer│
                └─────────────────┘
```

---

## 🛠️ Tech Stack

- Next.js 14, React 18, and TypeScript
- LangChain.js and LangGraph.js
- Qdrant vector database
- OpenAI and Anthropic chat models
- OpenAI, Cohere, Mistral, Nomic, Voyage, and Hugging Face embedding integrations

---

## 📂 Project Structure

```text
InfoRAG/
│
├── app/
│   ├── api/
│   │   ├── chat/retrieval_agents/route.ts
│   │   └── retrieval/ingest/route.ts
│   ├── ai_sdk/
│   ├── retrieval_agents/
│   ├── page.tsx
│   └── layout.tsx
├── components/
├── data/
├── public/images/
├── package.json
└── README.md
```

---

## 🔄 RAG Pipeline

### 1. Text Ingestion

The user enters or pastes text through the web interface.

### 2. Text Processing

The supplied text is divided into smaller chunks.

### 3. Embedding Generation

Each document chunk is converted into a numerical vector using an embedding model.

### 4. Vector Storage

The generated embeddings are stored in Qdrant along with their corresponding text. The selected embedding model determines the collection used.

### 5. User Query

The user asks a question about the ingested text.

### 6. Similarity Search

The query is converted into an embedding and compared with stored document vectors.

The most relevant chunks are retrieved from Qdrant.

### 7. Context-Aware Generation

The retrieved chunks are provided to the LLM as context.

The LLM generates an answer based on the retrieved information.

---

## 🚀 Getting Started

### 1. Install dependencies

```bash
corepack yarn install
```

### 2. Configure environment variables

Create a `.env.local` file in the project root. Set the Qdrant connection and credentials for the chat and embedding models you plan to use:

```env
OPENAI_API_KEY=your_openai_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key

QDRANT_URL=your_qdrant_url
QDRANT_API_KEY=your_qdrant_api_key
```

Add the API key for the embedding provider selected in the app if it differs from OpenAI. Supported integrations include Cohere, Mistral, Voyage, Nomic, and Hugging Face.

### 3. Start the development server

```bash
corepack yarn dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## API Routes

- `POST /api/retrieval/ingest?embeddingModel=<model>` accepts a JSON body containing `text`, splits and embeds it, and stores the vectors in Qdrant.
- `POST /api/chat/retrieval_agents?embeddingModel=<model>&chatModel=<provider>` runs a retrieval-agent conversation using the supplied chat messages.

---

## 💬 Example

### User

```text
What are the main responsibilities mentioned in this document?
```

### InfoRAG

```text
The document describes three main responsibilities:
1. ...
2. ...
3. ...
```

The answer is generated using relevant text chunks retrieved from the vector database.

---

## 🧠 Why RAG?

Traditional LLM applications rely only on the model's existing knowledge.

InfoRAG uses Retrieval-Augmented Generation to provide the model with relevant information from ingested text before generating an answer.

```text
Document
   ↓
Chunks
   ↓
Embeddings
   ↓
Qdrant
   ↓
Relevant Context
   ↓
LLM
   ↓
Answer
```

This makes the application useful for querying information in your text without requiring the model to have previously seen it.

---

## 📌 Key Concepts

* Retrieval-Augmented Generation (RAG)
* Document Chunking
* Text Embeddings
* Vector Similarity Search
* Vector Databases
* LangChain
* LLM-based Question Answering
* Next.js API Routes
* TypeScript

---

## 🔮 Future Improvements

* Support for multiple document formats
* Source citations in responses
* Conversation history
* Multiple document collections
* Improved document chunking strategies
* Metadata-based filtering
* Authentication and user-specific documents

---

## 📄 License

This project is for educational and portfolio purposes.
