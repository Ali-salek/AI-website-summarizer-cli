# 🌐 AI Website Summarizer CLI

[فارسی](README.fa.md) | **English**

A lightweight terminal tool that fetches any web page and summarizes it with an AI model through [OpenRouter](https://openrouter.ai). The summary is written in the **same language as the website** (Persian, English, and more).

![Python](https://img.shields.io/badge/python-3.9%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## ✨ Features

- 🔗 Paste a URL and get a concise Markdown summary in seconds
- 🌍 Automatically replies in the website's language
- 🧹 Strips scripts, styles, navigation, footers, forms and other noise before summarizing
- 📰 Highlights news and announcements separately
- 🔁 Interactive loop: summarize as many sites as you like in one session
- 🛡️ Prompt-injection aware: website content is treated as untrusted data
- 🔌 Works with any model available on OpenRouter

## 📦 Installation

```bash
git clone https://github.com/<your-username>/ai-website-summarizer-cli.git
cd ai-website-summarizer-cli

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
```

## ⚙️ Configuration

1. Get an API key from [OpenRouter](https://openrouter.ai/keys).
2. Copy the example environment file and fill it in:

```bash
cp .env.example .env
```

```env
API_KEY=your_openrouter_api_key_here
MODEL_NAME=openai/gpt-4o-mini
```

`MODEL_NAME` can be any model ID from the [OpenRouter model list](https://openrouter.ai/models).

## 🚀 Usage

```bash
python main.py
```

```text
==================================================
       AI WEBSITE SUMMARIZER
==================================================

Paste a website URL to summarize it.
Type 'exit' to quit.

Website URL > example.com

[1/3] Fetching website content...
[2/3] Building prompts...
[3/3] Generating AI summary...
```

- The `https://` prefix is added automatically if you omit it.
- Type `exit` or `quit` (or press `Ctrl+C`) to leave.

## 🧠 How It Works

1. **Fetch**: downloads the page with `requests`.
2. **Clean**: `BeautifulSoup` removes non-content elements and extracts readable text.
3. **Trim**: content is limited to 8,000 characters to keep requests fast and cheap.
4. **Summarize**: the text is sent to the selected model via the OpenRouter API (OpenAI-compatible SDK).

## 🔧 Customization

Everything lives in `main.py`:

| What                | Where                                   |
| ------------------- | --------------------------------------- |
| Summary style/tone  | `SYSTEM_PROMPT` and `USER_PROMPT`       |
| Max content length  | `content[:8000]` in `get_website_content` |
| Creativity          | `temperature` in `make_answer`          |
| Max summary length  | `max_tokens` in `make_answer`           |

## ⚠️ Limitations

- Pages rendered entirely with JavaScript (SPAs) may return little or no text.
- Sites that block scrapers or require login can't be fetched.
- Long pages are truncated to the first 8,000 characters.
- Respect each website's terms of service and `robots.txt`.
- API usage is billed by your OpenRouter account and chosen model.

## 🤝 Contributing

Issues and pull requests are welcome. Ideas: JS rendering support, saving summaries to a file, command-line arguments (`python main.py <url>`), chunked summarization for long pages.

## 📄 License

Released under the [MIT License](LICENSE).
