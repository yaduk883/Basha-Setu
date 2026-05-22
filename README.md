# BhashaSetu — Translation Data Collector

> *Setu* (सेतु) means bridge in Sanskrit. BhashaSetu is a bridge between English and India's many languages — built to collect high-quality, human-verified translation pairs for AI and NLP research.

---

## What is this?

BhashaSetu is a lightweight web app for collecting parallel translation data across Indian languages. The goal is simple: make it easy for contributors to submit clean, accurate English ↔ Indian language sentence pairs that can be used to train and fine-tune language models.

India has 22 scheduled languages and hundreds of dialects. Most of them are severely underrepresented in publicly available NLP datasets. This project is a small attempt to change that.

---

## Features

- Submit English ↔ Indian language translation pairs through a clean, minimal UI
- Supports 14 Indian languages including Hindi, Tamil, Telugu, Malayalam, Bengali, Kannada, Gujarati, Punjabi, Marathi, Odia, Urdu, Assamese, and Bodo
- Automatic script validation — catches transliteration and wrong-language inputs
- Duplicate detection before saving
- Admin dashboard with approval/rejection workflow
- CSV export for dataset use
- Dark mode support

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Database | Supabase (PostgreSQL) |
| Hosting | GitHub Pages |
| CI/CD | GitHub Actions |
| Charts | Chart.js |
| Icons | Tabler Icons |

No frameworks, no build tools. Just a single `app.html` file — intentionally kept simple so anyone can read, fork, and contribute without setup overhead.

---

## Getting Started

### Prerequisites

- A GitHub account
- A Supabase account (free tier is enough)

### 1. Fork the repository

```bash
git clone https://github.com/yaduk883/Basha-Setu.git
cd Basha-Setu
```

### 2. Set up Supabase

1. Create a new project at [supabase.com](https://supabase.com)
2. Run the following SQL in your Supabase SQL editor to create the translations table:

```sql
create table translations (
  id text primary key,
  source_lang text not null,
  target_lang text not null,
  source_text text not null,
  target_text text not null,
  status text default 'Pending',
  created_at timestamptz default now(),
  edited_at timestamptz
);
```

3. Enable Row Level Security (RLS) on the table and set appropriate policies for your use case.

### 3. Configure your credentials

Open `app.html` and update these lines with your own Supabase project details:

```js
const SUPABASE_URL = "https://your-project.supabase.co";
const SUPABASE_KEY = "your-publishable-key";
```

### 4. Set up the admin password (via GitHub Actions)

The admin password is injected at deploy time using GitHub Actions secrets — it never lives in your source code.

In your repository go to **Settings → Secrets and variables → Actions** and add:

| Secret name | Value |
|---|---|
| `ADMIN_PASSWORD` | Your chosen admin password |

The `.github/workflows/deploy.yml` will automatically inject it during deployment.

### 5. Deploy

Push to `main`. GitHub Actions will handle the rest — injecting secrets and deploying to GitHub Pages automatically.

---

## How to Contribute

Contributions are welcome, whether that's adding a new language, improving validation logic, or fixing a bug.

1. Fork the repo and create a new branch
2. Make your changes in `app.html`
3. Test locally by opening the file directly in your browser
4. Submit a pull request with a clear description of what you changed and why

If you're contributing translation data directly through the app, submissions go through a review queue before being marked as approved. Quality over quantity — accurate, natural translations are far more useful than large volumes of noisy data.

---

## Dataset

The data collected through BhashaSetu is intended for open research use. If you're interested in accessing the dataset or collaborating on downstream NLP tasks, feel free to open an issue or reach out directly.

---

## License

MIT License — see [LICENSE](LICENSE) for details.

You're free to use, modify, and distribute this project. If you build something with it or use the dataset, a mention would be appreciated but isn't required.

---

*Built with the hope that every Indian language gets the NLP representation it deserves.*
