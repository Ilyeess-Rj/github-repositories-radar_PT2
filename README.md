# GitHub Radar Bot 🔭🤖

An autonomous n8n workflow that scans GitHub daily for trending repositories matching your interests, and delivers a full Arabic voice + text + image breakdown via Telegram — plus on-demand Q&A about any specific repo.

## 🎯 What it does

### 📡 Daily automated digest
- Runs automatically on a **daily schedule** — no manual searching required.
- Scans GitHub for trending repos matching a predefined set of interests (e.g. AI, LLMs, automation tools, free-tier APIs, etc. — fully customizable via the system prompt).
- For each relevant repo found, it automatically fetches the **real README** (never guesses from memory) and generates a structured Arabic breakdown covering:
  - **What it does** — the project explained in one simple sentence.
  - **The problem it solves** — why it was built.
  - **Key strengths** — 2-3 standout features from the actual README.
  - **Ideas to stand out** — practical, realistic ways to use the project (a side project, a real problem it could solve, an integration angle, an uncommon use case).
  - **Interest score (1-10)** with actionable advice on how to leverage the project.

### 💬 On-demand assistant
- Ask about **any specific GitHub repo** at any time via Telegram.
- Get a **spoken Arabic explanation** (text-to-speech via ElevenLabs) of anything you want to know about it.
- Request an **instant illustrative image** (via Qwen image generation) explaining its architecture or how it works.
- Every answer is grounded in the repo's actual README — the bot never fabricates features or capabilities.

## 🧩 Tech Stack

| Service | Role |
|---|---|
| **n8n** | Workflow orchestration engine (scheduled + event-driven) |
| **Telegram Bot API** | User-facing interface for both the daily digest and on-demand queries |
| **OpenRouter (Nemotron)** + **Google Gemini** | LLMs powering the reasoning/writing agents |
| **Qwen (Alibaba Cloud)** | Search tool + on-demand image generation |
| **ElevenLabs** | Text-to-Speech for natural Arabic voice narration |
| **GitHub README tool** | Fetches real README content for grounded, hallucination-free answers |

## ⚙️ Setup & Usage

### 1. Import the workflow
- Open your n8n instance.
- **Workflows → Import from File** → select `GITHUB_RADAR_PT2_clean.json`.

### 2. Connect the credentials
The file ships with **no real API keys** (intentionally stripped). You'll need to connect your own:

| Credential | Where to get it |
|---|---|
| Telegram Bot Token | [@BotFather](https://t.me/BotFather) |
| OpenRouter API Key | [openrouter.ai](https://openrouter.ai) |
| Google Gemini (PaLM) API Key | [Google AI Studio](https://aistudio.google.com) |
| Qwen / Alibaba Cloud API Key | [Alibaba Cloud](https://www.alibabacloud.com) |
| ElevenLabs API Key | [elevenlabs.io](https://elevenlabs.io) |

### 3. Customize your interests
Edit the AI Agent's system prompt to set which topics the daily scan should focus on (e.g. AI, models, automations, free tokens, etc.) — fully customizable to any domain.

### 4. Replace placeholder values
The workflow file contains:
- `Telegram Chat ID` → fully dynamic (`={{ $('Telegram Trigger').item.json.message.chat.id }}`), automatically replying to whoever interacts with the bot.
- `YOUR_WEBHOOK_ID` → n8n auto-generates a new one on activation; you usually don't need to set this manually.
- `YOUR_INSTANCE_ID` → an internal identifier, auto-filled by n8n.

### 5. Activate the workflow
Toggle **Active** in n8n. The daily digest will start running on schedule, and you can message the bot anytime for on-demand repo explanations.

## 🗂️ Project Structure

```
github-radar-bot/
├── README.md
├── .gitignore
├── LICENSE
├── .env.example
└── GITHUB_RADAR_PT2_clean.json
```

## ⚠️ Security Notes

- **Never publish** a version containing real API keys or your real Telegram chat ID.
- Store secrets in a `.env` file or in n8n's credentials store — never hardcode them into the workflow JSON.

## 📄 License

This project is licensed under the Apache License 2.0 — you're free to use, modify, and distribute it (including commercially), as long as you retain the copyright notice and document any changes you make. See the [LICENSE](./LICENSE) file for full terms.
