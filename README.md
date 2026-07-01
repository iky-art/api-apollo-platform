# Apollo API Platform 🚀

Platform API key untuk Apollo AI — kompatibel dengan format OpenAI.

## Struktur Repo

```
apollo-api-platform/
├── api/
│   ├── v1/
│   │   ├── chat/
│   │   │   └── completions.js    ← Chat endpoint (OpenAI-compatible)
│   │   └── models.js             ← List models endpoint
│   ├── keys.js                   ← CRUD API keys
│   └── admin.js                  ← Admin dashboard API
├── lib/
│   └── supabase.js               ← Supabase client + auth helpers
├── public/
│   ├── index.html                ← Developer dashboard
│   └── admin.html                ← Admin panel
├── supabase_api_platform.sql     ← Jalankan di Supabase SQL Editor
├── vercel.json
└── package.json
```

## Setup

### 1. Clone & Deploy ke Vercel

```bash
git clone <repo>
cd apollo-api-platform
npm install
vercel --prod
```

### 2. Environment Variables (Vercel Dashboard)

| Key | Value |
|-----|-------|
| `GROQ_API_KEY` | API key Groq kamu |
| `SUPABASE_URL` | URL Supabase project |
| `SUPABASE_SERVICE_ROLE_KEY` | Service role key Supabase |
| `SUPABASE_ANON_KEY` | Anon key Supabase |
| `ADMIN_API_PASSWORD` | Password admin panel (contoh: `apollo-admin-2025`) |

### 3. Setup Database

Jalankan `supabase_api_platform.sql` di Supabase SQL Editor.

## API Usage

### Chat Completions

```bash
curl https://apollo-api.vercel.app/v1/chat/completions \
  -H "Authorization: Bearer apollo-sk-xxxx-xxxx-xxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "apollo-core",
    "messages": [{"role": "user", "content": "Halo!"}]
  }'
```

### List Models

```bash
curl https://apollo-api.vercel.app/v1/models \
  -H "Authorization: Bearer apollo-sk-xxxx-xxxx-xxxx"
```

## Tier & Limits

| Tier | Daily | RPM | Models | Max Keys |
|------|-------|-----|--------|----------|
| Free | 100 | 5 | Nano, Core | 1 |
| Pro | 1.000 | 20 | Semua | 5 |
| Developer | 10.000 | 60 | Semua | 999 |

## Models

| Apollo ID | Groq Model | Tier |
|-----------|-----------|------|
| apollo-nano | llama-3.1-8b-instant | Free |
| apollo-core | llama-3.3-70b-versatile | Free |
| apollo-scout | llama-4-scout-17b | Free |
| apollo-qwen | qwen3-32b | Free |
| apollo-code | gpt-oss-20b | Free |
| apollo-max | gpt-oss-120b | Pro |
| apollo-guard | gpt-oss-safeguard-20b | Pro |
| apollo-compound | groq/compound | Pro |
| apollo-compound-mini | groq/compound-mini | Pro |
| apollo-vision | llama-3.2-90b-vision | Pro |
| apollo-vision-mini | llama-3.2-11b-vision | Pro |

## Admin Panel

Akses: `https://apollo-api.vercel.app/admin`

Password: set via env `ADMIN_API_PASSWORD`

Fitur admin:
- Overview stats (total keys, requests, tokens)
- Kelola semua API keys
- Upgrade/downgrade tier
- Revoke key
- Usage logs
- Generate key manual untuk user

## OpenAI Compatibility

Bisa pakai library OpenAI resmi dengan mengubah `base_url`:

```python
from openai import OpenAI

client = OpenAI(
    api_key="apollo-sk-xxxx",
    base_url="https://apollo-api.vercel.app/v1"
)
```

```javascript
import OpenAI from 'openai';

const client = new OpenAI({
  apiKey: 'apollo-sk-xxxx',
  baseURL: 'https://apollo-api.vercel.app/v1'
});
```

