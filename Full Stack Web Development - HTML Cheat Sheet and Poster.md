# HTML + CSS + JavaScript Quick Reference — Printable Poster

*Designed to be printed or saved as a one-page reference. Compact enough to stick on a wall.*

---

## HTML — Every Tag You Need

### Document Structure
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Title</title>
  <link rel="stylesheet" href="style.css">
</head>
<body> ... </body>
</html>
```

### Text
```html
<h1>Heading 1</h1>  <!-- biggest -->
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>  <!-- smallest -->
<p>Paragraph</p>
<strong>Bold</strong>
<em>Italic</em>
<br>            <!-- line break -->
<hr>            <!-- horizontal line -->
```

### Links & Media
```html
<a href="url">Link</a>
<a href="url" target="_blank">New tab</a>
<a href="#id">Jump to section</a>
<img src="photo.jpg" alt="description">
```

### Lists
```html
<ul>              <!-- bullet points -->
  <li>Item</li>
</ul>
<ol>              <!-- numbered -->
  <li>Item</li>
</ol>
```

### Forms
```html
<form action="/submit" method="POST">
  <input type="text" placeholder="Name">
  <input type="email" placeholder="Email">
  <input type="password" placeholder="Password">
  <input type="number">
  <input type="checkbox"> Check me
  <input type="radio" name="g"> Option
  <textarea rows="4"></textarea>
  <select>
    <option>Option 1</option>
  </select>
  <button type="submit">Send</button>
</form>
```

### Containers
```html
<div>        <!-- block container -->
<span>       <!-- inline container -->
<header>     <!-- top of page -->
<nav>        <!-- navigation -->
<main>       <!-- main content -->
<section>    <!-- section -->
<article>    <!-- article/post -->
<aside>      <!-- sidebar -->
<footer>     <!-- bottom of page -->
```

### Tables
```html
<table>
  <tr>           <!-- row -->
    <th>Header</th>   <!-- header cell -->
    <td>Data</td>     <!-- normal cell -->
  </tr>
</table>
```

### Useful Attributes
```
id="unique"        class="multiple"
src="path"         href="url"
alt="description"  style="color:red"
data-*="value"     disabled
required           placeholder="text"
target="_blank"    rel="noopener"
```

---

## CSS — Style Cheat Sheet

### Selectors

| Pattern | Targets |
|---|---|
| `*` | Everything |
| `div` | All `<div>` |
| `.class` | `class="class"` |
| `#id` | `id="id"` |
| `div p` | `<p>` inside `<div>` |
| `div > p` | Direct child `<p>` |
| `div, p` | Both `<div>` and `<p>` |
| `[type="text"]` | `type="text"` |

### Box Model
```css
* { box-sizing: border-box; }

/* Shorthand order: top right bottom left */
margin: 10px;               /* all sides */
margin: 10px 20px;          /* top/bottom  left/right */
margin: 10px 15px 20px 25px; /* T R B L */
margin: 0 auto;             /* center block */

padding: 10px;              /* same shorthand as margin */
border: 1px solid black;
border-radius: 8px;         /* rounded corners */
border-radius: 50%;         /* circle */
```

### Flexbox (Parent)
```css
display: flex;
flex-direction: row | column;
justify-content: flex-start | center | space-between | space-around;
align-items: stretch | center | flex-start | flex-end;
flex-wrap: wrap;
gap: 10px;
```

### Flexbox (Child)
```css
flex: 1;              /* grow equally */
flex: 0 0 200px;      /* fixed at 200px */
align-self: center;
order: 2;             /* reorder (default 0) */
```

### Common Patterns
```css
/* Center text */
text-align: center;

/* Center block */
margin: 0 auto;

/* Center everything (flexbox) */
.parent { display: flex; justify-content: center; align-items: center; }

/* Card */
.card { background: white; padding: 20px; border-radius: 8px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1); }

/* Sticky header */
header { position: fixed; top: 0; width: 100%; z-index: 100; }
body { padding-top: 60px; }

/* Full page hero */
.hero { height: 100vh; display: flex; justify-content: center;
        align-items: center; }
```

### Responsive
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
```css
@media (max-width: 600px) { /* phone styles */ }
@media (max-width: 768px) { /* tablet styles */ }
@media (min-width: 1024px) { /* desktop styles */ }
```

### Units
```
px      absolute pixels
%       relative to parent
rem     relative to root font size (use for text!)
em      relative to current font size
vw      1% of viewport width
vh      1% of viewport height
fr      fraction of grid space
```

---

## JavaScript — Quick Reference

### Variables & Types
```javascript
let x = 5;              // can change
const y = 'hello';      // can't change
// Types: string, number, boolean, array, object, null, undefined
```

