# Advanced Full Stack Web Development Guide

So you've mastered the fundamentals. You can build a full stack app, deploy it, and debug it. Now it's time to go deeper — tools, patterns, and concepts that separate junior from senior developers.

---

## Table of Contents

1. [TypeScript — JavaScript with Superpowers](#1-typescript--javascript-with-superpowers)
2. [Next.js — The React Framework](#2-nextjs--the-react-framework)
3. [Tailwind CSS — Utility-First Styling](#3-tailwind-css--utility-first-styling)
4. [Authentication in Depth](#4-authentication-in-depth)
5. [Testing — Write Code You Can Trust](#5-testing--write-code-you-can-trust)
6. [Web Security — Don't Get Hacked](#6-web-security--dont-get-hacked)
7. [Performance Optimization — Speed Matters](#7-performance-optimization--speed-matters)
8. [CI/CD — Automate Everything](#8-cicd--automate-everything)
9. [Docker — Containers for Consistency](#9-docker--containers-for-consistency)
10. [WebSockets — Real-Time Communication](#10-websockets--real-time-communication)
11. [State Management in React](#11-state-management-in-react)
12. [GraphQL — A Better REST?](#12-graphql--a-better-rest)
13. [Database Hosting — Production Databases](#13-database-hosting--production-databases)
14. [Linux Basics — The Server OS](#14-linux-basics--the-server-os)
15. [Responsive Design Deep Dive](#15-responsive-design-deep-dive)
16. [Accessibility (a11y) — Build for Everyone](#16-accessibility-a11y--build-for-everyone)
17. [SEO Basics — Get Found on Google](#17-seo-basics--get-found-on-google)
18. [Package Managers Deep Dive](#18-package-managers-deep-dive)
19. [Monorepos — One Repo to Rule Them All](#19-monorepos--one-repo-to-rule-them-all)
20. [Microservices — Beyond the Monolith](#20-microservices--beyond-the-monolith)
21. [Serverless — No Servers to Manage](#21-serverless--no-servers-to-manage)
22. [Web Components — Native Reusable Components](#22-web-components--native-reusable-components)
23. [Error Tracking & Observability — Watch Your App in Production](#23-error-tracking--observability--watch-your-app-in-production)
24. [Internationalization (i18n) — Speak Your User's Language](#24-internationalization-i18n--speak-your-users-language)
25. [Background Jobs & Message Queues — Don't Make Users Wait](#25-background-jobs--message-queues--dont-make-users-wait)
26. [Feature Flags — Ship Code Without Fear](#26-feature-flags--ship-code-without-fear)
27. [Mobile Strategies — Beyond the Browser](#27-mobile-strategies--beyond-the-browser)

---

## 1. TypeScript — JavaScript with Superpowers

### What is TypeScript?

TypeScript is JavaScript **with types**. It compiles to plain JavaScript. Think of it as JS with a safety net.

```typescript
// JavaScript (no types)
function greet(name) {
  return 'Hello, ' + name;
}

// TypeScript (with types)
function greet(name: string): string {
  return 'Hello, ' + name;
}
```

The second version tells you: `name` must be a string, and the function returns a string. If you try to pass a number, TypeScript catches the error **before you run the code**.

### Why TypeScript?

| Without TypeScript | With TypeScript |
|---|---|
| `user.name` — is it a string? undefined? | `user.name` is typed as `string \| undefined` — you know to check |
| Refactoring breaks things silently | Refactoring is safe — the compiler tells you what broke |
| `data.map()` — is `data` an array? | The type says `data: string[]` — you know `.map()` works |
| IntelliSense shows generic suggestions | IntelliSense shows EXACT properties and methods |

**TypeScript doesn't make your code run faster.** It makes you **faster at writing correct code** by catching bugs at compile time instead of runtime.

### Setting Up TypeScript

```bash
mkdir ts-demo && cd ts-demo
npm init -y
npm install --save-dev typescript
npx tsc --init  # creates tsconfig.json
```

**`tsconfig.json` key settings:**
```json
{
  "compilerOptions": {
    "target": "ES2020",           // What JS version to output
    "module": "ESNext",           // Module system
    "strict": true,               // Enable all strict checks (recommended)
    "outDir": "./dist",           // Compiled JS goes here
    "rootDir": "./src",           // Your TS source files
    "esModuleInterop": true,      // Better import compatibility
    "skipLibCheck": true          // Skip checking .d.ts files (faster)
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

### Basic Types

```typescript
// Primitives
let name: string = 'Alice';
let age: number = 30;
let isActive: boolean = true;
let data: null = null;
let value: undefined = undefined;

// Arrays
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ['a', 'b'];  // generic syntax

// Objects
let user: { name: string; age: number } = { name: 'Alice', age: 30 };

// Optional properties
let config: { url: string; port?: number } = { url: 'http://localhost' };

// Union types
let id: string | number = 'abc123';
id = 456;  // OK

// Type alias
type User = { id: number; name: string; email: string };
let alice: User = { id: 1, name: 'Alice', email: 'a@b.com' };
```

### Interfaces

```typescript
interface Person {
  name: string;
  age: number;
  greet(): string;  // method signature
}

class Student implements Person {
  constructor(public name: string, public age: number) {}
  greet() { return `Hi, I'm ${this.name}`; }
}
```

**Interface vs Type:** Interfaces can be extended (merged), types cannot. Use `interface` for objects, `type` for unions/aliases.

### Generics — Type Variables

```typescript
function firstElement<T>(arr: T[]): T | undefined {
  return arr[0];
}

const num = firstElement([1, 2, 3]);      // type: number
const str = firstElement(['a', 'b']);     // type: string

// Multiple generics
function pair<A, B>(a: A, b: B): [A, B] {
  return [a, b];
}
```

Generics let you write reusable code that works with **any type** while keeping type safety.

### Type Narrowing

```typescript
function process(value: string | string[]) {
  if (Array.isArray(value)) {
    return value.join(', ');  // value is string[]
  }
  return value.toUpperCase();  // value is string
}
```

TypeScript narrows types based on checks (`typeof`, `instanceof`, `Array.isArray`, truthiness checks).

### TypeScript with Express

```typescript
import express, { Request, Response, NextFunction } from 'express';

const app = express();

interface User {
  id: number;
  name: string;
}

app.get('/api/users', (req: Request, res: Response<User[]>) => {
  const users: User[] = [{ id: 1, name: 'Alice' }];
  res.json(users);
});

// Typed request body
app.post('/api/users', (req: Request<{}, {}, { name: string }>, res: Response) => {
  const { name } = req.body;  // name is typed as string
  // ...
});
```

### TypeScript with React

```tsx
// Props interface
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';  // union + optional
}

function Button({ label, onClick, variant = 'primary' }: ButtonProps) {
  return <button className={`btn btn-${variant}`} onClick={onClick}>{label}</button>;
}

// useState with type inference
const [count, setCount] = useState(0);  // count is number

// useState with explicit type (for complex state)
const [user, setUser] = useState<User | null>(null);

// useRef
const inputRef = useRef<HTMLInputElement>(null);

// Events
function handleChange(e: React.ChangeEvent<HTMLInputElement>) {
  console.log(e.target.value);
}
```

### Why Strict Mode?

Without `strict: true`, TypeScript allows many things that defeat the purpose:

```typescript
const x = null;
console.log(x.toString());  // Runtime error! But TS won't catch it without strict

// With strict: true:
const x: null = null;
console.log(x.toString());  // ❌ Object is possibly 'null'
```

Always enable `strict: true`. It's the main reason to use TypeScript.

### Your Turn

1. Convert the Calculator project (Project 2) to TypeScript
2. Create a typed `useFetch` hook for React
3. Add TypeScript to the Blog project — type all API responses and request bodies

---

## 2. Next.js — The React Framework

### What is Next.js?

Next.js is a **React framework** that adds features React doesn't have out of the box:

| Feature | Plain React | Next.js |
|---|---|---|
| Routing | Need React Router | Built-in file-based routing |
| Server-Side Rendering (SSR) | Manual setup | Built-in |
| Static Site Generation (SSG) | Not available | Built-in |
| API routes | Need Express | Built-in API endpoints |
| Image optimization | Manual | Built-in `next/image` |
| SEO | Bad (client-side only) | Great (server-rendered HTML) |

### Rendering Strategies — Visual Comparison

```
Client:        ┌──────────┐     ┌──────────┐     ┌──────────┐
               │  Browser  │     │  Browser  │     │  Browser  │
               └─────┬─────┘     └─────▲─────┘     └────▲─────┘
                     │                 │                 │
CSR:  Browser  ──────┴── fetch JS ─────┴── render ──────┴── interactive
       loads HTML     (spinner)        (content shows)

               ┌──────────┐     ┌──────────┐     ┌──────────┐
               │  Server  │     │  Browser  │     │  Browser  │
               └────┬─────┘     └────▲─────┘     └────▲─────┘
                    │                 │                 │
SSR:  Request  ─────┴── render HTML ──┴── show page ───┴── hydrate
                   (server)         (no spinner)

               ┌──────────┐     ┌──────────┐
               │  Build   │     │   CDN    │     ┌──────────┐
               └────┬─────┘     └────▲─────┘     │  Browser  │
                    │                 │           └────▲─────┘
SSG:  Deploy  ──────┴── pre-render ───┴── serve ──────┴── instant
                   (at build)       (static HTML)

               ┌──────────┐     ┌──────────┐     ┌──────────┐
               │  Server  │     │   CDN    │     │  Browser  │
               └────┬─────┘     └────▲─────┘     └────▲─────┘
                    │                 │                 │
ISR:  Request ──────┴── render ──────┴── cache ────────┴── serve
                   (first hit)     (revalidate)       (next hits faster)
```

| Strategy | When it runs | Good for |
|---|---|---|
| **CSR** (Client-Side Rendering) | In the browser | Dashboards, logged-in apps |
| **SSR** (Server-Side Rendering) | On each request | Dynamic content, SEO needed |
| **SSG** (Static Site Generation) | At build time | Blogs, marketing pages |
| **ISR** (Incremental Static Regeneration) | On request + cached | Large sites with dynamic data |

### Pages & Routing (App Router)

Next.js uses **file-based routing**. Create files inside `app/` and they become URLs.

```
app/
├── page.js          →  /
├── layout.js        →  Wraps all pages
├── about/
│   └── page.js      →  /about
├── blog/
│   ├── page.js      →  /blog
│   └── [slug]/
│       └── page.js  →  /blog/:slug (dynamic route)
└── api/
    └── users/
        └── route.js →  /api/users
```

### Creating a Next.js App

```bash
npx create-next-app@latest my-app
cd my-app
npm run dev
```

### Server vs Client Components

Next.js has two kinds of components:

**Server Components** (default — NO `use client`):
```tsx
// app/page.tsx — this is a Server Component
async function Page() {
  const data = await fetch('https://api.example.com/data');
  const posts = await data.json();

  return (
    <div>
      {posts.map(post => <Post key={post.id} post={post} />)}
    </div>
  );
}
```
- Run on the server
- Can be `async` (fetch data directly)
- Cannot use `useState`, `useEffect`, or event handlers
- Send ONLY the rendered HTML to the client (smaller bundles, better SEO)

**Client Components** (opt in with `'use client'`):
```tsx
'use client';

import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```
- Run in the browser
- Can use hooks and event handlers
- Bundle is sent to the client

**Rule of thumb:** Make everything a Server Component by default. Add `'use client'` only when you need interactivity.

### Data Fetching

```tsx
// Server Component — fetch directly
async function BlogPage() {
  const res = await fetch('https://api.example.com/posts', {
    next: { revalidate: 3600 }  // Revalidate cache every hour
  });
  const posts = await res.json();

  return <div>{/* render */}</div>;
}
```

### API Routes

Create `app/api/items/route.ts`:

```typescript
import { NextResponse } from 'next/server';

export async function GET() {
  const items = await db.query('SELECT * FROM items');
  return NextResponse.json(items);
}

export async function POST(request: Request) {
  const body = await request.json();
  const result = await db.query('INSERT INTO items ...');
  return NextResponse.json(result, { status: 201 });
}
```

### Layouts

```tsx
// app/layout.tsx — wraps ALL pages
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html>
      <body>
        <nav>{/* global nav */}</nav>
        {children}
        <footer>{/* global footer */}</footer>
      </body>
    </html>
  );
}
```

### Static Site Generation

```tsx
// app/blog/[slug]/page.tsx
export async function generateStaticParams() {
  const posts = await fetch('https://api.example.com/posts').then(r => r.json());
  return posts.map(post => ({ slug: post.slug }));
}

async function BlogPost({ params }: { params: { slug: string } }) {
  const post = await fetch(`https://api.example.com/posts/${params.slug}`).then(r => r.json());
  return <article>{post.content}</article>;
}
```

Next.js pre-generates HTML for every `slug` at build time. The result: blazing fast pages with perfect SEO.

### Your Turn

1. Convert the Blog project from the guide to a Next.js app
2. Use Server Components for the post list, Client Components for comment forms
3. Add an API route for creating comments
4. Deploy to Vercel (one command: `npx vercel`)

---

## 3. Tailwind CSS — Utility-First Styling

### What is Tailwind?

Instead of writing custom CSS:

```css
.card {
  background: white;
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}
```

You write classes directly in HTML:

```html
<div class="bg-white rounded-xl p-5 shadow-md">
```

Tailwind provides **thousands of utility classes**. You compose them like Lego blocks.

### Why Tailwind?

| Problem | Solution |
|---|---|
| Naming things (`.card-header-wrapper-inner`) | You don't — just use utility classes |
| CSS file grows endlessly | Styles are colocated with HTML |
| Changing one style breaks another | Each utility class does ONE thing |
| Media queries require separate blocks | Responsive prefixes: `md:flex`, `lg:text-2xl` |

### Setup

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

**tailwind.config.js:**
```javascript
module.exports = {
  content: ['./src/**/*.{html,js,jsx,ts,tsx}'],
  theme: { extend: {} },
  plugins: [],
};
```

**Add to your CSS:**
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Core Concepts

**Spacing:** `p-4` (padding: 16px), `m-2` (margin: 8px), `gap-6` (gap: 24px)
**Numbers:** 0=0, 1=4px, 2=8px, 3=12px, 4=16px, 5=20px, 6=24px, 8=32px, 10=40px, 12=48px, 16=64px, 20=80px, 24=96px

**Flexbox:**
```html
<div class="flex items-center justify-between gap-4">
  <div class="flex-1">Left</div>
  <div>Right</div>
</div>
```

**Grid:**
```html
<div class="grid grid-cols-3 gap-6">
  <div class="col-span-2">Wide</div>
  <div>Narrow</div>
</div>
```

**Responsive:**
```html
<div class="text-base md:text-lg lg:text-xl p-4 md:p-8">
  <!-- text is 16px on mobile, 18px on tablet, 20px on desktop -->
  <!-- padding is 16px on mobile, 32px on desktop -->
</div>
```

Breakpoints: `sm` (640px), `md` (768px), `lg` (1024px), `xl` (1280px), `2xl` (1536px)

**Hover & States:**
```html
<button class="bg-blue-500 hover:bg-blue-700 active:bg-blue-900 disabled:opacity-50">
  Click me
</button>
```

**Dark Mode:**
```html
<div class="bg-white dark:bg-gray-900 text-black dark:text-white">
```

**Colors:** `text-red-500`, `bg-green-200`, `border-blue-700`
**Numbers:** 50 (lightest), 100, 200, 300, 400, 500 (default), 600, 700, 800, 900 (darkest)

### Building a Card

```html
<div class="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-shadow">
  <img class="w-full h-48 object-cover" src="..." alt="">
  <div class="p-6">
    <h3 class="text-xl font-semibold text-gray-900 mb-2">Card Title</h3>
    <p class="text-gray-600 mb-4">Card description text here.</p>
    <button class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors">
      Learn More
    </button>
  </div>
</div>
```

This is a complete card component — no CSS file needed.

### Customizing Tailwind

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: '#667eea',
        'brand-dark': '#5a6fd6',
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
      },
    },
  },
};
```

Now you can use `bg-brand`, `text-brand-dark`, `font-sans`.

### Your Turn

1. Rebuild the Portfolio project using ONLY Tailwind classes (no custom CSS)
2. Convert the Weather App to Tailwind
3. Add dark mode to the Portfolio using Tailwind's `dark:` prefix

---

## 4. Authentication in Depth

### What Authentication Covers

Auth is the **most implemented feature** in production web apps. It involves:

1. **Registration** — creating an account
2. **Login** — verifying identity
3. **Session management** — keeping the user logged in
4. **Authorization** — controlling what they can do
5. **Security** — protecting passwords, tokens, and data

### Password Hashing

Never store passwords as plain text. Use **bcrypt**:

```javascript
const bcrypt = require('bcryptjs');

// Register
const salt = await bcrypt.genSalt(12);  // 12 rounds — takes ~300ms
const hash = await bcrypt.hash(password, salt);
// Store `hash` in database

// Login
const match = await bcrypt.compare(password, storedHash);
```

**Why not just encrypt?** Hashing is one-way. If the database is stolen, hashes can't be reversed to passwords (unlike encryption).

### JWT — JSON Web Tokens

A JWT is a self-contained token that proves identity. It has three parts:

```
header.payload.signature
```

### JWT Authentication Flow

```
                        ┌─────────────────────────────────────┐
                        │            Your Server               │
                        │  ┌─────────┐    ┌────────────────┐  │
   ┌──────────┐         │  │  Login  │    │   Middleware    │  │
   │  Browser │──POST───┼─►│ /auth   │    │  verify JWT     │  │
   │          │email+pwd│  │         │    │  on each req    │  │
   │          │         │  └───┬─────┘    └───────▲────────┘  │
   │          │         │      │                  │           │
   │          │◄──JWT───┼──────┘   create JWT     │           │
   │          │  token  │  with {userId, role}     │           │
   │          │         │                          │           │
   │          │──GET────┼── header: ───────────────┘           │
   │          │  /posts │  Authorization: Bearer <JWT>         │
   │          │         │                                      │
   │          │◄──JSON──┼── posts (if valid JWT)               │
   └──────────┘         └─────────────────────────────────────┘

   1. Login ──► Server creates JWT ──► Browser stores it
   2. Request ──► Browser sends JWT in header ──► Server verifies
   3. Verified ──► Server processes request ──► Returns data
   4. Expired ──► Browser redirects to login
```

```javascript
const jwt = require('jsonwebtoken');

// Create token (login)
const token = jwt.sign(
  { userId: user.id, role: user.role },
  process.env.JWT_SECRET,
  { expiresIn: '7d' }
);

// Verify token (protected routes)
try {
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
  req.user = decoded;
} catch (err) {
  res.status(401).json({ error: 'Invalid token' });
}
```

**JWT best practices:**
- Store JWT in an `httpOnly` cookie (not localStorage) — prevents XSS theft
- Set `expiresIn` to something reasonable (15 min to 7 days)
- Rotate the secret key periodically
- Never include sensitive data in the payload (it's base64-encoded, not encrypted)

### HTTP-Only Cookies (Recommended)

```javascript
// Login — set cookie
res.cookie('token', token, {
  httpOnly: true,       // Cannot be read by JavaScript
  secure: true,         // HTTPS only
  sameSite: 'strict',   // CSRF protection
  maxAge: 7 * 24 * 60 * 60 * 1000  // 7 days
});
res.json({ user });

// Middleware to check auth
function auth(req, res, next) {
  const token = req.cookies.token;
  if (!token) return res.status(401).json({ error: 'Not logged in' });
  try {
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ error: 'Invalid token' });
  }
}
```

### Session-Based Auth (Alternative)

Instead of JWTs, store sessions in the database:

```javascript
// Login
req.session.userId = user.id;
// Express-session stores this in memory/database and sends a cookie
```

**JWT vs Sessions:**
| JWT | Sessions |
|---|---|
| No database lookup (fast) | Database lookup per request |
| Cannot be revoked easily | Can revoke by deleting session |
| Stateless — scales horizontally | Stateful — need shared session store |
| Good for APIs | Good for traditional server-rendered apps |

### OAuth — Login with Google/GitHub

Use a library like **Passport.js** or **NextAuth.js**:

```bash
npm install passport passport-google-oauth20
```

```javascript
passport.use(new GoogleStrategy({
  clientID: process.env.GOOGLE_CLIENT_ID,
  clientSecret: process.env.GOOGLE_CLIENT_SECRET,
  callbackURL: '/auth/google/callback'
}, (accessToken, refreshToken, profile, done) => {
  // Find or create user from profile
  done(null, user);
}));
```

**The flow:** User clicks "Login with Google" → redirected to Google → Google asks for permission → redirected back → you get user info.

### Role-Based Authorization

```javascript
function requireRole(role) {
  return (req, res, next) => {
    if (req.user.role !== role) {
      return res.status(403).json({ error: 'Forbidden' });
    }
    next();
  };
}

// Protect routes
app.delete('/api/posts/:id', auth, requireRole('admin'), deletePost);
```

### Your Turn

1. Add JWT auth to the Blog project (register, login, protected routes)
2. Only the post author can edit/delete their post
3. Add a "Login with GitHub" button using Passport.js

---

## 5. Testing — Write Code You Can Trust

### Why Test?

- **Prevent regressions** — new code doesn't break old features
- **Document behavior** — tests describe what your code should do
- **Confidence** — refactor without fear
- **Better design** — testable code is usually well-structured

### Types of Tests

```
        ┌──────────────────────┐
        │   E2E (Cypress)      │  ← Slow, expensive, high confidence
        ├──────────────────────┤
        │   Integration        │  ← Medium: tests how components work together
        ├──────────────────────┤
        │   Unit (Vitest)      │  ← Fast, cheap, many tests
        └──────────────────────┘
```

### Unit Tests with Vitest

```bash
npm install --save-dev vitest
```

```javascript
// math.js
export function add(a, b) { return a + b; }
export function divide(a, b) { if (b === 0) throw new Error('Cannot divide by zero'); return a / b; }

// math.test.js
import { describe, it, expect } from 'vitest';
import { add, divide } from './math';

describe('add', () => {
  it('adds two numbers', () => {
    expect(add(2, 3)).toBe(5);
  });
  it('handles negative numbers', () => {
    expect(add(-1, -1)).toBe(-2);
  });
});

describe('divide', () => {
  it('divides two numbers', () => {
    expect(divide(10, 2)).toBe(5);
  });
  it('throws on division by zero', () => {
    expect(() => divide(10, 0)).toThrow('Cannot divide by zero');
  });
});
```

### Testing Async Code

```javascript
// api.js
export async function fetchUser(id) {
  const res = await fetch(`/api/users/${id}`);
  if (!res.ok) throw new Error('Not found');
  return res.json();
}

// api.test.js
import { describe, it, expect, vi } from 'vitest';

describe('fetchUser', () => {
  it('returns user data on success', async () => {
    global.fetch = vi.fn().mockResolvedValue({
      ok: true,
      json: () => Promise.resolve({ id: 1, name: 'Alice' })
    });

    const user = await fetchUser(1);
    expect(user.name).toBe('Alice');
  });

  it('throws on error', async () => {
    global.fetch = vi.fn().mockResolvedValue({ ok: false });
    await expect(fetchUser(1)).rejects.toThrow('Not found');
  });
});
```

### Integration Tests with Supertest (Express)

```bash
npm install --save-dev supertest
```

```javascript
// server.js (refactored to export app)
const app = express();
// ... all routes ...
module.exports = app;

// server.test.js
const request = require('supertest');
const app = require('./server');

describe('POST /api/users', () => {
  it('creates a user', async () => {
    const res = await request(app)
      .post('/api/users')
      .send({ name: 'Alice', email: 'a@b.com' });

    expect(res.status).toBe(201);
    expect(res.body.name).toBe('Alice');
  });

  it('rejects missing name', async () => {
    const res = await request(app)
      .post('/api/users')
      .send({ email: 'a@b.com' });

    expect(res.status).toBe(400);
  });
});
```

### Testing React Components

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom jsdom
```

```tsx
// Counter.tsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(c => c + 1)}>+1</button>
    </div>
  );
}

// Counter.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { describe, it, expect } from 'vitest';
import Counter from './Counter';

describe('Counter', () => {
  it('starts at 0', () => {
    render(<Counter />);
    expect(screen.getByText('Count: 0')).toBeDefined();
  });

  it('increments on click', () => {
    render(<Counter />);
    fireEvent.click(screen.getByText('+1'));
    expect(screen.getByText('Count: 1')).toBeDefined();
  });
});
```

### E2E Tests with Playwright

```bash
npm install --save-dev @playwright/test
npx playwright install
```

```javascript
// tests/login.spec.js
import { test, expect } from '@playwright/test';

test('user can log in', async ({ page }) => {
  await page.goto('http://localhost:3000/login');
  await page.fill('#email', 'user@test.com');
  await page.fill('#password', 'password123');
  await page.click('button[type="submit"]');
  await expect(page.locator('.dashboard')).toBeVisible();
});
```

### What to Test

| Test | What | Example |
|---|---|---|
| **Unit** | Individual functions | `add(2, 3)` should return `5` |
| **Integration** | Features working together | POST to create user, GET to verify |
| **Component** | UI renders correctly | Button click updates count |
| **E2E** | Full user flow | Login → create post → see it in feed |

### Your Turn

1. Add unit tests for the Calculator JS logic
2. Add integration tests for the Blog API
3. Add a component test for a React button
4. Add an E2E test that creates a blog post and verifies it appears

---

## 6. Web Security — Don't Get Hacked

### The Most Common Attacks

| Attack | What it does | How to prevent |
|---|---|---|
| **XSS** | Injects malicious scripts into your page | Escape output, CSP headers |
| **CSRF** | Tricks user into making unwanted requests | SameSite cookies, CSRF tokens |
| **SQL Injection** | Injects malicious SQL queries | Parameterized queries, ORM |
| **MITM** | Intercepts traffic between client and server | HTTPS only |
| **DDOS** | Overwhelms your server with requests | Rate limiting, CDN |

### XSS — Cross-Site Scripting

XSS is when an attacker injects a `<script>` tag into your page. For example, a comment field:

```javascript
// ❌ DANGEROUS: direct innerHTML
comment.innerHTML = userInput;
// If userInput is: <script>alert('hacked')</script>
// Your page runs that script!

// ✅ SAFE: textContent
comment.textContent = userInput;
// Displays the literal text, doesn't execute it
```

**Three levels of XSS prevention:**

1. **Always use `textContent`** not `innerHTML` when displaying user data
2. **If you MUST use innerHTML**, sanitize with DOMPurify:
   ```bash
   npm install dompurify
   ```
   ```javascript
   import DOMPurify from 'dompurify';
   element.innerHTML = DOMPurify.sanitize(userInput);
   ```
3. **Set Content Security Policy (CSP) headers**:
   ```javascript
   app.use((req, res, next) => {
     res.setHeader('Content-Security-Policy',
       "default-src 'self'; script-src 'self' https://apis.example.com"
     );
     next();
   });
   ```

### CSRF — Cross-Site Request Forgery

CSRF tricks a logged-in user into making a request they didn't intend:

1. User is logged into `bank.com`
2. User visits `evil.com` which has: `<img src="bank.com/transfer?amount=1000&to=attacker">`
3. Browser sends the request with the user's cookies — bank thinks user authorized it

**Prevention:**

**SameSite cookies** (easiest):
```javascript
res.cookie('token', token, { sameSite: 'strict' });
```

**CSRF tokens** (traditional):
```javascript
const crypto = require('crypto');
const csrfToken = crypto.randomBytes(32).toString('hex');
// Send to frontend, frontend includes it in forms/headers
```

### SQL Injection

```javascript
// ❌ DANGEROUS: string concatenation
db.query(`SELECT * FROM users WHERE id = ${req.params.id}`);
// Attacker sends: 1; DROP TABLE users; --
// Query becomes: SELECT * FROM users WHERE id = 1; DROP TABLE users; --

// ✅ SAFE: parameterized query
db.query('SELECT * FROM users WHERE id = ?', [req.params.id]);
```

**Always use parameterized queries (`?` placeholders) or an ORM.** Never concatenate user input into SQL.

### More Security Headers

Use the **helmet** package to set secure HTTP headers:

```bash
npm install helmet
```

```javascript
const helmet = require('helmet');
app.use(helmet());
// Sets: X-Content-Type-Options, X-Frame-Options, Strict-Transport-Security, etc.
```

### Rate Limiting

Prevent brute force attacks:

```bash
npm install express-rate-limit
```

```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000,  // 15 minutes
  max: 100,                    // 100 requests per window
  message: 'Too many requests'
});

app.use('/api', limiter);

// Stricter for login
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 5,
  message: 'Too many login attempts'
});
app.post('/api/login', loginLimiter, loginHandler);
```

### Input Validation

Never trust user input. Validate everything:

```bash
npm install express-validator
```

```javascript
const { body, validationResult } = require('express-validator');

app.post('/api/users',
  body('email').isEmail(),
  body('age').isInt({ min: 0, max: 150 }),
  body('name').isLength({ min: 1, max: 100 }).trim(),
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    // Process request
  }
);
```

### Dependency Audit

```bash
npm audit                  # Check for known vulnerabilities
npm audit fix              # Auto-fix patches
npm update                 # Update all packages
```

Run `npm audit` before every deploy.

### Your Turn

1. Add helmet and express-rate-limit to the Blog project
2. Add input validation to all POST/PUT endpoints
3. Replace any `innerHTML` usage with `textContent` or DOMPurify
4. Add a Content Security Policy header

---

## 7. Performance Optimization — Speed Matters

### Why Performance Matters

- **53% of users leave** if a page takes >3 seconds to load
- **1 second delay** = 7% fewer conversions
- Google ranks faster sites higher

### Measuring Performance

```bash
# Lighthouse — built into Chrome DevTools
# Run a Lighthouse report: Audits tab → Generate report

# Web Vitals API (in browser)
new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    console.log(entry.name, entry.value);
  }
}).observe({ type: 'largest-contentful-paint', buffered: true });
```

Key metrics: **LCP** (Largest Contentful Paint — <2.5s), **FID** (First Input Delay — <100ms), **CLS** (Cumulative Layout Shift — <0.1)

### Frontend Optimization

**1. Code Splitting** — Don't load what you don't need:

```javascript
// ❌ BAD: imports everything, even if user never visits /admin
import AdminPanel from './AdminPanel';

// ✅ GOOD: only loads when needed
const AdminPanel = React.lazy(() => import('./AdminPanel'));

<Suspense fallback={<Loading />}>
  {showAdmin && <AdminPanel />}
</Suspense>
```

**2. Image Optimization**
- Use `<img loading="lazy">` — native lazy loading
- Use WebP format (smaller than JPEG/PNG)
- Responsive images with `srcset`:
  ```html
  <img src="photo-800.jpg"
       srcset="photo-400.jpg 400w, photo-800.jpg 800w, photo-1200.jpg 1200w"
       sizes="(max-width: 600px) 400px, 800px">
  ```
- In Next.js: use `next/image` (automatic optimization)

**3. Bundle Analysis**

```bash
npm install --save-dev vite-bundle-visualizer
npx vite-bundle-visualizer
```

This shows what's taking up space in your JavaScript bundle. Find and remove large libraries.

**4. Debouncing** — Don't run expensive code on every keystroke:

```javascript
function debounce(fn, delay = 300) {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => fn(...args), delay);
  };
}

const handleSearch = debounce(async (query) => {
  const results = await fetch(`/api/search?q=${query}`);
  // Update UI
}, 300);
```

### Backend Optimization

**1. Database Indexing**

```sql
-- ❌ SLOW: full table scan
SELECT * FROM posts WHERE author = 'Alice';

-- ✅ FAST: uses index
CREATE INDEX idx_posts_author ON posts(author);
SELECT * FROM posts WHERE author = 'Alice';
```

Indexes make reads faster, but writes slightly slower. Index columns used in `WHERE`, `JOIN`, and `ORDER BY`.

**2. Pagination** — Never send all data at once:

```javascript
// ❌ BAD: loads everything
app.get('/api/posts', (req, res) => {
  const posts = db.prepare('SELECT * FROM posts').all();
  res.json(posts);
});

// ✅ GOOD: paginated
app.get('/api/posts', (req, res) => {
  const page = parseInt(req.query.page) || 1;
  const limit = parseInt(req.query.limit) || 20;
  const offset = (page - 1) * limit;

  const posts = db.prepare('SELECT * FROM posts LIMIT ? OFFSET ?').all(limit, offset);
  res.json({ posts, page, hasMore: posts.length === limit });
});
```

**3. Caching**

```javascript
const cache = new Map();

app.get('/api/expensive-data', async (req, res) => {
  const cacheKey = 'expensive-data';
  if (cache.has(cacheKey)) {
    return res.json(cache.get(cacheKey));
  }

  const data = await expensiveOperation();
  cache.set(cacheKey, data);
  setTimeout(() => cache.delete(cacheKey), 60000);  // Expire after 1 min
  res.json(data);
});
```

For production, use **Redis** instead of in-memory cache.

### CDN — Content Delivery Network

A CDN (like Cloudflare, Fastly) stores copies of your static files on servers around the world. When a user in Tokyo visits your site, they get files from a Tokyo server — not from your origin server in the US.

**Cache headers** tell the CDN how long to keep files:

```javascript
// Static assets — cache forever (they have unique filenames)
app.use('/static', express.static('public', {
  maxAge: '1y',
  immutable: true
}));

// HTML — short cache or no cache
app.use('/', (req, res) => {
  res.set('Cache-Control', 'no-cache');
  res.sendFile('index.html');
});
```

### Lighthouse Score Targets

| Metric | Good | Needs Work | Poor |
|---|---|---|---|
| Performance | 90+ | 50-89 | <50 |
| Accessibility | 90+ | 50-89 | <50 |
| Best Practices | 90+ | 50-89 | <50 |
| SEO | 90+ | 50-89 | <50 |

### Your Turn

1. Run Lighthouse on your Portfolio or Blog project
2. Implement lazy loading for images
3. Add database indexing to the Blog project
4. Add pagination to the Blog API
5. Set up proper cache headers in Express

---

## 8. CI/CD — Automate Everything

### What is CI/CD?

**CI** (Continuous Integration): Every time you push code, it automatically runs tests.
**CD** (Continuous Deployment): If tests pass, automatically deploy to production.

```
                    CI Pipeline                          CD Pipeline
   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
   │  git     │   │  Build   │   │   Test   │   │ Deploy   │   │  Live!   │
   │  push    │──►│          │──►│          │──►│          │──►│          │
   │          │   │ npm ci   │   │ vitest   │   │ vercel   │   │ Production│
   └──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘
        │              │              │               │              │
        ▼              ▼              ▼               ▼              ▼
   Triggered      Install deps   Run all tests    Deploy if       Users see
   by push                       & lint           tests pass      new version

                        ┌─── FAIL ───► Fix code ───► Push again
                        │
   git push ──► build ──┤
                        │
                        └─── PASS ──► deploy ──► production

   ## Branch Strategy
   main ─────► auto-deploy to production
   develop ──► auto-deploy to staging
   feature/* ─► run tests only (no deploy)
```

### GitHub Actions

Create `.github/workflows/ci.yml` in your repo:

```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm test
      - run: npm run lint
```

### Adding Deployment

Deploy to Vercel automatically on push:

```yaml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm test
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.ORG_ID }}
          vercel-project-id: ${{ secrets.PROJECT_ID }}
```

### Environment Secrets in GitHub

Settings → Secrets and variables → Actions → Add secrets:
- `VERCEL_TOKEN` — from Vercel account settings
- `VERCEL_ORG_ID` — from Vercel project settings
- `VERCEL_PROJECT_ID` — from Vercel project settings

### Test Coverage

Add coverage reporting to your CI:

```yaml
- run: npm test -- --coverage
- uses: davelosert/vitest-coverage-report-action@v2
```

### Your Turn

1. Create a GitHub repo for the Blog project
2. Add a CI workflow that runs tests on every push
3. Add a CD workflow that deploys to Vercel

---

## 9. Docker — Containers for Consistency

### What is Docker?

Docker packages your app and all its dependencies into a **container**. A container runs the same way on your laptop, your coworker's laptop, and the production server.

```
┌─────────────────┐
│  Your App        │
├─────────────────┤
│  Node.js 20      │
├─────────────────┤
│  Alpine Linux    │  ← Minimal OS
├─────────────────┤
│  Docker Engine   │
└─────────────────┘
```

### VM vs Containers

```
┌─────────────────────────┐  ┌─────────────────────────┐
│      Virtual Machine    │  │       Container         │
├─────────────────────────┤  ├─────────────────────────┤
│  ┌──────────────────┐   │  │  ┌──────────────────┐   │
│  │     App A        │   │  │  │     App A        │   │
│  ├──────────────────┤   │  │  ├──────────────────┤   │
│  │  Full Guest OS   │   │  │  │  App Dependencies│   │
│  │  (Ubuntu, 4GB+)  │   │  │  │  (Node, Python)  │   │
│  ├──────────────────┤   │  │  ├──────────────────┤   │
│  │    Hypervisor    │   │  │  │   Docker Engine   │   │
│  ├──────────────────┤   │  │  ├──────────────────┤   │
│  │  Host OS (Linux) │   │  │  │ Host OS (Linux)  │   │
│  └──────────────────┘   │  └─────────────────────────┘
└─────────────────────────┘

  ┌──────────┬──────────────────────┬──────────────────────┐
  │          │        VM            │      Container       │
  ├──────────┼──────────────────────┼──────────────────────┤
  │  Size    │   1-10 GB            │   10-200 MB          │
  │  Boot    │   30-60 seconds      │   < 1 second         │
  │  OS      │   Full OS per VM     │   Shares host OS     │
  │  Memory  │   Heavy (GBs)        │   Light (MBs)        │
  │  Density │   1-5 per server     │   10-100 per server  │
  │  Safety  │   Strong isolation   │   Process isolation   │
  └──────────┴──────────────────────┴──────────────────────┘
```

### Dockerfile

```dockerfile
# Use official Node.js image
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy package files first (leverage Docker cache)
COPY package*.json ./
RUN npm ci --production

# Copy source code
COPY . .

# Expose port
EXPOSE 3000

# Start app
CMD ["node", "server.js"]
```

### .dockerignore

```
node_modules
.git
.env
*.log
```

### Building & Running

```bash
docker build -t my-app .
docker run -p 3000:3000 -e DATABASE_URL=... my-app
```

### Docker Compose (Multiple Services)

```yaml
# docker-compose.yml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
    depends_on:
      - db

  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: pass
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

Start everything with one command:
```bash
docker-compose up
```

### Why Docker Matters

- **No "it works on my machine"** problems
- **Consistent environment** across dev, test, production
- **Easy scaling** — run multiple container instances
- **Isolation** — each service in its own container

### Your Turn

1. Create a Dockerfile for the Notes App
2. Add a docker-compose.yml with the app + PostgreSQL
3. Test that `docker-compose up` starts everything

---

## 10. WebSockets — Real-Time Communication

### What WebSockets Solve

HTTP is **request-response**: you ask, the server answers. This doesn't work for real-time features:

- Chat: "Did I get a new message?" (requires polling — wasteful)
- Notifications: "Did someone like my post?" (same problem)
- Live updates: "Did the stock price change?"

**WebSocket** keeps a persistent connection open. Both sides can send data at any time.

```
HTTP Polling (wasteful):
   Client  ──► "Any messages?" ──► Server
           ◄── "No" ◄─────────────
           ──► "Any messages?" ──►
           ◄── "No" ◄─────────────
           ──► "Any messages?" ──►
           ◄── "Here's the msg" ◄─
                                          ▲ 95% of requests are wasted

WebSocket (efficient):
   Client  ◄══════════════════════► Server
           │  Connection stays open       │
           │  Server pushes new msg ──────►│
           │  Server pushes another ──────►│
           │  Client sends reply ─────────►│
           │  Bidirectional, instant       │
```

### WebSocket Handshake

```
Client                          Server
  │                                │
  │── HTTP Upgrade Request ───────►│
  │   GET /chat HTTP/1.1          │
  │   Upgrade: websocket          │
  │   Connection: Upgrade         │
  │   Sec-WebSocket-Key: abc123   │
  │                                │
  │◄── HTTP 101 Switching ────────│
  │   Upgrade: websocket          │
  │   Connection: Upgrade         │
  │   Sec-WebSocket-Accept: xyz   │
  │                                │
  │══════ WebSocket Established ═══►
  │  Both sides can now send       │
  │  messages at any time          │
  │                                │
  │── "Hello server!" ────────────►│
  │◄── "Hello client!" ───────────│
  │── [typing...] ────────────────►│
  │◄── [new message notification] ─│
  │                                │
  │── [close] ────────────────────►│
  │══════ Connection Closed ═══════│
```

### Socket.IO

Socket.IO is the most popular WebSocket library for Node.js:

```bash
npm install socket.io
```

**Server:**
```javascript
const http = require('http');
const { Server } = require('socket.io');

const server = http.createServer(app);
const io = new Server(server, {
  cors: { origin: 'http://localhost:5173' }
});

io.on('connection', (socket) => {
  console.log('User connected:', socket.id);

  // Receive message from client
  socket.on('chat message', (msg) => {
    // Send to ALL connected clients (including sender)
    io.emit('chat message', msg);
    // Or send to everyone EXCEPT sender:
    // socket.broadcast.emit('chat message', msg);
  });

  socket.on('disconnect', () => {
    console.log('User disconnected:', socket.id);
  });
});

server.listen(3000);
```

**Client:**
```html
<script src="/socket.io/socket.io.js"></script>
<script>
  const socket = io('http://localhost:3000');

  // Send message
  document.getElementById('form').addEventListener('submit', (e) => {
    e.preventDefault();
    socket.emit('chat message', input.value);
    input.value = '';
  });

  // Receive message
  socket.on('chat message', (msg) => {
    const item = document.createElement('li');
    item.textContent = msg;
    messages.appendChild(item);
  });
</script>
```

### Rooms

```javascript
// Join a room
socket.join('room-123');

// Send to everyone in a room (not all clients)
io.to('room-123').emit('new message', msg);
```

### Your Turn

1. Build a real-time chat app with Socket.IO
2. Add rooms (multiple chat channels)
3. Show who's online
4. Add typing indicators

---

## 11. State Management in React

### The Problem

As React apps grow, passing props through many levels gets painful:

```
Prop Drilling (bad):
   App
    │
    ▼
  Header  ──►  passes user + setUser down
    │
    ▼
 UserMenu ──►  passes user + setUser down
    │
    ▼
  Avatar  ──►  finally uses user

  5 components in the chain just to pass data
  Rename user → currentUser? Update EVERY intermediate component

Global State (good):
   ┌──────────────────────────────────────┐
   │            Store / Context            │
   │  { user, setUser, theme, lang, ... }  │
   └────────┬──────────┬─────────┬────────┘
            │          │         │
            ▼          ▼         ▼
         Header    UserMenu   Sidebar
                    │
                    ▼
                 Avatar
   Any component reads from store directly
   No prop drilling, no intermediate hops
```

```tsx
function App() {
  const [user, setUser] = useState(null);
  return <Header user={user} setUser={setUser} />;
}
function Header({ user, setUser }) {
  return <UserMenu user={user} setUser={setUser} />;
}
function UserMenu({ user, setUser }) {
  return <Avatar user={user} setUser={setUser} />;
}
// This is "prop drilling" — ugly and hard to maintain
```

### Solution 1: Context API

```tsx
// AuthContext.tsx
import { createContext, useContext, useState, ReactNode } from 'react';

interface AuthContextType {
  user: User | null;
  login: (email: string, password: string) => Promise<void>;
  logout: () => void;
}

const AuthContext = createContext<AuthContextType | null>(null);

export function AuthProvider({ children }: { children: ReactNode }) {
  const [user, setUser] = useState<User | null>(null);

  const login = async (email: string, password: string) => {
    const res = await fetch('/api/login', { method: 'POST', body: JSON.stringify({ email, password }) });
    const data = await res.json();
    setUser(data.user);
  };

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) throw new Error('useAuth must be inside AuthProvider');
  return context;
}
```

Usage — no prop drilling:
```tsx
function UserMenu() {
  const { user, logout } = useAuth();  // Direct access
  return <div>{user.name} <button onClick={logout}>Logout</button></div>;
}
```

**When to use Context:** For global state that doesn't change often (auth, theme, language).

**When NOT to use Context:** For frequently changing state (forms, real-time data) — it re-renders ALL consumers on every change.

### Solution 2: Zustand (Simple & Fast)

```bash
npm install zustand
```

```javascript
import { create } from 'zustand';

const useStore = create((set) => ({
  count: 0,
  increase: () => set((state) => ({ count: state.count + 1 })),
  decrease: () => set((state) => ({ count: state.count - 1 })),
  reset: () => set({ count: 0 }),
}));

function Counter() {
  const count = useStore((state) => state.count);
  const increase = useStore((state) => state.increase);
  return <button onClick={increase}>{count}</button>;
}
```

Zustand is simpler than Redux, doesn't need providers, and only re-renders components that use the changed piece of state.

### Solution 3: Redux (Heavy, but Industry Standard)

```bash
npm install @reduxjs/toolkit react-redux
```

```javascript
// store.js
import { configureStore, createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => { state.value += 1 },
    decrement: (state) => { state.value -= 1 },
  },
});

export const { increment, decrement } = counterSlice.actions;
export const store = configureStore({ reducer: { counter: counterSlice.reducer } });
```

```jsx
// App.jsx
import { Provider, useSelector, useDispatch } from 'react-redux';
import { increment } from './store';

function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}

function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();
  return <button onClick={() => dispatch(increment())}>{count}</button>;
}
```

### Which One to Use?

| Tool | Complexity | Best for |
|---|---|---|
| useState + lifting state up | None | Simple, local state |
| Context API | Low | Auth, theme, language |
| Zustand | Low-Medium | Most apps |
| Redux Toolkit | High | Large enterprise apps |

**Start with useState. Graduate to Context or Zustand. Only use Redux if you need it.**

### Your Turn

1. Replace prop drilling in a project with Context
2. Add Zustand to the React project for cart/basket state
3. Compare: which approach was easier?

---

## 12. GraphQL — A Better REST?

### REST Problems

```
GET /api/users          →  Returns ALL user data (maybe more than needed)
GET /api/users/1/posts  →  Makes 2 requests when you need user + posts together
POST /api/users         →  Over-fetches or under-fetches
```

### GraphQL — One Endpoint, Ask for Exactly What You Need

```graphql
# What you ask for
query {
  user(id: 1) {
    name
    email
    posts {
      title
    }
  }
}
```

```json
// What you get back
{
  "data": {
    "user": {
      "name": "Alice",
      "email": "alice@test.com",
      "posts": [
        { "title": "Hello World" }
      ]
    }
  }
}
```

One request, exactly the data you need, nested relationships included.

### Apollo Server (Backend)

```bash
npm install @apollo/server graphql
```

```javascript
import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';

const typeDefs = `#graphql
  type User {
    id: ID!
    name: String!
    posts: [Post]
  }

  type Post {
    id: ID!
    title: String!
    content: String!
  }

  type Query {
    user(id: ID!): User
    posts: [Post]
  }
`;

const resolvers = {
  Query: {
    user: (_, { id }) => db.users.find(u => u.id === id),
    posts: () => db.posts,
  },
  User: {
    posts: (user) => db.posts.filter(p => p.userId === user.id),
  },
};

const server = new ApolloServer({ typeDefs, resolvers });
const { url } = await startStandaloneServer(server);
console.log(`GraphQL ready at ${url}`);
```

### Apollo Client (Frontend)

```bash
npm install @apollo/client graphql
```

```jsx
import { ApolloClient, InMemoryCache, gql, useQuery } from '@apollo/client';

const client = new ApolloClient({
  uri: 'http://localhost:4000',
  cache: new InMemoryCache(),
});

const GET_USER = gql`
  query GetUser($id: ID!) {
    user(id: $id) {
      name
      email
      posts { title }
    }
  }
`;

function UserProfile({ userId }) {
  const { loading, error, data } = useQuery(GET_USER, {
    variables: { id: userId },
  });

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return <div>{data.user.name}</div>;
}
```

### REST vs GraphQL

| REST | GraphQL |
|---|---|
| Multiple endpoints (`/api/users`, `/api/posts`) | Single endpoint (`/graphql`) |
| Server decides what data to send | Client decides what data to ask for |
| Over-fetching common | Exactly what you ask for |
| Versioned (`/v1/api/users`) | Evolvable (no versioning needed) |
| Caching is easy (URL-based) | Caching is harder |
| Simple to understand | Requires learning GraphQL syntax |

### Your Turn

1. Convert the Blog API to GraphQL
2. Write a query that gets posts + their comments in one request
3. Add a mutation to create a new post

---

## 13. Database Hosting — Production Databases

### Why Not SQLite in Production?

SQLite is great for development — single file, no setup. But in production:

- **Render deletes the file** on every restart
- **Can't scale** — one writer at a time
- **No access control** beyond file permissions
- **No backup** solution built in

### Supabase — PostgreSQL + Auth + Storage

Supabase is an open-source Firebase alternative. It gives you:

- PostgreSQL database (not just storage — real SQL)
- Built-in authentication
- File storage
- Real-time subscriptions
- REST API from your tables

**Setup:**
```javascript
import { createClient } from '@supabase/supabase-js';
const supabase = createClient(process.env.SUPABASE_URL, process.env.SUPABASE_ANON_KEY);

// Query
const { data, error } = await supabase.from('posts').select('*');

// Insert
const { data, error } = await supabase.from('posts').insert({ title: 'Hello' });

// Real-time
supabase.channel('posts').on('postgres_changes', { event: 'INSERT', schema: 'public', table: 'posts' },
  (payload) => console.log('New post:', payload.new)
).subscribe();
```

### Neon — Serverless PostgreSQL

Neon is PostgreSQL designed for serverless. Key features:

- **Free tier** — 500MB, always-on
- **Branching** — instant database branches (like Git branches)
- **Connection pooling** — handles many concurrent connections from serverless functions
- **`psql` compatible** — same SQL you already know

```javascript
const { Pool } = require('pg');
const pool = new Pool({ connectionString: process.env.NEON_DATABASE_URL });
```

### MongoDB Atlas — NoSQL in the Cloud

For when you don't need strict schemas:

```javascript
const { MongoClient } = require('mongodb');
const client = new MongoClient(process.env.MONGODB_URI);
await client.connect();
const db = client.db('myapp');
const posts = db.collection('posts');

const result = await posts.insertOne({ title: 'Hello', tags: ['web', 'js'] });
const allPosts = await posts.find().toArray();
```

### Which to Choose?

| Database | Type | Best for |
|---|---|---|
| **Supabase** | PostgreSQL + Auth | Full stack apps, need auth built-in |
| **Neon** | Serverless PostgreSQL | Serverless functions, want raw SQL |
| **MongoDB Atlas** | NoSQL | Flexible schemas, JSON-like data |
| **PlanetScale** | MySQL compatible | Horizontal scaling |
| **Railway** | PostgreSQL + hosting | All-in-one platform |

### Your Turn

1. Create a free Supabase project
2. Migrate the Blog project from SQLite to Supabase
3. Add a real-time subscription — new posts appear instantly

---

## 14. Linux Basics — The Server OS

### Why Linux?

Most servers run Linux. Knowing basic Linux commands is essential for deployment and debugging.

### The Terminal

```bash
pwd              # Print working directory (where am I?)
ls               # List files
ls -la           # List all files (including hidden) with details
cd /path         # Change directory
mkdir dirname    # Create directory
rm file          # Delete file
rm -rf dir       # Delete directory (careful — no undo!)
cp src dest      # Copy file
mv src dest      # Move/rename file
cat file         # Print file contents
less file        # View file with paging (q to quit)
head -n 20 file  # First 20 lines
tail -n 20 file  # Last 20 lines
tail -f file     # Watch file for changes (logs!)
```

### SSH — Connect to a Server

```bash
ssh user@your-server.com
ssh -i ~/.ssh/my-key.pem user@your-server.com  # With key file
```

Once connected, you're on a remote machine. Every command runs there.

### File Permissions

```bash
chmod 755 script.sh   # rwxr-xr-x — owner can write, others can read/execute
chmod 600 key.pem     # rw------- — only owner can read
chown user:group file  # Change owner
```

### Process Management

```bash
ps aux                    # List all running processes
kill PID                  # Stop a process
kill -9 PID               # Force stop (SIGKILL)
top                       # Interactive process viewer
htop                      # Better than top (install first)
```

### Systemd (Service Management)

```bash
sudo systemctl status nginx     # Check if nginx is running
sudo systemctl restart nginx    # Restart nginx
sudo systemctl enable myapp     # Start on boot
```

### Viewing Logs

```bash
journalctl -u myapp       # Systemd logs for your app
journalctl -u myapp -f    # Follow (live) logs
```

### Your Turn

1. SSH into a free AWS EC2 instance or DigitalOcean droplet
2. Install Node.js on it
3. Copy your app and run it
4. Set it up as a systemd service so it restarts on crash

---

## 15. Responsive Design Deep Dive

### Beyond Media Queries

You already know `@media (max-width: 768px)`. Now let's go deeper.

### Container Queries

Instead of responding to the viewport, respond to the **parent container**:

```css
.card-container {
  container-type: inline-size;
}

@container (max-width: 400px) {
  .card {
    flex-direction: column;
  }
}
```

This is powerful for reusable components that appear in different-width containers.

### Clamp() — Fluid Typography

```css
/* Font size: minimum 16px, preferred 4vw, maximum 32px */
h1 {
  font-size: clamp(1rem, 4vw, 2rem);
}

/* Width: minimum 300px, preferred 80%, maximum 1200px */
.container {
  width: clamp(300px, 80%, 1200px);
}
```

No media queries needed for sizing!

### Modern CSS Layout Patterns

**Holy Grail Layout (header, nav, main, aside, footer):**
```css
body {
  display: grid;
  grid-template-rows: auto 1fr auto;
  grid-template-columns: 200px 1fr 200px;
  grid-template-areas:
    "header header header"
    "nav    main   aside"
    "footer footer footer";
  min-height: 100vh;
}
```

**Auto-fill grid (responsive without media queries):**
```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}
```

### Mobile-First vs Desktop-First

**Mobile-first** (recommended):
```css
/* Base styles = mobile */
.container { padding: 10px; }

/* Tablet */
@media (min-width: 768px) {
  .container { padding: 20px; }
}

/* Desktop */
@media (min-width: 1024px) {
  .container { padding: 40px; }
}
```

Start with the smallest screen, add complexity as screen grows.

### Your Turn

1. Refactor your Portfolio to use `clamp()` for typography
2. Use `auto-fill` + `minmax()` for the project cards instead of a fixed grid
3. Add a container query to a reusable card component

---

## 16. Accessibility (a11y) — Build for Everyone

### Why Accessibility

- **15% of the world** has some disability (WHO)
- Accessible sites rank better in Google
- It's often the law (ADA, Section 508)
- Better accessibility = better UX for everyone

### Semantic HTML — The Foundation

```html
<!-- ❌ BAD: all divs -->
<div class="nav">
  <div class="nav-item" onclick="goHome()">Home</div>
</div>

<!-- ✅ GOOD: semantic -->
<nav>
  <a href="/">Home</a>
</nav>
```

Semantic elements (`<nav>`, `<main>`, `<article>`, `<button>`, `<form>`, `<label>`) give screen readers free information about your page structure.

### ARIA — Accessible Rich Internet Applications

When HTML isn't enough:

```html
<!-- Custom checkbox (not a real checkbox) -->
<div
  role="checkbox"
  aria-checked="false"
  tabindex="0"
  aria-label="Accept terms"
  onclick="toggleCheckbox()"
  onkeydown="if(event.key===' ') toggleCheckbox()"
></div>
```

**Key ARIA rules:**
1. Don't use ARIA if you can use a native HTML element
2. `role` tells screen readers what an element is
3. `aria-label` provides a text name when there's no visible label
4. `aria-live` announces dynamic content changes
5. `aria-hidden="true"` hides decorative elements from screen readers

### Keyboard Navigation

```javascript
// Handle keyboard events for custom interactive elements
button.addEventListener('keydown', (e) => {
  if (e.key === 'Enter' || e.key === ' ') {
    e.preventDefault();
    activateButton();
  }
});
```

**Native `<button>` elements already handle Enter/Space.** Use them unless you have a compelling reason not to.

### Focus Management

```css
/* Visible focus indicator (required for keyboard users) */
:focus-visible {
  outline: 3px solid #667eea;
  outline-offset: 2px;
}

/* Remove focus for mouse users only */
:focus:not(:focus-visible) {
  outline: none;
}
```

### Color Contrast

Text must have sufficient contrast against its background:

- **Normal text:** contrast ratio ≥ 4.5:1
- **Large text (18px+ bold or 24px+):** ≥ 3:1

Check with: https://webaim.org/resources/contrastchecker/

### Screen Reader Testing

- Turn on VoiceOver (Mac): `Cmd + F5`
- Turn on NVDA (Windows): free screen reader
- Navigate with `Tab`, `Shift+Tab`, arrow keys
- Can you use the app without seeing the screen?

### Your Turn

1. Run an accessibility audit on a project (Lighthouse → Accessibility)
2. Add `aria-labels` to all icon-only buttons
3. Ensure all form inputs have `<label>` elements
4. Fix any color contrast issues
5. Test keyboard navigation through your app

---

## 17. SEO Basics — Get Found on Google

### How Google Sees Your Site

Google "crawls" your pages, reads the HTML, and indexes the content. If your site is all JavaScript with no server-rendered HTML, Google might not see your content at all.

### Meta Tags

```html
<head>
  <title>My Blog — Web Development Tutorials</title>
  <meta name="description" content="Learn web development from scratch. Tutorials on HTML, CSS, JavaScript, React, and more.">
  <meta name="robots" content="index, follow">
  <link rel="canonical" href="https://example.com/page">
</head>
```

### Open Graph (Social Media Preview)

```html
<meta property="og:title" content="My Blog Post">
<meta property="og:description" content="A great post about...">
<meta property="og:image" content="https://example.com/thumbnail.jpg">
<meta property="og:url" content="https://example.com/post">
<meta name="twitter:card" content="summary_large_image">
```

### Semantic HTML for SEO

Search engines understand page structure through headings:

```html
<h1>Page Title (only one per page)</h1>
  <h2>Section</h2>
    <h3>Subsection</h3>
  <h2>Another Section</h2>
```

### Sitemaps

```xml
<!-- public/sitemap.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://example.com/about</loc>
    <priority>0.8</priority>
  </url>
</urlset>
```

Submit to Google Search Console.

### SEO Checklist

```
[ ] Descriptive <title> tag (each page unique)
[ ] Meta description (160 chars, compelling)
[ ] Only one <h1> per page
[ ] Proper heading hierarchy (h1 → h2 → h3)
[ ] Image alt attributes
[ ] Semantic HTML (nav, main, article)
[ ] Fast page load (Lighthouse)
[ ] Mobile-friendly
[ ] HTTPS
[ ] Sitemap submitted
[ ] robots.txt
```

### Your Turn

1. Add meta tags to a project
2. Create a sitemap
3. Run a Lighthouse SEO audit and fix the issues
4. Submit your site to Google Search Console

---

## 18. Package Managers Deep Dive

### npm — Node Package Manager

You already use npm. But there's more:

```bash
npm outdated              # Show outdated packages
npm update                # Update within semver range
npm audit                 # Security audit
npm audit fix             # Auto-fix vulnerabilities
npm ci                    # Clean install (CI environments — faster, exact versions)
npm ls --depth=0          # Show top-level installed packages
npm why <package>         # Why is this package installed?
```

### package-lock.json

This file ensures **reproducible builds**. It locks the exact version of every dependency (including nested dependencies). Always commit it to git.

### Semantic Versioning (SemVer)

```
"express": "^4.18.2"
           │  │  │
           │  │  └── Patch (v4.18.3 — bug fixes, safe)
           │  └──── Minor (v4.19.0 — new features, safe)
           └─────── Major (v5.0.0 — breaking changes!)
```

- `^4.18.2` — Accept minor + patch updates (safe)
- `~4.18.2` — Accept only patch updates (very safe)
- `4.18.2` — Exact version only (no updates)
- `*` — Any version (dangerous — don't do this)

### Yarn

```bash
npm install --global yarn

yarn init -y
yarn add express
yarn add --dev vitest
yarn install  # Equivalent to npm ci
```

Yarn is faster than npm (parallel downloads, better caching). Modern npm (v7+) has caught up significantly.

### pnpm

```bash
npm install --global pnpm

pnpm init
pnpm add express
pnpm install
```

pnpm uses **hard links** — packages are stored once globally, linked into projects. This saves massive disk space in monorepos.

| Feature | npm | Yarn | pnpm |
|---|---|---|---|
| Speed | Good | Better | Best |
| Disk space | Normal | Normal | Minimal (shared store) |
| Monorepo support | Workspaces | Workspaces | Built-in |
| Popularity | Most popular | Very popular | Growing fast |

### Your Turn

1. Run `npm audit` on a project and fix vulnerabilities
2. Try `pnpm` on a new project
3. Set up npm workspaces for a multi-package project

---

## 19. Monorepos — One Repo to Rule Them All

### What is a Monorepo?

A monorepo is a single repository containing **multiple projects** (frontend, backend, shared library, etc.).

```
my-app/
├── packages/
│   ├── shared/        # Shared types/utilities
│   │   └── package.json
│   ├── frontend/      # React app
│   │   └── package.json
│   └── backend/       # Express API
│       └── package.json
├── package.json       # Root (workspaces config)
└── pnpm-workspace.yaml
```

### Why Monorepo?

- **Shared code** — types, utilities, configs live in one place
- **Atomic commits** — change frontend + backend in a single commit
- **Consistent tooling** — one ESLint config, one TypeScript config
- **Simpler CI** — one pipeline builds everything

### Setting Up with npm Workspaces

```json
// Root package.json
{
  "workspaces": ["packages/*"]
}
```

```bash
npm install  # Installs all dependencies for all packages
```

Create `packages/shared/index.ts`:
```typescript
export interface User {
  id: number;
  name: string;
}
```

Reference it from `packages/frontend/package.json`:
```json
{
  "dependencies": {
    "shared": "workspace:*"
  }
}
```

```typescript
import { User } from 'shared';
```

### Turborepo — Build Orchestration

```bash
npm install --save-dev turbo
```

```json
// Root package.json
{
  "scripts": {
    "build": "turbo run build",
    "dev": "turbo run dev"
  }
}
```

```json
// turbo.json
{
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],  // Build dependencies first
      "outputs": ["dist/**"]
    },
    "dev": {
      "cache": false
    }
  }
}
```

Turborepo caches build outputs and only rebuilds changed packages. Huge time savings in CI.

### Your Turn

1. Convert the Blog project into a monorepo: `packages/frontend`, `packages/backend`, `packages/shared`
2. Move shared types to `packages/shared`
3. Use Turborepo to orchestrate builds

---

## 20. Microservices — Beyond the Monolith

### Monolith vs Microservices

```
┌══════════════════╗     ┌────────┐  ┌────────┐  ┌──────────┐  ┌──────────────┐
║    MONOLITH     ║     │ Auth   │  │ Posts  │  │ Comments  │  │ Notifications│
║                 ║     │Service │  │Service │  │ Service   │  │   Service    │
║  ┌───────────┐  ║     └───┬────┘  └───┬────┘  └────┬─────┘  └──────┬───────┘
║  │  Auth     │  ║         │           │            │               │
║  ├───────────┤  ║         └─────┬─────┴──────┬─────┘               │
║  │  Posts    │  ║               │            │                     │
║  ├───────────┤  ║         ┌─────▼────────────▼─────────────────────┘
║  │ Comments  │  ║         │         API Gateway / Message Queue
║  ├───────────┤  ║         └─────▲────────────▲─────────────────────┐
║  │ Notific.  │  ║               │            │                     │
║  ├───────────┤  ║         ┌─────┴────┐  ┌────┴─────┐         ┌────┴──────┐
║  │  DB       │  ║         │ Auth DB  │  │ Posts DB │         │Comments DB│
║  └───────────┘  ║         └──────────┘  └──────────┘         └───────────┘
║                 ║
║  One big app    ║     ┌────────────────────────────────────────────────────┐
║  One deploy     ║     │  Each service: independent codebase, deploy, DB   │
║  One DB         ║     │  Communicate via HTTP REST or message queues      │
║  Scale all or   ║     │  Scale only what needs scaling                    │
║  nothing        ║     └────────────────────────────────────────────────────┘
╚══════════════════╝

| Monolith | Microservices |
|---|---|
| Single codebase, one deploy | Multiple services, each deployed independently |
| Simple to develop | Complex orchestration |
| Hard to scale (scale everything) | Scale only what's needed |
| One database | One database per service |
| Simple testing | Integration testing is harder |

### When to Use Microservices

**Use them when:**
- Your team has 10+ developers
- Different parts of the app need different scaling (e.g., auth is rarely called, image processing is heavy)
- You need to use different tech stacks for different services

**Don't use them when:**
- You're a solo developer or small team
- Your app is simple (a monolith is fine)
- You haven't deployed a monolith in production yet

### Communication Between Services

**HTTP REST:**
```javascript
// Posts service calls User service
const user = await fetch(`http://user-service:3001/api/users/${post.authorId}`);
```

**Message Queue (RabbitMQ, Redis Pub/Sub):**
```javascript
// When a post is created, emit event
await redis.publish('post:created', JSON.stringify(post));

// Email service listens
redis.subscribe('post:created', (msg) => {
  sendNotificationEmail(JSON.parse(msg));
});
```

### Your Turn

1. Split the Blog project into two services: Posts API + Comments API
2. Make them communicate via HTTP
3. Add Docker Compose to run both services

---

## 21. Serverless — No Servers to Manage

### What is Serverless?

Serverless means you write functions, and the cloud provider runs them on demand. You don't manage servers — you upload code and it runs when triggered.

### Traditional vs Serverless

```
Traditional Server (always on):      Serverless (on demand):

┌──────────────────────────┐        ┌──────────────────────────┐
│      Your Server          │        │     Cloud Provider       │
│  ┌────────────────────┐  │        │                          │
│  │  Your App running   │  │        │  ┌──┐  ┌──┐  ┌──┐       │
│  │  24/7, even when   │  │        │  │f1│  │f2│  │f3│       │
│  │  no one visits      │  │        │  └──┘  └──┘  └──┘       │
│  └────────────────────┘  │        │   │     │     │           │
│  You pay: $20/month      │        │   └──┬──┘     │           │
│  Even at 3AM with        │        │      │        │           │
│  zero users              │        │  ┌────▼────────▼──┐       │
└──────────────────────────┘        │  │   API Gateway   │       │
                                    │  └─────▲──────────┘       │
                                    │        │                  │
┌──────────────────────────┐        │  ┌─────┴─────┐            │
│  What if traffic spikes?  │        │  │  Request   │            │
│                          │        │  └───────────┘            │
│  ┌──┐ ┌──┐ ┌──┐         │        │   │  │  │                 │
│  │  │ │  │ │  │  CRASH   │        │   ▼  ▼  ▼                 │
│  └──┘ └──┘ └──┘         │        │  ┌──┐ ┌──┐ ┌──┐          │
│  Too many users,         │        │  │f1│ │f2│ │f3│  SCALES!  │
│  server can't handle     │        │  └──┘ └──┘ └──┘          │
└──────────────────────────┘        │  Auto-scales instantly    │
                                    │  You pay per execution    │
                                    └──────────────────────────┘

┌──────────────────────┬───────────────────┬───────────────────┐
│                      │  Traditional      │   Serverless      │
├──────────────────────┼───────────────────┼───────────────────┤
│  Server management   │  You manage it    │  Provider manages  │
│  Scaling             │  Manual/limited   │  Auto-scales       │
│  Cost when idle      │  You pay anyway   │  Zero (no calls)   │
│  Cold start          │  Always ready     │  First call is slow│
│  Max execution time  │  Unlimited        │  Usually 10-30s    │
│  Best for            │  Steady traffic   │  Spiky/unpredictable│
└──────────────────────┴───────────────────┴───────────────────┘
```

### Vercel Functions

```javascript
// api/hello.js — deployed on Vercel
export default function handler(req, res) {
  res.json({ message: 'Hello from serverless!' });
}
```

Deploy to Vercel → it becomes `https://your-app.vercel.app/api/hello`.

### AWS Lambda

```javascript
exports.handler = async (event) => {
  const body = JSON.parse(event.body);
  const result = await db.query('INSERT INTO items ...');
  return {
    statusCode: 201,
    body: JSON.stringify(result),
  };
};
```

### Edge Functions

Edge functions run on CDN nodes (closest to the user), not in one central region. This means **near-zero latency** globally.

```javascript
// Next.js Edge Middleware — runs on every request (before the page)
export function middleware(request) {
  const country = request.geo.country;
  const response = NextResponse.next();

  if (country === 'US') {
    response.cookies.set('currency', 'USD');
  }

  return response;
}
```

### Serverless vs Traditional

| Traditional | Serverless |
|---|---|
| Server runs 24/7 | Function runs on demand |
| Pay for uptime | Pay for execution |
| Scale manually or with auto-scaling | Scales instantly to zero or infinity |
| Cold start = 0 (always running) | Cold start = ~100ms-1s (first request) |
| Session state in memory | Stateless (use DB/external cache) |

### Your Turn

1. Convert the Weather App API to a serverless function on Vercel
2. Add Edge middleware that redirects users to a country-specific page

---

## 22. Web Components — Native Browser Components

### What Are Web Components?

Web Components let you create **reusable custom HTML elements** using browser-native APIs — no framework needed.

```html
<script type="module">
  class MyButton extends HTMLElement {
    connectedCallback() {
      this.innerHTML = `<button style="background: blue; color: white; border: none; padding: 10px;">
        ${this.getAttribute('label') || 'Click me'}
      </button>`;
    }
  }

  customElements.define('my-button', MyButton);
</script>

<!-- Use anywhere in HTML -->
<my-button label="Hello!"></my-button>
```

### Custom Elements

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: 'open' });  // Shadow DOM — encapsulated styles
  }

  connectedCallback() {
    const name = this.getAttribute('name');
    const email = this.getAttribute('email');

    this.shadowRoot.innerHTML = `
      <style>
        .card { border: 1px solid #ddd; padding: 16px; border-radius: 8px; }
        h2 { margin: 0 0 8px; }
      </style>
      <div class="card">
        <h2>${name}</h2>
        <p>${email}</p>
      </div>
    `;
  }
}

customElements.define('user-card', UserCard);
```

```html
<user-card name="Alice" email="alice@example.com"></user-card>
```

### Shadow DOM

The Shadow DOM provides **style encapsulation** — styles inside the component don't leak out, and outside styles don't leak in.

### HTML Templates

```html
<template id="user-card-template">
  <style>
    .card { border: 1px solid #ddd; padding: 16px; border-radius: 8px; }
    h2 { margin: 0 0 8px; color: #333; }
  </style>
  <div class="card">
    <h2 id="name"></h2>
    <p id="email"></p>
  </div>
</template>

<script>
  class UserCard extends HTMLElement {
    constructor() {
      super();
      const template = document.getElementById('user-card-template');
      this.attachShadow({ mode: 'open' })
        .appendChild(template.content.cloneNode(true));
    }

    connectedCallback() {
      this.shadowRoot.getElementById('name').textContent = this.getAttribute('name');
      this.shadowRoot.getElementById('email').textContent = this.getAttribute('email');
    }
  }
</script>
```

### Web Components vs React

| Web Components | React |
|---|---|
| Browser native (no framework) | Library (need to install) |
| No state management | useState, useEffect, etc. |
| No reactivity | Automatic re-rendering |
| Can be used in ANY framework | Only in React |
| Good for design systems | Good for complex UIs |

**Best use:** Create a design system with Web Components, then use it in React, Vue, and plain HTML.

### Your Turn

1. Create a custom `<loading-spinner>` Web Component
2. Create a `<tool-tip>` component with Shadow DOM
3. Use these components in a plain HTML page

---

## 23. Error Tracking & Observability — Watch Your App in Production

You've deployed your app. People are using it. Everything is great.

Then your phone blows up. Users can't log in. But when you check the app, it works fine for you.

**This is the worst feeling in software.** An invisible bug that only affects some users, sometimes, for reasons unknown.

Error tracking and observability are your insurance against this nightmare. They watch your app in production, record what breaks, and tell you exactly what happened.

### Logging — The Bare Minimum

Every app should have logs. Every. Single. One.

**Bad logging:**
```javascript
// ❌ What broke? No idea.
try {
  await processPayment(userId, amount);
} catch (error) {
  console.log("Something went wrong");
}
```

**Good logging:**
```javascript
// ✅ Now you can actually debug it
try {
  await processPayment(userId, amount);
} catch (error) {
  console.error("Payment failed:", {
    userId,
    amount,
    error: error.message,
    stack: error.stack,
    timestamp: new Date().toISOString(),
  });
}
```

**Log levels matter:**
```javascript
console.log("User logged in");       // Info — normal operation
console.warn("Rate limit hit", ip);  // Warning — might need attention
console.error("DB connection lost"); // Error — definitely needs fixing
```

#### Structured Logging — Logs Machines Can Read

Plain text logs are fine for humans. But when you have 10,000 log lines per minute, you need STRUCTURE — logs in a format that tools can parse:

```javascript
// Instead of:
console.log(`User ${userId} paid $${amount} at ${new Date()}`);

// Do:
console.log(JSON.stringify({
  event: "payment_completed",
  userId,
  amount,
  currency: "USD",
  timestamp: new Date().toISOString(),
  duration: 342, // how long it took in ms
}));
```

**Logging libraries for Node.js:**
- **pino** — Fastest JSON logger (12x faster than console.log)
- **winston** — Most popular, very configurable
- **bunyan** — JSON-only, simple API

```javascript
const pino = require('pino');
const logger = pino({ level: process.env.LOG_LEVEL || 'info' });

logger.info({ userId, action: 'login' }, 'User logged in');
logger.warn({ ip, attempts: 5 }, 'Rate limit approaching');
logger.error({ err: error, userId }, 'Payment failed');
```

### Sentry — The Gold Standard for Error Tracking

Sentry is free for small projects and catches errors you'd never find otherwise.

```bash
npm install @sentry/node @sentry/tracing
```

```javascript
const Sentry = require('@sentry/node');

Sentry.init({
  dsn: process.env.SENTRY_DSN,  // Get this from sentry.io
  environment: process.env.NODE_ENV,
  tracesSampleRate: 1.0,  // Record 100% of traces in dev, less in prod
});

// Sentry automatically catches uncaught exceptions

// For handled errors, tell Sentry explicitly:
try {
  riskyOperation();
} catch (error) {
  Sentry.captureException(error);
  // Still handle the error gracefully for the user
  res.status(500).send("Something went wrong");
}

// Add context to help debug:
Sentry.setUser({ id: userId, email: user.email });
Sentry.setTag("payment_method", "stripe");
Sentry.setExtra("cart_items", cartItems.length);
```

**What Sentry gives you:**
- Stack trace with line numbers (from your source maps)
- Browser, OS, device info
- User actions leading up to the error
- Environment and release version
- Automatic grouping of identical errors

**Magic trick — source maps:** Sentry shows you the original TypeScript/React code, not minified garbage. Set it up once:

```javascript
Sentry.init({
  dsn: process.env.SENTRY_DSN,
  integrations: [new Sentry.Integrations.Http({ tracing: true })],
});
// Upload source maps during build
// npx @sentry/cli sourcemaps upload --release=1.0.0 ./dist
```

### Performance Monitoring — Beyond Just Errors

Your app works. But is it fast?

```javascript
const transaction = Sentry.startTransaction({
  name: "checkout-flow",
  op: "checkout",
});

// Measure specific operations
const span = transaction.startChild({ op: "database", description: "getUser" });
const user = await db.findUser(userId);
span.finish();

const span2 = transaction.startChild({ op: "payment", description: "chargeCard" });
await stripe.charges.create({ amount, currency: 'usd' });
span2.finish();

transaction.finish();
```

**Key metrics to watch:**
- **Apdex** — Application Performance Index (% of requests under a threshold)
- **p50/p95/p99 latency** — 50% of requests are X fast, 95% are Y fast
- **Error rate** — percentage of requests that error
- **Throughput** — requests per second

### Uptime Monitoring — Is Your Site Even Up?

Error tracking catches bugs. Uptime monitoring catches "the whole site is down."

**Free options:**
- **Better Uptime** — 5-minute checks, free tier, phone/Slack/email alerts
- **Pingdom** — Industry standard, paid
- **Upptime** — Open source, runs on GitHub Actions (free)
- **Checkly** — Browser-based checks (actually loads your page)

```yaml
# upptime.yml — GitHub Actions workflow
name: Uptime Check
on:
  schedule:
    - cron: "*/5 * * * *"  # Every 5 minutes
jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - run: curl -f https://your-app.com/api/health || exit 1
```

### Health Endpoints — Let Monitoring Tools Check Inside

Create a `/api/health` endpoint that reports your app's internal state:

```javascript
app.get('/api/health', async (req, res) => {
  const health = {
    status: 'ok',
    timestamp: new Date().toISOString(),
    uptime: process.uptime(),
    memory: process.memoryUsage(),
    database: 'unknown',
  };

  try {
    await db.query('SELECT 1');
    health.database = 'connected';
  } catch (error) {
    health.status = 'degraded';
    health.database = 'disconnected';
  }

  res.status(health.status === 'ok' ? 200 : 503).json(health);
});
```

### Alerting — Don't Watch the Dashboards, Let Them Watch You

Set up alerts that actually matter:

| Alert | When | Why |
|---|---|---|
| Error rate spike | 5%+ errors in 5 minutes | Something is broken for everyone |
| p95 latency spike | > 2 seconds for 5 minutes | Something is slow (DB? API?) |
| Uptime check failed | 2 consecutive failures | Site might be down |
| Disk space | < 10% remaining | Logs filling up the server |
| Memory usage | > 90% for 10 minutes | Memory leak |

**Don't over-alert.** If everything is an emergency, nothing is. Start with 3 alerts: error rate, latency, and uptime. Add more as you learn what matters.

### Your Turn

1. Add structured logging (pino or winston) to your app
2. Set up Sentry for error tracking (free tier is fine)
3. Create a `/api/health` endpoint
4. Set up uptime monitoring with Better Uptime or Upptime
5. Intentionally crash your app — see the error appear in Sentry

---

## 24. Internationalization (i18n) — Speak Your User's Language

Your app works in English. Congratulations — you've reached about 20% of the world's population.

**The other 80% would rather use your app in Spanish, Arabic, Japanese, or French.** And if they can't, they'll find a competitor who supports their language.

Internationalization (i18n — there are 18 letters between 'i' and 'n') is the process of making your app work in multiple languages. Not just translating text — formatting dates, numbers, currencies, plurals, and even layout direction.

### The Wrong Way — Copy/Paste Pages

```javascript
// ❌ The "I hate my life" approach
if (lang === 'es') {
  res.send('<h1>Bienvenido a mi sitio</h1>');
} else if (lang === 'fr') {
  res.send('<h1>Bienvenue sur mon site</h1>');
} else {
  res.send('<h1>Welcome to my site</h1>');
}
```

This works for 3 languages across 1 page. For a real app with 10 languages and 50 pages, this becomes a nightmare of spaghetti code.

### The Right Way — Translation Files

Separate your text from your code:

```javascript
// lang/en.json
{
  "welcome": "Welcome to my site",
  "greeting": "Hello, {name}!",
  "items_count": "You have {count} items | You have one item | You have {count} items",
  "login": "Log in",
  "logout": "Log out",
  "created_at": "Created on {date, date, medium}"
}
```

```javascript
// lang/es.json
{
  "welcome": "Bienvenido a mi sitio",
  "greeting": "¡Hola, {name}!",
  "items_count": "Tienes {count} artículos | Tienes 1 artículo | Tienes {count} artículos",
  "login": "Iniciar sesión",
  "logout": "Cerrar sesión",
  "created_at": "Creado el {date, date, medium}"
}
```

```javascript
// Usage in your app
import i18next from 'i18next';

i18next.t('welcome');           // "Bienvenido a mi sitio" (if lang=es)
i18next.t('greeting', { name: 'Ana' });  // "¡Hola, Ana!"
i18next.t('items_count', { count: 5 });  // "Tienes 5 artículos"
```

### i18next — The Industry Standard

i18next is the most popular i18n library for JavaScript. It works with React, Vue, Next.js, Node.js, and even vanilla JS.

```bash
npm install i18next react-i18next
```

```javascript
// i18n.js — your i18n config
import i18n from 'i18next';
import { initReactI18next } from 'react-i18next';
import en from './lang/en.json';
import es from './lang/es.json';
import ar from './lang/ar.json';

i18n.use(initReactI18next).init({
  resources: { en: { translation: en }, es: { translation: es }, ar: { translation: ar } },
  lng: navigator.language.split('-')[0], // Detect browser language
  fallbackLng: 'en',                      // Show English if translation missing
  interpolation: { escapeValue: false },  // React already escapes
});
```

```javascriptx
// React component
import { useTranslation } from 'react-i18next';

function Welcome() {
  const { t, i18n } = useTranslation();

  return (
    <div>
      <h1>{t('welcome')}</h1>
      <p>{t('greeting', { name: user.name })}</p>
      <button onClick={() => i18n.changeLanguage('es')}>Español</button>
      <button onClick={() => i18n.changeLanguage('en')}>English</button>
    </div>
  );
}
```

### Plurals — It's Not "1 items"

English has two plural forms: singular (1 item) and plural (0 or 2+ items). Other languages have more — Arabic has 6.

```json
{
  "items": "{{count}} item",
  "items_plural": "{{count}} items"
}
```

i18next handles plural rules automatically (it knows which languages need which forms):

```json
{
  "items": "{{count}} item",
  "items_plural": "{{count}} items",
  "items_interval": "(0){No items}(1){One item}(2-4){A few items}(5-){Many items}"
}
```

### Date, Time, and Number Formatting

Dates are different everywhere:
- US: March 14, 2026 — 03/14/2026
- UK: 14 March 2026 — 14/03/2026
- Japan: 2026年3月14日

```javascript
const date = new Date("2026-03-14");

// Intl.DateTimeFormat is built into every browser
new Intl.DateTimeFormat('en-US').format(date);  // "3/14/2026"
new Intl.DateTimeFormat('en-GB').format(date);  // "14/03/2026"
new Intl.DateTimeFormat('ja-JP').format(date);  // "2026/3/14"
new Intl.DateTimeFormat('ar-SA').format(date);  // "١٤/٣/٢٠٢٦"

// Change ICU format in i18next:
t('created_at', { date: new Date() });
// en: "Created on Mar 14, 2026"
// es: "Creado el 14 mar 2026"
```

**Numbers too:**
```javascript
new Intl.NumberFormat('en-US').format(1234567.89);  // "1,234,567.89"
new Intl.NumberFormat('de-DE').format(1234567.89);  // "1.234.567,89"
new Intl.NumberFormat('ar-SA').format(1234567.89);  // "١٬٢٣٤٬٥٦٧٫٨٩"

// Currency
new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(19.99);
// "$19.99"
```

### RTL — Right-to-Left Layouts

Arabic, Hebrew, Persian, Urdu — these languages read right to left. Your layout needs to flip.

```css
/* In your CSS, DON'T hardcode left/right */
/* ❌ Bad */
.text { padding-left: 10px; }

/* ✅ Good — use logical properties */
.text { padding-inline-start: 10px; }      /* left in LTR, right in RTL */
.sidebar { margin-inline-end: 16px; }       /* right in LTR, left in RTL */
```

```html
<!-- Set the dir attribute on the html element -->
<html dir="rtl" lang="ar">
```

**In React with next-i18next or react-i18next:**
```javascriptx
// Automatically set dir on <html>
useEffect(() => {
  document.documentElement.dir = i18n.dir();  // 'ltr' or 'rtl'
  document.documentElement.lang = i18n.language;
}, [i18n.language]);
```

### Translation Management — Don't Do It Manually

For small projects, editing JSON files by hand is fine. For production apps, use a translation management system:

- **Locize** — Made by the i18next team, has OTA (over-the-air) updates
- **Crowdin** — Good for community translations
- **POEditor** — Simple, affordable
- **Transifex** — Enterprise

**Workflow:**
1. Developers add keys to the codebase
2. Push to translation service via API
3. Translators work in the web interface
4. Pull translations back → deploy

### Pseudolocalization — Test Without Translating

Before you have real translations, test that your UI handles text expansion (German words are 30% longer than English):

```
[!!Ţȟîš îš ȟöŵ ŷöûŕ ȃƥƥ ŵîļļ ŀööķ îñ Ģȇŕɱȃñ!!]
```

Some i18n tools can generate this automatically. It exposes layout bugs before translators start working.

### Common Mistakes

| Mistake | Fix |
|---|---|
| Concatenating strings (`"Hello " + name`) | Use interpolation: `t('greeting', { name })` |
| Hardcoding plurals (`count + " items"`) | Use i18next plural syntax |
| Translating in CSS (`content: "Loading"`) | CSS can't be translated — use HTML |
| Ignoring text length (German is 30% longer) | Test with pseudolocalization |
| Forgetting RTL | Set `dir` and use logical CSS properties |
| Translating images with text (screenshots) | Use separate images per language or overlay text |

### Your Turn

1. Install i18next and add English + one other language to your app
2. Translate 5 UI strings — welcome, buttons, error messages
3. Handle plurals correctly for "X items in cart"
4. Add a language switcher button
5. (Bonus) Add RTL support and test with Arabic

---

## 25. Background Jobs & Message Queues — Don't Make Users Wait

Your server receives a request. It needs to:
1. Process a credit card payment
2. Send a confirmation email
3. Generate a PDF invoice
4. Update analytics
5. Notify the warehouse

If your user waits for ALL of this to finish before seeing "Payment successful," they'll wait 5+ seconds and assume your app is broken.

**The fix: do the important thing NOW, do the rest LATER.**

```javascript
// ❌ User waits for everything
app.post('/checkout', async (req, res) => {
  await processPayment(req.body);       // 2 seconds
  await sendEmail(req.body.email);      // 1 second
  await generateInvoice(req.body);      // 1.5 seconds
  await updateAnalytics(req.body);      // 0.5 seconds
  res.send('Done');                     // Total: 5 seconds = bad UX
});

// ✅ User sees result instantly, background does the rest
app.post('/checkout', async (req, res) => {
  await processPayment(req.body);       // 2 seconds - user waits
  queue.add('sendEmail', req.body);     // Instant
  queue.add('generateInvoice', req.body); // Instant
  queue.add('updateAnalytics', req.body); // Instant
  res.send('Done');                     // Total: 2 seconds = happy user
});
```

### What Is a Background Job?

A background job is a task that runs outside the main request-response cycle. It's handled by a **worker process** that picks up tasks from a **queue** and processes them one at a time (or many at once).

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Your App   │────>│   Queue      │────>│   Worker    │
│  (Express)  │     │  (Redis)     │     │  (Node.js)  │
└─────────────┘     └──────────────┘     └─────────────┘
       │                   │                    │
   Adds jobs              Stores              Processes
   to queue             pending jobs           each job
```

### Bull — Redis-Based Queue for Node.js

Bull is the most popular job queue for Node.js. It uses Redis as its storage backend.

```bash
npm install bull
# You also need Redis running:
#   Windows: Install WSL and `sudo apt install redis-server`
#   Mac: `brew install redis`
#   Docker: `docker run -p 6379:6379 redis`
```

```javascript
const Queue = require('bull');

// Create a queue
const emailQueue = new Queue('email', {
  redis: { host: 'localhost', port: 6379 },
});

// Add a job
app.post('/signup', async (req, res) => {
  const user = await createUser(req.body);

  // Add job to queue — returns immediately
  await emailQueue.add({
    to: user.email,
    subject: 'Welcome!',
    template: 'welcome-email',
    userId: user.id,
  }, {
    attempts: 3,           // Retry 3 times if it fails
    backoff: 5000,         // Wait 5 seconds between retries
    removeOnComplete: true // Auto-cleanup
  });

  res.status(201).json({ user });
});

// Worker process (separate file, separate process)
// worker.js
emailQueue.process(async (job) => {
  const { to, subject, template, userId } = job.data;
  console.log(`Sending email to ${to} (attempt ${job.attemptsMade + 1})`);

  await sendEmail(to, subject, template);
  console.log(`Email sent to ${to}`);
});
```

Run the worker separately:
```bash
node worker.js   # In a separate terminal or as a background process
```

### Job Lifecycle

```
Added → Waiting → Active → Completed
                      ↓
                   Failed → Retry (if attempts remain) → Active
                      ↓
              Failed (no retries left)
```

Bull gives you dashboard endpoints to monitor everything:

```javascript
// See queue status
app.get('/admin/queues', async (req, res) => {
  const [waiting, active, completed, failed] = await Promise.all([
    emailQueue.getWaitingCount(),
    emailQueue.getActiveCount(),
    emailQueue.getCompletedCount(),
    emailQueue.getFailedCount(),
  ]);
  res.json({ waiting, active, completed, failed });
});
```

### Delayed Jobs — Schedule for Later

```javascript
// Send a reminder email 24 hours after signup
await emailQueue.add(
  { to: user.email, type: 'reminder' },
  { delay: 24 * 60 * 60 * 1000 }  // 24 hours in ms
);

// Reset at midnight
const now = new Date();
const midnight = new Date(now.getFullYear(), now.getMonth(), now.getDate() + 1);
await analyticsQueue.add(
  { type: 'daily-report' },
  { delay: midnight - now }
);
```

### Recurring Jobs — Cron Without Cron

```javascript
const Queue = require('bull');
const queue = new Queue('reports');

// Every day at 2 AM
queue.add({ type: 'daily-report' }, { repeat: { cron: '0 2 * * *' } });

// Every hour
queue.add({ type: 'hourly-cleanup' }, { repeat: { cron: '0 * * * *' } });

// Every Monday at 9 AM
queue.add({ type: 'weekly-summary' }, { repeat: { cron: '0 9 * * 1' } });
```

### Concurrency — Process Many Jobs at Once

```javascript
// Process 5 emails simultaneously
emailQueue.process(5, async (job) => {
  await sendEmail(job.data);
});

// Process invoices one at a time (order matters)
invoiceQueue.process(1, async (job) => {
  await generateInvoice(job.data);
});
```

### Error Handling & Retries

Things fail. Services go down. Networks hiccup. Bull handles retries gracefully:

```javascript
emailQueue.add(jobData, {
  attempts: 5,                    // Try 5 times
  backoff: {
    type: 'exponential',          // Wait: 1s, 2s, 4s, 8s, 16s
    delay: 1000,
  },
});

// Listen for failures to alert yourself
emailQueue.on('failed', (job, err) => {
  console.error(`Job ${job.id} failed after ${job.attemptsMade} attempts:`, err);
  Sentry.captureException(err);
});
```

### Bull Board — Visual Dashboard

Bull Board gives you a web UI to see queues, retry jobs, and inspect failures:

```bash
npm install bull-board
```

```javascript
const { BullBoard } = require('bull-board');
const { QueueAdapter } = require('bull-board/bull');

BullBoard.setQueues([
  new QueueAdapter(emailQueue),
  new QueueAdapter(invoiceQueue),
]);

app.use('/admin/queues', BullBoard.UI);
```

Visit `/admin/queues` — you'll see a beautiful dashboard with job counts, retry buttons, and failure details.

### Real-World Patterns

**1. Welcome email sequence:**
```
Signup → Job 1: Send welcome email (immediate)
       → Job 2: Send tips email (24h later)
       → Job 3: Ask for review (72h later)
```

**2. Image processing:**
```
Upload → Resize to 3 sizes (thumb, medium, large)
       → Generate WebP version
       → Store metadata in database
       → Invalidate CDN cache
```

**3. Batch operations:**
```
Export 10,000 users to CSV
  → One job creates the task
  → Workers process users in batches of 100
  → Final job assembles and emails the file
```

### When NOT to Use Background Jobs

- **Real-time responses the user waits for** — use synchronous code or WebSockets
- **Simple tasks** — sending one email isn't worth the complexity of a queue
- **You have < 100 users** — just do it synchronously until you need to scale
- **Tasks that must be atomic** — can't retry a payment twice

### Alternatives to Bull

| Option | Storage | Best For |
|---|---|---|
| **Bull** | Redis | Node.js apps, fast, feature-rich |
| **Bee Queue** | Redis | Lighter than Bull, same concepts |
| **Agenda** | MongoDB | Mongo users, nice job scheduling API |
| **PG Boss** | PostgreSQL | Postgres users, minimal dependencies |
| **Zeplo** | Cloud | Serverless, no Redis needed |
| **Trigger.dev** | Cloud | Open source, web UI, built-in retries |

### Your Turn

1. Install Redis (via Docker: `docker run -p 6379:6379 redis`)
2. Create an email queue with Bull
3. Add a job when a user signs up
4. Create a worker that "sends" the email (just logs it)
5. Add a retry with exponential backoff
6. Install Bull Board and inspect your queues

---

## 26. Feature Flags — Ship Code Without Fear

You've just built a big new feature — a redesigned checkout flow. It's been in development for 3 weeks. It touches 12 files. You're terrified to deploy it.

**The old way:** Create a feature branch, work on it for weeks, merge it, deploy, HOLD YOUR BREATH, pray nothing breaks.

**The better way:** Deploy the new code immediately but HIDE it behind a feature flag. Turn it on for 10% of users. Monitor. Fix. Turn on for everyone.

Feature flags let you control exactly who sees what, when — without redeploying.

### The Simplest Feature Flag — An If Statement

```javascript
// flagCheckoutRedesign.js
const FEATURES = {
  newCheckout: process.env.NEW_CHECKOUT === 'true',  // Simple toggle
};

// In your code:
if (FEATURES.newCheckout) {
  res.render('checkout-v2');
} else {
  res.render('checkout-v1');
}
```

**This is already better than not having flags.** You can turn the feature on/off with an env var — no code change, no redeploy.

### Why Feature Flags Beat Branches

| Situation | Feature Branch | Feature Flag |
|---|---|---|
| Code is half-finished | Can't merge without breaking | Merge any time, flag hides it |
| Found a bug in production | Revert the whole deploy | Turn off ONE flag |
| Need to A/B test | Impossible | 50% of users see B |
| Merge conflicts | Every long-lived branch has them | Small, frequent merges |
| QA wants to test in production | Can't hide from users | Enable for specific users |

### LaunchDarkly — The Industry Standard

LaunchDarkly is a full-featured feature flag platform. Free for small teams.

```bash
npm install launchdarkly-node-server-sdk
```

```javascript
const LaunchDarkly = require('launchdarkly-node-server-sdk');

const client = LaunchDarkly.init(process.env.LD_SDK_KEY);

app.get('/checkout', async (req, res) => {
  const user = { key: req.userId, email: req.userEmail };

  // Ask LaunchDarkly: should this user see the new checkout?
  const showNewCheckout = await client.variation('new-checkout', user, false);

  if (showNewCheckout) {
    res.render('checkout-v2');
  } else {
    res.render('checkout-v1');
  }
});
```

**The LaunchDarkly dashboard lets you:**
- Toggle any feature instantly (no deploy)
- Target specific users (by email, geography, plan type)
- Roll out to 10%, then 50%, then 100%
- Set automatic kill switches (if error rate > 5%, turn off)
- Add user targeting rules

### A Simple Self-Hosted Alternative

LaunchDarkly is great but has a cost. For small projects, build your own:

```javascript
// features.json — config file
{
  "new-checkout": {
    "enabled": true,
    "percentage": 50,
    "users": ["user123", "user456"],
    "rules": {
      "beta-testers": true,
      "premium-users": true
    }
  },
  "dark-mode": {
    "enabled": false,
    "percentage": 0
  }
}
```

```javascript
const features = require('./features.json');

function isEnabled(flagName, user) {
  const flag = features[flagName];
  if (!flag) return false;
  if (!flag.enabled) return false;

  // Check specific users
  if (flag.users?.includes(user.id)) return true;

  // Check percentage
  if (flag.percentage) {
    // Deterministic: same user always gets the same result
    const hash = hashCode(user.id + flagName) % 100;
    if (hash < flag.percentage) return true;
  }

  // Check rules
  if (flag.rules?.['beta-testers'] && user.isBetaTester) return true;
  if (flag.rules?.['premium-users'] && user.plan === 'premium') return true;

  return false;
}
```

### Kill Switch — Your Emergency Brake

The most important feature flag is the **kill switch**. If a new feature is causing errors, kill it instantly:

```javascript
// A single flag that controls CANARY DEPLOYMENTS
const canaryEnabled = await client.variation('canary-deploy', user, false);

// If something goes wrong, flip this flag OFF
// All users instantly fall back to old code
```

### A/B Testing — Feature Flags as Science Experiments

Feature flags let you run controlled experiments:

```javascript
// User sees one of two button colors
const buttonColor = await client.variation('signup-button-color', user, 'blue');

if (buttonColor === 'green') {
  showGreenButton();  // Test group
} else {
  showBlueButton();  // Control group
}

// Track conversion rate for each group
analytics.track('signup_attempt', {
  variant: buttonColor,
  userId: user.id,
});
```

**Statistical significance — wait until you have enough data:**
- At least 1,000 users per variant
- Run for at least 7 days (weekday vs weekend patterns matter)
- Use a calculator: https://www.evanmiller.org/ab-testing/sample-size.html

### Flag Pollution — Too Many Flags

```
// ❌ After 2 years of feature flags
if (flag1 && (flag2 || !flag3) && flag4 && user.plan === 'premium') {
  // Nobody knows what this does anymore
}
```

**Cleanup discipline:**
1. When a feature is fully rolled out, REMOVE the flag
2. Delete the old code path too (not just the flag check)
3. Keep a CHANGELOG of removed flags
4. Review unused flags monthly

### Types of Feature Flags

| Type | Lifespan | Example |
|---|---|---|
| **Release flag** | Days to weeks | Toggle between old and new UI |
| **Experiment flag** | Weeks to months | A/B test a button color |
| **Permission flag** | Permanent | "Premium users can access this" |
| **Ops flag** | Hours to days | Kill switch for a slow database query |
| **Kill switch** | Permanent | Emergency off for any new feature |

### Your Turn

1. Create a simple feature flag system using a JSON config file
2. Add a flag for "dark mode" — turn it on for 20% of users
3. Implement a kill switch that turns off the new checkout if errors spike
4. Deploy code that's hidden behind a flag, then enable it without redeploying
5. (Bonus) Set up LaunchDarkly free tier and integrate it

---

## 27. Mobile Strategies — Beyond the Browser

Your web app works great on desktop. But 60%+ of web traffic is mobile. If your app feels like a shrunken desktop site, users will bounce in seconds.

**You have 4 options for going mobile:**
1. Responsive web app (PWA) — low effort, good reach
2. React Native — share code, native feel
3. Flutter — beautiful UI, single codebase
4. Native (Swift/Kotlin) — maximum performance, double the work

There's no single "best" choice. Each has trade-offs. Let's be honest about them.

### Option 1: PWA (Progressive Web App) — Your Best First Move

A PWA is a website that behaves like a native app. It can be installed, works offline, and can send push notifications.

**What makes a PWA:**
- HTTPS (security requirement)
- Manifest (install prompt, splash screen, home screen icon)
- Service worker (offline support, caching)
- Responsive (works on any screen)

```json
// manifest.json
{
  "name": "My App",
  "short_name": "App",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#3b82f6",
  "icons": [
    { "src": "/icon-192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icon-512.png", "sizes": "512x512", "type": "image/png" }
  ]
}
```

```javascript
// sw.js — Service Worker (cache-first strategy)
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then((cached) => cached || fetch(event.request))
      .catch(() => cached)  // Offline? Show cached version
  );
});
```

**PWA Pros:**
- One codebase for everything
- No app store approval (instant updates)
- 100% of your existing skills transfer
- Users can install with one tap (no app store)
- Works offline
- Push notifications

**PWA Cons:**
- No access to native APIs (Bluetooth, NFC, file system)
- Can't run in the background (no music player while locked)
- iOS support is weaker than Android (Safari limitations)
- Harder to monetize (no in-app purchases through App Store)
- Feels slightly less "native" (but getting better)

**When to choose PWA:**
- Content apps (news, blogs, recipes)
- E-commerce (mobile shopping)
- Dashboards and admin panels
- You're a solo developer or tiny team
- You want to ship fast

### Option 2: React Native — JavaScript Meets Native

React Native lets you write mobile apps using React components that compile to native iOS and Android views.

```javascriptx
import { View, Text, StyleSheet, Button } from 'react-native';

export default function HomeScreen() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Hello from React Native!</Text>
      <Button title="Press me" onPress={() => alert('Pressed!')} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', alignItems: 'center' },
  title: { fontSize: 24, fontWeight: 'bold' },
});
```

**React Native Pros:**
- Share code between iOS and Android (~95% code reuse)
- If you know React, you know 80% of React Native
- Huge ecosystem (Expo, React Navigation, many libraries)
- Hot reload (changes appear instantly)
- Access to native APIs via modules
- Better performance than PWA

**React Native Cons:**
- Not quite native performance (complex animations can stutter)
- Debugging is harder than web (no browser DevTools)
- Some platforms need native code (Bluetooth, ARKit)
- Bundle size is large (30-50MB for a simple app)
- Third-party library compatibility can break with updates

**The Expo advantage:**
```bash
npm create expo-app my-app --template
cd my-app
npm start               # Scan QR code with Expo Go app
```

Expo handles all the native build tooling for you. No Xcode or Android Studio needed for development. Your phone scans a QR code and runs the app instantly.

```bash
# Build for production
eas build --platform ios
eas build --platform android
```

**When to choose React Native:**
- You already know React
- Need a real native app with app store distribution
- Need access to native features (camera, GPS, push notifications)
- You have a team but not enough for two native teams

### Option 3: Flutter — Google's Wild Card

Flutter uses Dart (not JavaScript) and renders its own UI using Skia (a graphics engine). It doesn't use native components — it paints everything itself.

```dart
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Hello from Flutter!', style: TextStyle(fontSize: 24)),
            ElevatedButton(
              onPressed: () => print('Pressed!'),
              child: Text('Press me'),
            ),
          ],
        ),
      ),
    );
  }
}
```

**Flutter Pros:**
- Pixel-perfect UI on both platforms (same rendering engine)
- Excellent performance (60fps guaranteed)
- Hot reload (faster than React Native)
- Great documentation and widget library
- Web and desktop support (same codebase for everything)
- Dart is a nice language (TypeScript-like)

**Flutter Cons:**
- Have to learn Dart (yet another language)
- No shared code with web (different UI paradigm)
- Large app size (~15MB for hello world)
- Less mature ecosystem than React Native
- Custom UI doesn't feel native on either platform (it feels like Flutter)
- Harder to integrate with native SDKs

**When to choose Flutter:**
- You want beautiful, custom UI (animations, transitions)
- Performance is critical
- You're building for mobile + desktop + web
- You're willing to learn Dart
- You're starting from scratch (no existing web codebase)

### Option 4: Native (Swift/Kotlin) — The Full Monty

Writing native apps means using Swift for iOS and Kotlin for Android. Two separate codebases, two separate teams.

```swift
// Swift — iOS
import SwiftUI

struct ContentView: View {
    @State private var count = 0
    
    var body: some View {
        VStack {
            Text("Count: \(count)")
                .font(.title)
            Button("Increment") { count += 1 }
        }
    }
}
```

```kotlin
// Kotlin — Android
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            var count by remember { mutableStateOf(0) }
            Column(horizontalAlignment = Alignment.CenterHorizontally) {
                Text("Count: $count", fontSize = 24.sp)
                Button(onClick = { count++ }) { Text("Increment") }
            }
        }
    }
}
```

**Native Pros:**
- Best performance (direct access to GPU, sensors, everything)
- Best user experience (following platform conventions)
- Access to every API on day one (no waiting for third-party libraries)
- Smallest app size
- Best tooling (Xcode, Android Studio)

**Native Cons:**
- Two codebases (2x development, 2x maintenance, 2x bugs)
- Different languages, different patterns
- Harder to find developers who know both
- Slower to ship features
- More expensive

**When to choose Native:**
- Performance-critical apps (games, AR/VR)
- Apps that need deep OS integration (health sensors, Bluetooth LE)
- You have separate iOS and Android teams
- The app is simple enough that two codebases aren't a burden

### The Honest Comparison

| Factor | PWA | React Native | Flutter | Native |
|---|---|---|---|---|
| **Dev speed** | Fastest | Fast | Fast | Slowest |
| **Code sharing** | 100% (web only) | 95% (iOS + Android) | 100% (all platforms) | 0% (separate codebases) |
| **Performance** | Good | Very good | Excellent | Best |
| **App feel** | Web-ish | Close to native | Flutter-ish | Native |
| **Offline** | Yes (limited) | Yes | Yes | Yes |
| **Push notifications** | Android yes, iOS limited | Yes | Yes | Yes |
| **App store** | No (installed from web) | Yes | Yes | Yes |
| **App size** | KBs | 30-50MB | 15-30MB | 5-15MB |
| **Learn once** | Web dev skills | React skills | Dart skills | Swift + Kotlin |
| **Best for** | Content apps, e-commerce, dashboards | Social, productivity, most apps | Beautiful UI, cross-platform | Games, performance-critical |

### The Practical Decision Tree

```
Is performance critical (60fps+ animations)?
  YES → Is it a game or AR?
           YES → Native
           NO  → Flutter
  NO  → Do you already have a web app?
           YES → Is the mobile experience simple (content, forms, lists)?
                    YES → PWA (start here, upgrade later)
                    NO  → React Native
           NO  → Will you ever need a web app too?
                    YES → React Native (share with web via React)
                    NO  → Flutter or Native (your call)
```

### Real Talk — The Trough of Disappointment

Every mobile development journey looks like this:

```
Week 1: 🎉 This is amazing! Building apps is so fast!
Week 2: 🤔 Why won't this animation work on Android?
Week 3: 😡 The keyboard is covering my input fields!
Week 4: 🥲 My app works but feels... wrong. Why?
Week 5: 😤 Platform conventions are different! My iOS app looks like Android!
Week 6: 😎 I understand now. It's not "write once, run anywhere." It's "write once, debug everywhere."
Week 7-12: 💪 Actually building real features. Getting good at this.
```

**This is normal.** Every mobile developer goes through this. The difference between those who succeed and those who quit is: the successful ones knew the pain was coming and pushed through it.

### Hyprid: PWA + React Native — The Best of Both Worlds

Many successful apps use a hybrid approach:
- **Content/landing pages** → PWA (shareable links, instant loading)
- **Core experience** → React Native (native performance, app store)
- **Admin panel** → Web (desktop-focused)

### Your Turn

1. Convert a page of your web app into a React Native screen (use Expo for easy setup)
2. Add a service worker to your existing web app (make it a PWA)
3. Test your PWA on a real phone (must be HTTPS)
4. Run Lighthouse PWA audit on your site
5. Research: what would it take to ship your app on the App Store?

---

## Final Words

You've covered an enormous amount of ground. Here's what you now know:

- **TypeScript** — types, interfaces, generics
- **Next.js** — SSR, SSG, App Router, Server Components
- **Tailwind CSS** — utility-first styling
- **Authentication** — JWT, sessions, OAuth, bcrypt
- **Testing** — unit, integration, E2E with Vitest, Supertest, Playwright
- **Security** — XSS, CSRF, SQL injection, CSP, helmet
- **Performance** — code splitting, caching, CDN, Lighthouse
- **CI/CD** — GitHub Actions, automated deploy
- **Docker** — containers, Docker Compose
- **WebSockets** — real-time with Socket.IO
- **State Management** — Context, Zustand, Redux
- **GraphQL** — Apollo Server + Client
- **Database Hosting** — Supabase, Neon, MongoDB
- **Linux** — SSH, commands, processes, systemd
- **Responsive Design** — container queries, clamp(), modern CSS
- **Accessibility** — ARIA, semantic HTML, keyboard nav
- **SEO** — meta tags, sitemaps, semantic HTML
- **Package Managers** — npm, Yarn, pnpm
- **Monorepos** — workspaces, Turborepo
- **Microservices** — splitting apps, inter-service communication
- **Serverless** — Vercel Functions, Edge Functions, Lambda
- **Web Components** — custom elements, Shadow DOM
- **Error Tracking** — Sentry, logs, health endpoints, alerting
- **Internationalization** — i18next, plurals, RTL, date/number formatting
- **Background Jobs** — Bull, Redis queues, retries, cron scheduling
- **Feature Flags** — LaunchDarkly, canary releases, A/B testing
- **Mobile Strategies** — PWA, React Native, Flutter, Native — and when to choose each

That's more than most developers with 5 years of experience know. Seriously.

**The difference between knowing and being:**
- Learning these concepts makes you knowledgeable
- **Building with them** makes you a senior developer

Pick one topic. Build something with it. Break it. Fix it. Move to the next.

You started as a beginner who didn't know what HTML was. You're now an advanced developer with a toolkit that spans frontend, backend, mobile, DevOps, testing, security, and architecture.

**That's not just learning. That's transformation.**

Welcome to advanced territory. You belong here.
