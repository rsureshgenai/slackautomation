# 🤖 Slack Welcome + Auto Newsletter Bot

An automated Slack bot built with **n8n** that welcomes new members and sends AI-generated offer images to a Slack channel every 5 minutes.

---

## 🚀 What This Bot Does

### Flow 1 — Welcome Bot (Slack Trigger)
- Listens for messages in the **#social** Slack channel
- When someone says **"Hi"**, instantly sends a welcome message
- Filters out bot messages to prevent loops

### Flow 2 — Newsletter Bot (Schedule Trigger)
- Runs automatically **every 5 minutes**
- Rotates through different offer content
- Generates AI images using **OpenAI DALL-E**
- Uploads images to **imgbb**
- Posts the offer image directly to **#social**

---

## 🔗 Workflow Architecture

Flow 1:
Slack Trigger → IF "Hi" → Send Welcome Message

Flow 2:
Schedule Trigger → Rotate Content → Generate AI Image → Upload to imgbb → Send to Slack

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Workflow automation |
| Slack API | Trigger + Send messages |
| OpenAI DALL-E | AI image generation |
| imgbb API | Image hosting |
| Hostinger VPS | n8n self-hosting |

---

## ⚙️ Setup Instructions

### 1. Prerequisites
- n8n instance (self-hosted or cloud)
- Slack workspace with admin access
- OpenAI API key
- imgbb API key

### 2. Slack App Configuration
1. Go to [api.slack.com/apps](https://api.slack.com/apps)
2. Create a new app → **Newsletter AI Bot**
3. Add **Bot Token Scopes**:
   - `channels:read`
   - `channels:history`
   - `chat:write`
4. Enable **Event Subscriptions**
5. Add bot event: `message.channels`
6. Set Request URL to your n8n webhook URL
7. Install app to workspace

### 3. n8n Workflow Setup
1. Import the workflow JSON into n8n
2. Add credentials:
   - **Slack API** → Bot User OAuth Token
   - **OpenAI API** → API Key
   - **imgbb API** → API Key
3. Set the Slack Trigger webhook URL in Slack API
4. Publish the workflow

### 4. Environment Variables (Hostinger)
N8N_HOST=your-domain.com
N8N_PORT=5678
N8N_PROTOCOL=https

---

## 📸 How It Works

### Welcome Flow
1. User sends **"Hi"** in #social
2. Bot checks if it's a human message (not a bot)
3. Bot instantly replies with a welcome message

### Newsletter Flow
1. Schedule triggers every **5 minutes**
2. Content rotates between different offer types:
   - 20% OFF on all services
   - New Feature Released
   - Special Discount
3. OpenAI generates a professional offer image
4. Image is uploaded to imgbb
5. Image URL is posted to #social

---

## 🔧 Nodes Used

- **Slack Trigger** — Listens for Slack messages
- **IF Node** — Checks if message contains "hi" and is from a human
- **Schedule Trigger** — Runs every 5 minutes
- **Code Node** — Rotates offer content
- **OpenAI Node** — Generates AI images
- **HTTP Request** — Uploads to imgbb API
- **Slack Node** — Sends messages to #social

---

## 🐛 Common Issues and Fixes

| Issue | Fix |
|-------|-----|
| Slack trigger not firing | Check Event Subscriptions webhook URL |
| OAuth scope error | Add channels:read, channels:history, chat:write |
| Image shows undefined | Use {{ $('HTTP Request').item.json.data.url }} |
| Challenge verification failed | Publish workflow before verifying URL |
| Bot responding to itself | Add $json.bot_id is empty condition in IF node |

---

## 📌 Key Learnings

- Setting up Slack webhooks and OAuth scopes
- Integrating OpenAI image generation in workflows
- Chaining multiple APIs (Slack + OpenAI + imgbb)
- Building event-driven and scheduled automations
- Debugging n8n production vs test webhook URLs
- Handling bot loop prevention

---

## 🔥 Future Improvements

- Add personalized welcome images per user
- Track which offers have been sent to avoid repetition
- Add more offer categories
- Send offers at optimal engagement times
- Add analytics to track click rates

---

## 👨‍💻 Author

**Suresh R**
GEN AI Architect Program — Batch 7 (2026)

---

## 📄 License

MIT License — feel free to use and modify!
