# 🤖 AI Telegram Bot Workflow (n8n)

## 🚀 Overview

This workflow creates an AI-powered Telegram chatbot using n8n. It
listens to user messages, processes them using OpenAI, optionally
fetches real-time data via SerpAPI, and responds back to the user on
Telegram.

------------------------------------------------------------------------

## 🔄 Workflow Architecture

Telegram → AI Agent → OpenAI → Tools (SerpAPI / Gmail) → Telegram
Response

------------------------------------------------------------------------

## 🧩 Nodes Explained

### 📩 Telegram Trigger

-   Listens for incoming Telegram messages
-   Starts the workflow
-   Captures user input (text, chat ID)

------------------------------------------------------------------------

### 🤖 AI Agent

-   Core logic of the workflow
-   Processes user queries
-   Decides when to use tools (SerpAPI / Gmail)
-   Generates intelligent responses

------------------------------------------------------------------------

### 💬 OpenAI Chat Model

-   Uses GPT model (gpt-4o-mini)
-   Handles natural language understanding
-   Generates AI responses

------------------------------------------------------------------------

### 🧠 Simple Memory

-   Stores chat history per user
-   Enables context-aware conversations

------------------------------------------------------------------------

### 🌐 SerpAPI Tool

-   Fetches real-time search results
-   Used for latest news or live queries

------------------------------------------------------------------------

### 📧 Gmail Tool

-   Sends emails when requested by user
-   Supports dynamic subject and message

------------------------------------------------------------------------

### 📤 Send Message (Telegram)

-   Sends AI response back to user
-   Uses chat ID from trigger

------------------------------------------------------------------------

## ⚙️ Features

-   AI-powered chatbot
-   Context memory
-   Real-time search integration
-   Email sending capability
-   Multi-tool AI agent
-   Fully automated responses

------------------------------------------------------------------------

## 🧪 How to Use

1.  Start your Telegram bot
2.  Send a message (e.g., "latest AI news")
3.  AI Agent processes request
4.  Response is generated and sent back

------------------------------------------------------------------------

## 🔑 Requirements

-   Telegram Bot Token
-   OpenAI API Key
-   SerpAPI Key (optional)
-   Gmail OAuth (optional)

------------------------------------------------------------------------

## 📦 Workflow File

Included JSON file: WF_Telegram_AI_Agent.json

------------------------------------------------------------------------

## 🎯 Outcome

End-to-end AI assistant:

Telegram → AI → Tools → Telegram Response

------------------------------------------------------------------------

## 👨‍💻 Author

Built using n8n for AI automation and chatbot workflows.
