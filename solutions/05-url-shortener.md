# Project 5: URL Shortener — Solution

## File Structure

```
url-shortener/
├── backend/
│   ├── database.js
│   ├── server.js
│   └── package.json
└── frontend/
    ├── index.html
    └── (no separate CSS/JS — everything is in index.html)
```

## backend/package.json

```json
{
  "name": "url-shortener-backend",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.0",
    "better-sqlite3": "^9.0.0",
    "cors": "^2.8.0",
    "dotenv": "^16.0.0"
  }
}
```

## backend/database.js

```javascript
const Database = require('better-sqlite3');
const path = require('path');

const db = new Database(path.join(__dirname, 'urls.db'));
db.pragma('journal_mode = WAL');

db.exec(`
  CREATE TABLE IF NOT EXISTS urls (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    code TEXT NOT NULL UNIQUE,
    original_url TEXT NOT NULL,
    clicks INTEGER DEFAULT 0,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
  );
`);

module.exports = db;
```

## backend/server.js

```javascript
require('dotenv').config();
const express = require('express');
const crypto = require('crypto');
const cors = require('cors');
const path = require('path');
const db = require('./database');

const app = express();
const PORT = process.env.PORT || 3001;

app.use(cors());
app.use(express.json());

// ─── API: Create short URL ───

app.post('/api/shorten', (req, res) => {
  const { url } = req.body;

  if (!url) return res.status(400).json({ error: 'URL is required' });

  // Basic URL validation
  try {
    new URL(url);
  } catch {
    return res.status(400).json({ error: 'Invalid URL format' });
  }

  // Generate unique code (6 random characters)
  const code = crypto.randomBytes(4).toString('base64url').slice(0, 6);

  db.prepare('INSERT INTO urls (code, original_url) VALUES (?, ?)').run(code, url);

  const shortUrl = `${req.protocol}://${req.get('host')}/${code}`;
  res.status(201).json({ shortUrl, code, originalUrl: url });
});

// ─── Redirect: short code → original URL ───

app.get('/:code', (req, res) => {
  const { code } = req.params;

  const url = db.prepare('SELECT * FROM urls WHERE code = ?').get(code);

  if (!url) {
    return res.status(404).send(`
      <html><body style="font-family:sans-serif;text-align:center;padding:50px;">
        <h1>🔗 Not Found</h1>
        <p>This shortened URL doesn't exist.</p>
        <a href="/">Create one</a>
      </body></html>
    `);
  }

  // Increment click count
  db.prepare('UPDATE urls SET clicks = clicks + 1 WHERE id = ?').run(url.id);

  // Redirect to the original URL
  res.redirect(url.original_url);
});

// ─── API: Get stats ───

app.get('/api/stats/:code', (req, res) => {
  const url = db.prepare('SELECT * FROM urls WHERE code = ?').get(req.params.code);
  if (!url) return res.status(404).json({ error: 'Not found' });
  res.json(url);
});

// Serve frontend
app.use(express.static(path.join(__dirname, '../frontend')));

app.listen(PORT, () => console.log(`URL shortener running at http://localhost:${PORT}`));
```

## frontend/index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>URL Shortener</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #667eea, #764ba2);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }
    .card {
      background: white;
      padding: 40px;
      border-radius: 16px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.2);
      width: 100%;
      max-width: 500px;
      text-align: center;
    }
    h1 { margin-bottom: 8px; color: #333; }
    .subtitle { color: #666; margin-bottom: 30px; }
    .input-group {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }
    input {
      flex: 1;
      padding: 14px;
      border: 2px solid #e2e8f0;
      border-radius: 8px;
      font-size: 16px;
    }
    input:focus { outline: none; border-color: #667eea; }
    button {
      padding: 14px 24px;
      background: #667eea;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
    }
    button:hover { background: #5a6fd6; transform: translateY(-1px); }
    .result {
      display: none;
      background: #f0fdf4;
      border: 2px solid #86efac;
      border-radius: 8px;
      padding: 20px;
      margin-top: 20px;
    }
    .result.show { display: block; }
    .result a {
      display: block;
      color: #16a34a;
      font-size: 1.2rem;
      word-break: break-all;
      margin-bottom: 12px;
      text-decoration: none;
      font-weight: 600;
    }
    .result a:hover { text-decoration: underline; }
    .copy-btn {
      background: #22c55e;
      padding: 8px 20px;
      font-size: 14px;
    }
    .copy-btn:hover { background: #16a34a; }
    .error {
      color: #dc2626;
      margin-top: 10px;
      display: none;
    }
    .error.show { display: block; }
  </style>
</head>
<body>
  <div class="card">
    <h1>🔗 Link Shortener</h1>
    <p class="subtitle">Paste a long URL and make it short</p>

    <div class="input-group">
      <input type="url" id="url-input" placeholder="https://very-long-url.com/..." autofocus>
      <button id="shorten-btn">Shorten</button>
    </div>

    <div class="error" id="error"></div>

    <div class="result" id="result">
      <p style="color:#666;margin-bottom:8px;">Your shortened URL:</p>
      <a id="short-url" href="#" target="_blank"></a>
      <button class="copy-btn" id="copy-btn">Copy to Clipboard</button>
    </div>
  </div>

  <script>
    const API_URL = 'http://localhost:3001';

    const urlInput = document.getElementById('url-input');
    const shortenBtn = document.getElementById('shorten-btn');
    const resultDiv = document.getElementById('result');
    const shortUrl = document.getElementById('short-url');
    const errorDiv = document.getElementById('error');
    const copyBtn = document.getElementById('copy-btn');

    shortenBtn.addEventListener('click', shortenUrl);
    urlInput.addEventListener('keydown', (e) => {
      if (e.key === 'Enter') shortenUrl();
    });

    async function shortenUrl() {
      const url = urlInput.value.trim();
      if (!url) return;

      errorDiv.classList.remove('show');
      resultDiv.classList.remove('show');
      shortenBtn.textContent = 'Shortening...';
      shortenBtn.disabled = true;

      try {
        const res = await fetch(`${API_URL}/api/shorten`, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ url }),
        });

        if (!res.ok) {
          const err = await res.json();
          throw new Error(err.error);
        }

        const data = await res.json();
        shortUrl.textContent = data.shortUrl;
        shortUrl.href = data.shortUrl;
        resultDiv.classList.add('show');
        urlInput.value = '';
      } catch (err) {
        errorDiv.textContent = err.message;
        errorDiv.classList.add('show');
      } finally {
        shortenBtn.textContent = 'Shorten';
        shortenBtn.disabled = false;
      }
    }

    copyBtn.addEventListener('click', () => {
      navigator.clipboard.writeText(shortUrl.textContent).then(() => {
        copyBtn.textContent = 'Copied!';
        setTimeout(() => { copyBtn.textContent = 'Copy to Clipboard'; }, 2000);
      });
    });

    urlInput.focus();
  </script>
</body>
</html>
```
