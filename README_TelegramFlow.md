# 🤖 Telegram Chatbot using n8n + OpenAI

A no-code AI-powered Telegram bot built with [n8n](https://n8n.io) and OpenAI, self-hosted on a VPS (e.g. Hostinger) via Docker.

---

## 📐 Flow Architecture

```
[Telegram Trigger] → [Basic LLM Chain] → [OpenAI Chat Model] → [Send Text Message]
```

| Node | Role |
|---|---|
| **Telegram Trigger** | Listens for incoming messages via webhook |
| **Basic LLM Chain** | Packages the user message + system prompt and routes to LLM |
| **OpenAI Chat Model** | Calls OpenAI API and generates a reply |
| **Send Text Message** | Sends the AI response back to the Telegram chat |

---

## ⚡ Quick Setup (Step by Step)

### Step 1 — Create a Telegram Bot
1. Open Telegram → search **@BotFather**
2. Send `/newbot` → enter a bot name → enter a username (must end with `bot`)
3. Copy the **API Key** shown

### Step 2 — Configure n8n Telegram Trigger
1. In n8n, add a **Telegram Trigger** node
2. Set trigger type: **Message Trigger**
3. Add Telegram credentials → paste the API Key from Step 1

### Step 3 — Add Basic LLM Chain
1. Add a **Basic LLM Chain** node
2. Set the **prompt** (input) to:
   ```
   {{ $json.message.text }}
   ```
3. Set the **system prompt** to define bot behaviour, e.g.:
   ```
   You are a personal assistant
   ```

### Step 4 — Connect OpenAI Chat Model
1. Add an **OpenAI Chat Model** node (connects as sub-node of LLM Chain)
2. Add OpenAI credentials → paste your OpenAI API Key
3. Select model (e.g. `gpt-4o`, `gpt-3.5-turbo`)

### Step 5 — Add Send Message Node
1. Add a **Telegram → Send a Text Message** node
2. Set credentials to the same Telegram bot
3. Set **Chat ID**:
   ```
   {{ $("Telegram Trigger").item.json.message.chat.id }}
   ```
   > 💡 To find your own chat ID, message **@get_id_bot** on Telegram
4. Set **Text** (the reply):
   ```
   {{ $json.text }}
   ```

### Step 6 — Activate & Test
1. Click **Execute Workflow** to test
2. Click **Publish** (top right) to activate permanently
3. Send a message to your bot on Telegram

---

## 🔑 Variables / Parameters Reference

| Variable | Node | Value | Description |
|---|---|---|---|
| `$json.message.text` | LLM Chain prompt | User's message | The text sent by user in Telegram |
| `$("Telegram Trigger").item.json.message.chat.id` | Send Message → Chat ID | Dynamic | Unique identifier of the Telegram chat |
| `$json.text` | Send Message → Text | LLM response | The AI-generated reply text |
| System Prompt | Basic LLM Chain | `"You are a personal assistant"` | Sets LLM personality/behaviour |
| OpenAI API Key | OpenAI Chat Model | From OpenAI platform | Authenticates requests to OpenAI |
| Telegram Bot Token | Telegram nodes | From @BotFather | Authenticates the Telegram bot |

---

## 🐳 Hosting on Hostinger VPS (Docker)

n8n is deployed as a Docker container via Hostinger's Docker Manager.

**Docker project name:** `n8n-hgrp`  
**Container image:** `docker.n8n.io/n8nio/n8n`  
**Port mapping:** `32770:5678`

### Required Environment Variables

| Name | Value | Purpose |
|---|---|---|
| `TZ` | e.g. `Asia/Kolkata` | Timezone for workflow scheduling |
| `TRAEFIK_HOST` | Your domain/subdomain | Routes external traffic to n8n |
| `N8N_TRUSTED_PROXIES` | `0.0.0.0/0` | **Required for SSL/HTTPS fix** |

---

## 🔒 SSL / HTTPS Fix (Telegram Webhook Issue)

If n8n **cannot connect to Telegram** (insecure browser / HTTP error / webhook fails), this is caused by n8n not trusting the proxy headers from the reverse proxy.

**Fix:** Add the following environment variable in your Docker container:

```
N8N_TRUSTED_PROXIES = 0.0.0.0/0
```

**How to set it in Hostinger Docker Manager:**
1. Go to **VPS → Docker Manager**
2. Click **Edit** on your n8n container
3. Scroll to **Environment** section
4. Add:
   - **Name:** `N8N_TRUSTED_PROXIES`
   - **Value:** `0.0.0.0/0`
5. Click **Deploy**

> ⚠️ `0.0.0.0/0` trusts all proxies. Fine for private VPS use; for production, restrict to your actual proxy IP.

---

## 🗂 Project Structure (n8n Workflow)

```
Telegram Flow (n8n Workflow)
├── Telegram Trigger          ← Entry point (webhook)
│   └── Updates: message
├── Basic LLM Chain           ← Core logic node
│   ├── Prompt: $json.message.text
│   ├── System prompt: "You are a personal assistant"
│   └── Model* → OpenAI Chat Model
│       └── Model: gpt-4o (or chosen model)
└── Send a Text Message       ← Output node
    ├── Chat ID: $("Telegram Trigger").item.json.message.chat.id
    └── Text: $json.text
```

---

## 🔗 Useful Links

- [n8n Telegram Trigger docs](https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.telegramtrigger/)
- [BotFather on Telegram](https://t.me/BotFather)
- [Get your Chat ID](https://t.me/get_id_bot)
- [OpenAI API Keys](https://platform.openai.com/api-keys)
- [n8n Docker setup](https://docs.n8n.io/hosting/installation/docker/)
