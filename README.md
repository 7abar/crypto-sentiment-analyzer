# 🪙 Crypto Sentiment Analyzer

> Real-time sentiment analysis for 50+ cryptocurrency tokens using fine-tuned BERT — built for traders, researchers, and Web3 enthusiasts.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0-orange?logo=pytorch)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-yellow)
![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green?logo=fastapi)
![Docker](https://img.shields.io/badge/Docker-ready-blue?logo=docker)

---

## 📌 Overview

Crypto Sentiment Analyzer is an end-to-end NLP pipeline that:
- Ingests real-time posts from **Twitter/X** and **Reddit**
- Classifies sentiment (Bullish / Bearish / Neutral) using a **fine-tuned BERT model**
- Serves results via a **REST API** for downstream use (trading signals, dashboards, alerts)

> ⚡ Processes 10,000+ posts/day | 87% classification accuracy on crypto-domain test set

---

## 🏗️ Architecture

```
Twitter API v2 ──┐
                 ├──► Ingestion Pipeline ──► Preprocessing ──► BERT Model ──► FastAPI ──► Dashboard
Reddit (PRAW) ───┘         (async)            (NLP Clean)      (inference)    (REST)
                                                                    │
                                                            Model Registry
                                                         (auto-retrain weekly)
```

---

## 🚀 Features

- 🔍 **Real-time ingestion** — async scraping via Twitter API v2 & PRAW
- 🧠 **Fine-tuned BERT** — domain-adapted on 50,000+ labeled crypto tweets
- 🏷️ **Auto-labeling** — uses OpenAI API to generate training labels, reducing manual effort by ~70%
- 📡 **REST API** — FastAPI endpoints for token-level sentiment scores
- 🐳 **Dockerized** — ready to deploy on any cloud (AWS EC2, GCP, Railway)
- 🔄 **Auto-retraining** — scheduled weekly retraining pipeline via cron

---

## 📊 Model Performance

| Metric    | Score  |
|-----------|--------|
| Accuracy  | 87.3%  |
| F1-Score  | 0.85   |
| Precision | 0.86   |
| Recall    | 0.84   |

> Evaluated on 5,000 held-out crypto tweets (May 2024)

---

## 🛠️ Tech Stack

| Layer         | Technology                          |
|---------------|-------------------------------------|
| Language      | Python 3.10+                        |
| ML Framework  | PyTorch, HuggingFace Transformers   |
| Data Source   | Twitter API v2, Reddit (PRAW)       |
| API           | FastAPI                             |
| LLM           | OpenAI API (auto-labeling)          |
| Infra         | Docker, AWS EC2                     |
| Data          | pandas, numpy                       |

---

## 📁 Project Structure

```
crypto-sentiment-analyzer/
├── src/
│   ├── scraper.py          # Async Twitter & Reddit ingestion
│   ├── preprocessor.py     # Text cleaning, ticker extraction
│   ├── model.py            # BERT fine-tuning & inference
│   ├── labeler.py          # OpenAI-powered auto-labeling
│   └── api.py              # FastAPI REST endpoints
├── notebooks/
│   └── 01_eda_and_training.ipynb   # Exploratory analysis & model training
├── data/
│   └── sample/             # Sample labeled dataset (500 tweets)
├── tests/
│   └── test_model.py
├── Dockerfile
├── requirements.txt
└── README.md
```

---

## ⚙️ Setup & Installation

```bash
# 1. Clone the repo
git clone https://github.com/YOUR_USERNAME/crypto-sentiment-analyzer.git
cd crypto-sentiment-analyzer

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set environment variables
cp .env.example .env
# Fill in: TWITTER_BEARER_TOKEN, REDDIT_CLIENT_ID, OPENAI_API_KEY

# 4. Run the API
uvicorn src.api:app --reload
```

**Or with Docker:**
```bash
docker build -t crypto-sentiment .
docker run -p 8000:8000 --env-file .env crypto-sentiment
```

---

## 📡 API Usage

```bash
# Get sentiment for a token
GET /sentiment?token=BTC&limit=100

# Response
{
  "token": "BTC",
  "sentiment": "bullish",
  "score": 0.82,
  "sample_size": 100,
  "timestamp": "2024-05-01T10:00:00Z"
}
```

---

## 🗺️ Roadmap

- [ ] Add Telegram & Discord as data sources
- [ ] Real-time WebSocket streaming endpoint
- [ ] Multi-language support (Bahasa, Chinese)
- [ ] On-chain correlation analysis (price vs sentiment)

---

## 📄 License

MIT License — feel free to use, modify, and distribute.