### Conditionals
```javascript
if (x > 5) { } else if (x === 5) { } else { }
const result = x > 5 ? 'yes' : 'no';
```

### Loops
```javascript
for (let i = 0; i < 5; i++) { }
for (const item of array) { }
array.forEach(item => { });
```

### Functions
```javascript
function name(params) { return value; }
const name = (params) => value;
```

### Arrays (Most Used)
```javascript
array.map(fn)        // transform each → new array
array.filter(fn)     // keep matches → new array
array.find(fn)       // first match
array.forEach(fn)    // loop
array.includes(x)    // check if exists
array.push(x)        // add to end
array.pop()          // remove from end
array.sort()         // sort
```

### DOM
```javascript
document.getElementById('id')
document.querySelector('.class')
el.textContent = 'text'
el.innerHTML = '<b>html</b>'
el.style.color = 'red'
el.classList.add('class')
el.classList.remove('class')
el.classList.toggle('class')
document.createElement('tag')
parent.appendChild(child)
el.remove()
el.addEventListener('click', fn)
```

### Async/Await
```javascript
async function getData() {
  try {
    const res = await fetch('/api/data');
    if (!res.ok) throw new Error('Bad response');
    return await res.json();
  } catch (err) {
    console.error(err);
  }
}
```

### Fetch
```javascript
// GET
fetch('/api/data').then(r => r.json())

// POST
fetch('/api/data', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ key: 'value' })
})
```

### Event Delegation
```javascript
parent.addEventListener('click', (e) => {
  const btn = e.target.closest('.btn');
  if (!btn) return;
  // handle click
});
```

---

## React — Component Quick Reference

```javascript
// Component (function-based)
function Card({ title, children }) {
  return <div className="card"><h2>{title}</h2>{children}</div>;
}

// Hooks
const [count, setCount] = useState(0);
useEffect(() => { fetch('/api').then(r => r.json()).then(setData); }, []);

// Conditional rendering
{isLoggedIn ? <Dashboard /> : <Login />}

// List rendering
{items.map(item => <li key={item.id}>{item.name}</li>)}

// Event handler
<button onClick={() => setCount(c => c + 1)}>+1</button>
```

---

## TypeScript — Type Quick Reference

```typescript
// Basic types
let name: string = 'Alice';
let age: number = 30;
let isDone: boolean = false;
let items: string[] = ['a', 'b'];
let mixed: any = 'whatever';  // avoid when possible

// Interfaces & Types
interface User { id: number; name: string; email?: string; }
type Status = 'active' | 'inactive';
const user: User = { id: 1, name: 'Bob' };

// Function types
function add(a: number, b: number): number { return a + b; }
const greet = (name: string): string => `Hello ${name}`;
```

---

## Tailwind CSS — Quick Patterns

```html
<!-- Layout -->
<div class="flex flex-col md:flex-row gap-4 p-4">
  <div class="flex-1 bg-white rounded-lg shadow p-6">
    <!-- card content -->
  </div>
</div>

<!-- Responsive text -->
<h1 class="text-2xl md:text-4xl font-bold text-center">Title</h1>

<!-- Buttons -->
<button class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700">
  Click
</button>

<!-- Centered container -->
<div class="max-w-4xl mx-auto px-4"></div>
```

---

## Deployment — Quick Commands

```bash
# Vercel (frontend/static)
npm i -g vercel && vercel

# Render (backend) — connect GitHub repo, set start command:
# node server.js

# Custom domain
# Vercel: Project → Domains → add domain
# Render: Settings → Custom Domain
```

---

## Express — Server Quick Reference

```javascript
const express = require('express');
const app = express();
app.use(express.json());

app.get('/path', (req, res) => res.json(data));
app.post('/path', (req, res) => res.status(201).json(data));
app.put('/path/:id', (req, res) => res.json(data));
app.delete('/path/:id', (req, res) => res.status(204).send());

app.listen(3000, () => console.log('Running'));
```

---

## SQL — Database Quick Reference

```sql
CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT);
INSERT INTO users (name) VALUES ('Alice');
SELECT * FROM users;
SELECT * FROM users WHERE id = 1;
UPDATE users SET name = 'Bob' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

---

## HTTP Status Codes

| Code | Meaning | Code | Meaning |
|---|---|---|---|
| 200 | OK | 401 | Unauthorized |
| 201 | Created | 403 | Forbidden |
| 301 | Moved | 404 | Not Found |
| 400 | Bad Request | 500 | Server Error |

---

## Git — Version Control

```bash
git init                    # start tracking
git add .                   # stage all
git commit -m "message"     # save checkpoint
git push                    # upload to GitHub
git pull                    # download from GitHub
git branch                  # list branches
git switch -c new-branch    # create & switch
git merge branch-name       # merge into current
git log --oneline           # view history
```
