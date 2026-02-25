# 🌐 Free Translate API

A **free, self-hosted translation API** powered by Google Translate — with a beautiful browser UI and clean JSON responses. No API keys, no costs, no limits.

> **GitHub:** [soumenmaity3/free-translate](https://github.com/soumenmaity3/free-translate)

---

## ✨ Features

- 🔤 Translate words and sentences between **109+ languages**
- 🔍 **Auto language detection** — no need to specify source language
- 📖 Returns **phonetics, definitions, synonyms, and examples**
- 🖥️ Comes with a **built-in browser UI** for visual translation
- 🐳 **Docker-ready** for easy deployment on any cloud platform
- 🆓 100% free — powered by `googletrans`

---

## 🚀 Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/soumenmaity3/free-translate.git
cd free-translate
```

### 2. Install dependencies
```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m pip install legacy-cgi
```

### 3. Create a `.env` file in the project root
```env
SECRET_KEY=django-insecure-your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=*
```

### 4. Run migrations
```powershell
.\.venv\Scripts\python.exe manage.py migrate
```

### 5. Start the server
```powershell
.\.venv\Scripts\python.exe manage.py runserver
```

Open your browser at 👉 **http://127.0.0.1:8000/**

---

## 🌍 API Endpoints

### `GET /translate` — Translate Text

| Parameter | Required | Description |
|-----------|----------|-------------|
| `sl` | ❌ No | Source language code (auto-detected if omitted) |
| `dl` | ✅ Yes | Destination language code |
| `text` | ✅ Yes | Word or sentence to translate |

**Example — with source language:**
```
GET /translate?sl=en&dl=tr&text=example
```

**Example — auto language detection:**
```
GET /translate?dl=es&text=hello world
```

**Response:**
```json
{
  "source-language": "en",
  "source-text": "example",
  "destination-language": "tr",
  "destination-text": "örnek",
  "pronunciation": {
    "source-text-phonetic": "iɡˈzampəl",
    "source-text-audio": "https://translate.google.com/translate_tts?...",
    "destination-text-audio": "https://translate.google.com/translate_tts?..."
  },
  "translations": {
    "all-translations": [["örnek", ["example", "sample", "instance"]]],
    "possible-translations": ["örnek", "misal", "örnek vermek"],
    "possible-mistakes": null
  },
  "definitions": [
    {
      "part-of-speech": "noun",
      "definition": "a thing characteristic of its kind or illustrating a general rule.",
      "example": "it's a good example of how action can produce results",
      "other-examples": ["..."],
      "synonyms": { "": ["specimen", "sample", "instance"] }
    }
  ],
  "see-also": null
}
```

---

### `GET /languages` — List Supported Languages

Returns all supported language codes and their names.

```
GET /languages
```

**Response:**
```json
{
  "en": "english",
  "es": "spanish",
  "tr": "turkish",
  "fr": "french",
  "de": "german",
  "ar": "arabic",
  ...
}
```

---

## 🏗️ Tech Stack

| Technology | Role |
|------------|------|
| **Python 3.10+** | Backend language |
| **Django 4.1** | Web framework |
| **googletrans** | Google Translate wrapper |
| **Gunicorn** | Production WSGI server |
| **Docker** | Containerization |
| **python-dotenv** | Environment variable management |

---

## 🐳 Deploy with Docker

```bash
docker build -t free-translate-api .
docker run -p 8000:8000 \
  -e SECRET_KEY=your-secret-key \
  -e DEBUG=False \
  -e ALLOWED_HOSTS=yourdomain.com \
  free-translate-api
```

---

## ☁️ Deploy on Render

1. Push this repo to GitHub
2. Go to [render.com](https://render.com) → **New Web Service**
3. Connect your GitHub repo
4. Set **Runtime** to `Docker`
5. Add environment variables: `SECRET_KEY`, `DEBUG=False`, `ALLOWED_HOSTS=your-app.onrender.com`
6. Click **Deploy** 🚀

> See [`DEPLOY.md`](./DEPLOY.md) for the full step-by-step guide.

---

## 📚 Documentation

| File | Description |
|------|-------------|
| [`SETUP.md`](./SETUP.md) | How to run the project locally |
| [`API_DOCS.md`](./API_DOCS.md) | Full REST API reference |
| [`DEPLOY.md`](./DEPLOY.md) | GitHub & Render deployment guide |
| [`PROJECT_EXPLAINED.md`](./PROJECT_EXPLAINED.md) | End-to-end project architecture explanation |

---

## 📁 Project Structure

```
free_translate_api/
├── core/               → Django settings, URL routing
├── index/              → Homepage view
├── translate/          → Translation & Languages API logic
├── templates/
│   └── index.html      → Browser-based translation UI
├── manage.py
├── requirements.txt
├── Dockerfile
└── .env                → Local secrets (not in Git)
```

---

## ⚠️ Important Notes

- **Never commit `.env`** to GitHub — it's already in `.gitignore`
- Set `DEBUG=False` in production
- `googletrans` is a reverse-engineered library. It's free but may occasionally break if Google updates their internal API

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE.md) file for details.

---

## 👤 Author

**Soumen Maity**
- GitHub: [@soumenmaity3](https://github.com/soumenmaity3)

 
