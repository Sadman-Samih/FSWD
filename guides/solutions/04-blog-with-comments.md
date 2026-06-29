# Project 4: Blog with Comments — Solution

## File Structure

```
blog-app/
├── backend/
│   ├── database.js
│   ├── server.js
│   └── package.json
└── frontend/
    ├── index.html
    ├── style.css
    └── app.js
```

## backend/package.json

```json
{
  "name": "blog-backend",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.0",
    "better-sqlite3": "^9.0.0",
    "cors": "^2.8.0"
  }
}
```

## backend/database.js

```javascript
const Database = require('better-sqlite3');
const path = require('path');

const db = new Database(path.join(__dirname, 'blog.db'));
db.pragma('journal_mode = WAL');

db.exec(`
  CREATE TABLE IF NOT EXISTS posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    content TEXT NOT NULL,
    author TEXT NOT NULL DEFAULT 'Anonymous',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
  );

  CREATE TABLE IF NOT EXISTS comments (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    post_id INTEGER NOT NULL,
    author TEXT NOT NULL DEFAULT 'Anonymous',
    body TEXT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE
  );
`);

module.exports = db;
```

## backend/server.js

```javascript
const express = require('express');
const cors = require('cors');
const path = require('path');
const db = require('./database');

const app = express();
const PORT = process.env.PORT || 3001;

app.use(cors());
app.use(express.json());

// ─── POSTS ───

// Get all posts
app.get('/api/posts', (req, res) => {
  const posts = db.prepare(`
    SELECT posts.*, COUNT(comments.id) as comment_count
    FROM posts
    LEFT JOIN comments ON comments.post_id = posts.id
    GROUP BY posts.id
    ORDER BY posts.created_at DESC
  `).all();
  res.json(posts);
});

// Get a single post with its comments
app.get('/api/posts/:id', (req, res) => {
  const post = db.prepare('SELECT * FROM posts WHERE id = ?').get(req.params.id);
  if (!post) return res.status(404).json({ error: 'Post not found' });

  const comments = db.prepare(
    'SELECT * FROM comments WHERE post_id = ? ORDER BY created_at ASC'
  ).all(req.params.id);

  res.json({ ...post, comments });
});

// Create a post
app.post('/api/posts', (req, res) => {
  const { title, content, author } = req.body;
  if (!title || !content) {
    return res.status(400).json({ error: 'Title and content are required' });
  }

  const result = db.prepare(
    'INSERT INTO posts (title, content, author) VALUES (?, ?, ?)'
  ).run(title, content, author || 'Anonymous');

  const post = db.prepare('SELECT * FROM posts WHERE id = ?').get(result.lastInsertRowid);
  res.status(201).json(post);
});

// Delete a post (and its comments via CASCADE)
app.delete('/api/posts/:id', (req, res) => {
  const result = db.prepare('DELETE FROM posts WHERE id = ?').run(req.params.id);
  if (result.changes === 0) return res.status(404).json({ error: 'Post not found' });
  res.status(204).send();
});

// ─── COMMENTS ───

// Add a comment to a post
app.post('/api/posts/:id/comments', (req, res) => {
  const post = db.prepare('SELECT * FROM posts WHERE id = ?').get(req.params.id);
  if (!post) return res.status(404).json({ error: 'Post not found' });

  const { body, author } = req.body;
  if (!body) return res.status(400).json({ error: 'Comment body is required' });

  const result = db.prepare(
    'INSERT INTO comments (post_id, author, body) VALUES (?, ?, ?)'
  ).run(req.params.id, author || 'Anonymous', body);

  const comment = db.prepare('SELECT * FROM comments WHERE id = ?').get(result.lastInsertRowid);
  res.status(201).json(comment);
});

// Delete a comment
app.delete('/api/comments/:id', (req, res) => {
  const result = db.prepare('DELETE FROM comments WHERE id = ?').run(req.params.id);
  if (result.changes === 0) return res.status(404).json({ error: 'Comment not found' });
  res.status(204).send();
});

// Serve frontend in production
if (process.env.NODE_ENV === 'production') {
  app.use(express.static(path.join(__dirname, '../frontend')));
}

app.listen(PORT, () => {
  console.log(`Blog API running at http://localhost:${PORT}`);
});
```

## frontend/style.css

```css
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #f0f2f5;
  color: #1a1a1a;
  line-height: 1.6;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 30px 20px;
}

