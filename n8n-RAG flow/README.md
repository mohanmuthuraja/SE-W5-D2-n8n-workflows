# n8n RAG Chatbot (Telegram + Google Drive + Pinecone)

## Overview

This workflow implements a Retrieval-Augmented Generation (RAG) chatbot
using: - Telegram (user interface) - Google Drive (document ingestion) -
Pinecone (vector database) - OpenAI (LLM + embeddings) - SerpAPI
(fallback search)

It automatically ingests documents from Google Drive, stores embeddings
in Pinecone, and answers user queries via Telegram.

------------------------------------------------------------------------

## Features

-   📥 Auto-ingest new files from Google Drive
-   🔎 Vector search using Pinecone
-   🤖 AI Agent with memory
-   🌐 Fallback to Google search (SerpAPI)
-   💬 Telegram chatbot interface

------------------------------------------------------------------------

## Architecture

### 1. Document Ingestion Pipeline

Google Drive Trigger → Download File → Text Split → Embeddings →
Pinecone

### 2. Chatbot Pipeline

Telegram → AI Agent → Vector Search → (Fallback: SerpAPI) → Response

------------------------------------------------------------------------

## Nodes Explained

### Ingestion Flow

-   **Google Drive Trigger**
    -   Watches folder for new files
-   **Download File**
    -   Downloads the uploaded file
-   **Recursive Character Text Splitter**
    -   Splits documents into chunks
-   **Default Data Loader**
    -   Converts binary to text
-   **Embeddings OpenAI**
    -   Generates embeddings
-   **Pinecone Vector Store**
    -   Stores vectors in namespace

### Chat Flow

-   **Telegram Trigger**
    -   Receives user messages
-   **AI Agent**
    -   Core reasoning engine
-   **OpenAI Chat Model**
    -   LLM for responses
-   **Simple Memory**
    -   Maintains chat context
-   **Vector Store Tool**
    -   Retrieves relevant chunks
-   **SerpAPI Tool**
    -   Fallback for unknown queries
-   **Send Message**
    -   Sends reply to Telegram

------------------------------------------------------------------------

## Setup Instructions

### 1. Requirements

-   n8n (latest version)
-   OpenAI API key
-   Pinecone account
-   Telegram Bot token
-   Google Drive OAuth
-   SerpAPI key

------------------------------------------------------------------------

### 2. Configure Credentials

Set up in n8n: - OpenAI API - Pinecone API - Telegram API - Google Drive
OAuth - SerpAPI

------------------------------------------------------------------------

### 3. Google Drive Setup

-   Create a folder
-   Upload documents (txt, pdf, etc.)
-   Set folder ID in trigger node

------------------------------------------------------------------------

### 4. Pinecone Setup

-   Create index: `vectordb`
-   Set namespace dynamically or fixed

------------------------------------------------------------------------

### 5. Telegram Setup

-   Create bot via @BotFather
-   Add token in credentials
-   Start chat with bot

------------------------------------------------------------------------

## How It Works

1.  Upload file → stored in Pinecone
2.  User sends message on Telegram
3.  AI Agent:
    -   Searches vector DB
    -   If no answer → calls SerpAPI
4.  Response sent back to user

------------------------------------------------------------------------

## Notes

-   Namespace is dynamically generated for ingestion
-   Query node uses fixed namespace → must match if needed
-   Supports multi-turn conversations via memory

------------------------------------------------------------------------

## Import Workflow

Use this file:

Workflow JSON: see attached in repo

------------------------------------------------------------------------

## Improvements

-   Add metadata filtering
-   Use reranking
-   Add multi-file support
-   Use streaming responses

------------------------------------------------------------------------

## License

MIT