h1 { text-align: center; color: #1a1a1a; margin-bottom: 30px; }

h2 { margin-bottom: 15px; color: #333; }

/* ── Forms ── */

form {
  background: white;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
  margin-bottom: 30px;
}

input, textarea {
  width: 100%;
  padding: 12px;
  margin-bottom: 12px;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  font-size: 1rem;
  font-family: inherit;
}

input:focus, textarea:focus {
  outline: none;
  border-color: #667eea;
}

textarea {
  min-height: 100px;
  resize: vertical;
}

button {
  padding: 12px 24px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}

button:hover { background: #5a6fd6; }

/* ── Post List ── */

.post-card {
  background: white;
  padding: 20px 25px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
  margin-bottom: 15px;
  cursor: pointer;
  transition: transform 0.2s;
}

.post-card:hover {
  transform: translateY(-2px);
}

.post-card h3 {
  color: #333;
  margin-bottom: 8px;
}

.post-meta {
  color: #888;
  font-size: 0.85rem;
  display: flex;
  gap: 15px;
}

/* ── Single Post View ── */

#back-btn {
  background: transparent;
  color: #667eea;
  padding: 8px 0;
  margin-bottom: 20px;
}

#back-btn:hover { text-decoration: underline; }

#post-detail {
  background: white;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
  margin-bottom: 25px;
}

#post-detail .post-meta { margin-bottom: 20px; }

.comment {
  background: #f8f9fa;
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 10px;
}

.comment-author {
  font-weight: 600;
  color: #667eea;
  font-size: 0.9rem;
}

.comment-date {
  color: #999;
  font-size: 0.8rem;
  margin-left: 10px;
}

.comment-body {
  margin-top: 5px;
  color: #555;
}

.hidden { display: none; }
```

## frontend/app.js

```javascript
const API_URL = 'http://localhost:3001';

const postForm = document.getElementById('post-form');
const postsList = document.getElementById('posts-list');
const postView = document.getElementById('post-view');
const postDetail = document.getElementById('post-detail');
const backBtn = document.getElementById('back-btn');
const commentForm = document.getElementById('comment-form');
const commentsList = document.getElementById('comments-list');
const postTitle = document.getElementById('post-title');
const postContent = document.getElementById('post-content');
const postAuthor = document.getElementById('post-author');
const commentAuthor = document.getElementById('comment-author');
const commentBody = document.getElementById('comment-body');

let currentPostId = null;

// ─── Load all posts ───

async function loadPosts() {
  const res = await fetch(`${API_URL}/api/posts`);
  const posts = await res.json();

  postsList.innerHTML = posts.map(post => `
    <div class="post-card" data-id="${post.id}">
      <h3>${escapeHtml(post.title)}</h3>
      <div class="post-meta">
        <span>By ${escapeHtml(post.author)}</span>
        <span>${post.comment_count} comments</span>
        <span>${new Date(post.created_at).toLocaleDateString()}</span>
      </div>
    </div>
  `).join('');

  document.querySelectorAll('.post-card').forEach(card => {
    card.addEventListener('click', () => loadPost(card.dataset.id));
  });
}

// ─── Load single post ───

async function loadPost(id) {
  currentPostId = id;
  const res = await fetch(`${API_URL}/api/posts/${id}`);
  const post = await res.json();

  postsList.classList.add('hidden');
  postView.classList.remove('hidden');

  postDetail.innerHTML = `
    <h2>${escapeHtml(post.title)}</h2>
    <div class="post-meta">
      <span>By ${escapeHtml(post.author)}</span>
      <span>${new Date(post.created_at).toLocaleDateString()}</span>
    </div>
    <p>${escapeHtml(post.content)}</p>
  `;

  renderComments(post.comments);
}

// ─── Render comments ───

function renderComments(comments) {
  if (comments.length === 0) {
    commentsList.innerHTML = '<p style="color:#888;">No comments yet.</p>';
    return;
  }

  commentsList.innerHTML = comments.map(c => `
    <div class="comment">
      <div>
        <span class="comment-author">${escapeHtml(c.author)}</span>
        <span class="comment-date">${new Date(c.created_at).toLocaleDateString()}</span>
      </div>
      <div class="comment-body">${escapeHtml(c.body)}</div>
    </div>
  `).join('');
}

// ─── Create Post ───

postForm.addEventListener('submit', async (e) => {
  e.preventDefault();

  await fetch(`${API_URL}/api/posts`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: postTitle.value,
      content: postContent.value,
      author: postAuthor.value || 'Anonymous'
    })
  });

  postTitle.value = '';
  postContent.value = '';
  postAuthor.value = '';
  loadPosts();
});

// ─── Add Comment ───

commentForm.addEventListener('submit', async (e) => {
  e.preventDefault();

  await fetch(`${API_URL}/api/posts/${currentPostId}/comments`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      body: commentBody.value,
      author: commentAuthor.value || 'Anonymous'
    })
  });

  commentBody.value = '';
  commentAuthor.value = '';
  loadPost(currentPostId);
});

// ─── Back button ───

backBtn.addEventListener('click', () => {
  postView.classList.add('hidden');
  postsList.classList.remove('hidden');
  currentPostId = null;
});

// ─── Helpers ───

function escapeHtml(text) {
  const div = document.createElement('div');
  div.textContent = text;
  return div.innerHTML;
}

// ─── Init ───

loadPosts();
```

## frontend/index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Blog</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>📝 Simple Blog</h1>

    <!-- Create Post Form -->
    <form id="post-form">
      <input id="post-title" placeholder="Post title" required>
      <textarea id="post-content" placeholder="Write your post..." required></textarea>
      <input id="post-author" placeholder="Your name (optional)">
      <button type="submit">Publish</button>
    </form>

    <!-- Posts List -->
    <div id="posts-list"></div>

    <!-- Single Post View (hidden by default) -->
    <div id="post-view" class="hidden">
      <button id="back-btn">← Back</button>
      <div id="post-detail"></div>
      <form id="comment-form">
        <input id="comment-author" placeholder="Your name (optional)">
        <textarea id="comment-body" placeholder="Write a comment..." required></textarea>
        <button type="submit">Comment</button>
      </form>
      <div id="comments-list"></div>
    </div>
  </div>

  <script src="app.js"></script>
</body>
</html>
```
