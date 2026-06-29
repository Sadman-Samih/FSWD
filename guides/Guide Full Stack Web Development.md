# Full Stack Web Development — The Complete Beginner's Guide

## A Friendly, No-Nonsense Journey from Zero to Building Real Apps

> **"The best time to start was yesterday. The second best time is right now."**
>
> This guide is written for **you** — someone who's heard about "coding" or "web development" and wants to actually *do* it. No gatekeeping. No assumed knowledge. Just clear explanations, real analogies, and a path forward.

---

## How to Use This Guide

- **If you're brand new:** Read chapters 1–4 in order. Do every exercise.
- **If you know some HTML/CSS:** Jump to chapter 5 (JavaScript).
- **If you're comfortable with frontend:** Start at chapter 7 (Backend).

Each chapter ends with a **Your Turn** section — actually do these. Coding is a skill, not a spectator sport.

---

## Table of Contents

1. [[#1. So You Want to Build Websites?|So You Want to Build Websites?]]
2. [[#2. How the Web Actually Works|How the Web Actually Works]]
3. [[#3. Setting Up Your Tools|Setting Up Your Tools]]
4. [[#4. HTML — The Language Your Browser Speaks|HTML — The Language Your Browser Speaks]]
5. [[#5. CSS — Making Things Look Good|CSS — Making Things Look Good]]
6. [[#6. JavaScript — Bringing Your Site to Life|JavaScript — Bringing Your Site to Life]]
7. [[#7. The Backend — What Happens Behind the Scenes|The Backend — What Happens Behind the Scenes]]
8. [[#8. Databases — Remembering Things|Databases — Remembering Things]]
9. [[#9. Building Your First Full Stack App|Building Your First Full Stack App]]
10. [[#10. APIs — How Frontend and Backend Talk|APIs — How Frontend and Backend Talk]]
11. [[#11. Deploying — Showing Your Work to the World|Deploying — Showing Your Work to the World]]
12. [[#12. Git & GitHub — Time Travel for Your Code|Git & GitHub — Time Travel for Your Code]]
13. [[#13. Your Learning Roadmap|Your Learning Roadmap]]
14. [[#14. Intro to React|Intro to React]]
15. [[#15. The Complete Reference|The Complete Reference]]
16. [[#16. Troubleshooting — When Things Break|Troubleshooting — When Things Break]]
17. [[#17. Glossary|Glossary]]
18. [[#18. Practice Projects|Practice Projects]]
    - [[#Project 1: Personal Portfolio Site|Project 1: Personal Portfolio Site]]
    - [[#Project 2: Calculator|Project 2: Calculator]]
    - [[#Project 3: Weather App|Project 3: Weather App]]
    - [[#Project 4: Blog with Comments|Project 4: Blog with Comments]]
    - [[#Project 5: URL Shortener|Project 5: URL Shortener]]
19. [[#19. Desktop Apps with Electron — Take Your Web Skills Beyond the Browser|Desktop Apps with Electron]]

---

## 1. So You Want to Build Websites?

### The Myth

You might think you need to be a math genius. Or that you need a computer science degree. Or that all programmers look like they're in a Hollywood movie typing green text on a black screen.

**None of that is true.**

### The Reality

Web development is **building things**. Think of it like cooking:

- **HTML** is your grocery list (ingredients)
- **CSS** is how you plate the food (presentation)
- **JavaScript** is the recipe steps (process)
- **Backend** is the kitchen staff and pantry (behind the scenes)

You don't need to be a master chef to make a good meal. You just need to learn a few recipes and practice.

### What "Full Stack" Actually Means

Imagine you're building a house:

- **Frontend** = the rooms, windows, paint, furniture (what people see)
- **Backend** = the foundation, plumbing, electrical, roof (what makes it work)
- **Full Stack** = you know enough to build the whole house yourself

```
╔══════════════════════════════════════════════════════════╗
║                     YOUR WEBSITE                        ║
║                                                         ║
║  ┌──────────────────────────────────────────────────┐   ║
║  │             FRONTEND (What users see)             │   ║
║  │  ┌──────────┐  ┌──────────┐  ┌────────────────┐  │   ║
║  │  │   HTML   │  │   CSS    │  │  JavaScript    │  │   ║
║  │  │ Structure│  │  Style   │  │ Interactivity  │  │   ║
║  │  └──────────┘  └──────────┘  └────────────────┘  │   ║
║  └──────────────────────────────────────────────────┘   ║
║                         │                                ║
║                         ▼                                ║
║  ┌──────────────────────────────────────────────────┐   ║
║  │           BACKEND (Behind the scenes)             │   ║
║  │  ┌────────────────┐  ┌────────────────┐          │   ║
║  │  │    Server      │  │   Database     │          │   ║
║  │  │  (Node.js)     │  │     (SQL)      │          │   ║
║  │  └────────────────┘  └────────────────┘          │   ║
║  └──────────────────────────────────────────────────┘   ║
╚══════════════════════════════════════════════════════════╝
```
### What You'll Build By The End of This Guide

A **full notes app** where you can:
- Add a note (with title and content)
- See all your notes
- Edit a note
- Delete a note
- It works on your phone

And you'll understand **every single line of code** that makes it work.

---

## 2. How the Web Actually Works

### Your Browser's Secret Life

Every time you visit a website, your browser throws a party involving multiple computers around the world. Here's the guest list:

```
YOU ──> Your Browser (Chrome/Firefox/Safari/Edge)
         │
         │  "Hey, where's google.com?"
         ▼
       DNS Server (The Internet's Phone Book)
         │
         │  "It's at 142.250.80.46"
         ▼
       Google's Server
         │
         │  "Here's my homepage (HTML, CSS, JS)"
         ▼
       Your Browser renders the page
         │
         │  "Looking good!"
         ▼
       YOU see the Google homepage
```

**DNS (Domain Name System)** is the internet's phone book. Instead of remembering `142.250.80.46`, you remember `google.com`. DNS connects the two.

**Your Turn:** Type `142.250.80.46` into your browser's address bar. What happens? (It might redirect, but you'll land on Google!)

### The Client-Server Dance

This is the most important concept in web development:

```
CLIENT (Your browser)                  SERVER (A computer in a data center)
       │                                       │
       │  ─── GET /index.html ──────────────>  │
       │                                       │  "Let me find that file..."
       │  <─── [200 OK] HTML content ────────  │
       │                                       │
       │  ─── GET /style.css ───────────────>  │
       │  <─── [200 OK] CSS content ────────   │
       │                                       │
       │  ─── GET /app.js ─────────────────>   │
       │  <─── [200 OK] JS content ────────    │
```

**The Client** (your browser) **requests** things. **The Server** (another computer) **responds** with things.

That's it. That's the entire web in one paragraph.

### HTTP Status Codes — The Server's Mood Ring

When a server responds, it includes a status code. Think of them like:

| Code | Meaning | Emoji |
|---|---|---|
| `200` | OK — everything's fine | ✅ |
| `201` | Created — new thing was made | 🆕 |
| `301` | Moved — this page lives somewhere else now | 🔀 |
| `400` | Bad Request — you messed up | ❌ |
| `401` | Unauthorized — who are you? | 🔒 |
| `403` | Forbidden — you're not allowed | 🚫 |
| `404` | Not Found — this doesn't exist | 🤷 |
| `500` | Server Error — something broke on the server | 💥 |

**Pro tip:** When something breaks, check the status code first. It tells you where the problem is.

### URLs — Breaking Them Down

```
https://www.example.com:443/blog/article?page=2#comments
│      │       │          │   │             │       │
│      │       │          │   │             │       └── Fragment (scroll to comments)
│      │       │          │   │             └── Query string (extra data)
│      │       │          │   └── Path (which page)
│      │       │          └── Port (443 = HTTPS default)
│      │       └── Domain name
│      └── Subdomain
└── Protocol (HTTP or HTTPS)
```

**Your Turn:** Pick any URL from your browser's address bar and label each part.

---

## 3. Setting Up Your Tools

You need four things to start building websites. Let's install them.

### 3.1 VS Code — Where You'll Write Code

VS Code is like Microsoft Word, but for code. It's free, powerful, and everyone uses it.

1. Go to [https://code.visualstudio.com](https://code.visualstudio.com)
2. Click the big blue **Download** button
3. Install it (next, next, finish — default settings are fine)

**Your Turn:** Open VS Code. Press `Ctrl+N` (new file). Type something. Save it as `hello.txt`. Congrats — you just used a code editor!

### 3.2 Live Server — See Changes Instantly

Without Live Server, you'd have to refresh your browser every time you save a file. With it, your page automatically reloads. Magic.

1. In VS Code, click the **Extensions** icon (looks like four blocks on the left sidebar)
2. Search for "Live Server"
3. Click **Install** (by Ritwick Dey)

**Your Turn:** Create a file called `index.html`, type `Hello World`, then right-click the file and choose "Open with Live Server". A browser will open showing your file. Change the text in VS Code, save — the browser updates instantly.

### 3.3 Node.js — JavaScript on Your Computer

JavaScript was originally only for browsers. Node.js lets it run anywhere — including on servers.

1. Go to [https://nodejs.org](https://nodejs.org)
2. Download the **LTS** version (Long Term Support — it's the stable one)
3. Install it (next, next, finish)

**Verify it worked:**

Open a terminal in VS Code (`Ctrl+` ` — backtick key, or Terminal → New Terminal):

```bash
node --version
npm --version
```

If you see numbers like `v20.x.x` and `10.x.x`, you're good. If you get an error, restart VS Code and try again.

### 3.4 Git — Your Code's Time Machine

Git saves snapshots of your code so you can go back in time if something breaks.

1. Go to [https://git-scm.com](https://git-scm.com)
2. Download and install (default settings)

**Verify:**

```bash
git --version
```

### 3.5 Terminal Basics — Talking to Your Computer Like a Hacker

The terminal is a text-based way to control your computer. It looks like a hacker movie screen, but it's just a conversation — you type a command, the computer does it, and maybe says something back.

**Think of it like talking to a dog that only understands very specific words.** You have to say "Sit" not "hey buddy could you maybe sit down please." Same deal: `cd projects` not "please navigate to the projects folder."

#### Your Starter Pack (The 5 You Already Need)

```bash
pwd           # Where am I? (Print Working Directory)
ls            # What's in this folder? (LiSt)
dir           # Same thing on Windows
cd foldername # Go INTO a folder (Change Directory)
cd ..         # Go UP one folder
mkdir blah    # Make a new folder (MaKe DIRectory)
code .        # Open VS Code in this folder
```

**Your Turn:** `mkdir playground` → `cd playground` → `code .`

#### PATH — The Computer's Phonebook

When you type `node --version`, your computer has to FIND the `node` program. It doesn't search everywhere — that'd take forever. It checks a list of folders called the **PATH**.

**Think of PATH like your phone's contact list.** When you say "call Mom," your phone looks up "Mom" in your contacts to find the number. When you type `node`, your computer looks it up in PATH to find the program.

```bash
# See what's in your PATH
echo $PATH        # Mac/Linux
echo $env:PATH    # Windows PowerShell
```

If you install something and the terminal says "command not found," it means the program's folder isn't in your PATH. The fix: either add it to PATH, or use the full path:

```bash
# Full path (ugly but always works)
C:\Users\You\AppData\Roaming\npm\node.exe

# Or just add the folder to PATH (one-time setup)
```

#### Command Flags — The "-" Things

Most commands accept **flags** (also called options) that modify how they work. Flags start with `-` (short) or `--` (long).

```bash
# Without flags
ls

# With flags — show hidden files, human-readable sizes
ls -la
ls --all --human-readable
```

**Flags are like pizza toppings.** `ls` is a plain cheese pizza. `ls -la` adds pepperoni and extra cheese.

| Flag Pattern | Example | What It Means |
|---|---|---|
| `-a` | `ls -a` | Short flag — show hidden files |
| `--all` | `ls --all` | Long flag — same thing, easier to remember |
| `-la` | `ls -la` | Combined: show details + hidden files |
| `--version` | `node --version` | Long flag — show version |

Most commands have a `--help` flag. It's the "I'm lost" button:

```bash
git --help          # Show all git commands
npm install --help  # Show all npm install options
code --help         # See what VS Code can do from terminal
```

#### The Pipe — Connecting Commands Like LEGOs

The pipe `|` takes the output of one command and feeds it into the next. It's like a garden hose connecting two things.

```bash
# List all files, then scroll through them one page at a time
ls -la | more

# Count how many files are in a folder
ls | find /c /v ""    # Windows
ls | wc -l            # Mac/Linux

# Find a specific process
ps | findstr node     # Windows: find node processes
ps aux | grep node    # Mac/Linux: same thing
```

**Real-world use:** "I want to find all my `.txt` files, sort them by size, and save the list to a file."

```bash
ls -la *.txt | sort > text-files.txt
```

The `>` sends output INTO a file instead of printing it. `>>` appends instead of overwriting.

#### Tab Completion — Your Secret Weapon

Hit **Tab** while typing a command or file path — the terminal auto-completes it.

```
cd proj[Tab] → cd projects/
node serv[Tab] → node server.js
npm inst[Tab] → npm install
```

**If you hit Tab and nothing happens**, there are multiple matches. Hit Tab twice to see them all.

#### npm Init, npx, and Running Scripts

You'll use these constantly:

```bash
# Create a new package.json (the recipe card for your project)
npm init -y          # Quick setup, accepts all defaults

# Run a package without installing it permanently
npx create-react-app my-app
npx live-server      # Like Live Server but from the terminal

# Run a script from package.json
npm start
npm run dev
npm test
```

**`npx` is a "try before you buy."** It downloads the package, runs it once, then deletes it. No clutter.

#### The -- Before Special Arguments

Some commands need `--` to separate options from arguments. It means "everything after this is not a flag":

```bash
# Without -- : npm thinks "test" is a flag
npm install -- --save-dev

# Git: "this branch name might look like a flag"
git checkout -- main
```

#### Keyboard Shortcuts Every Dev Uses

| Shortcut | What It Does |
|---|---|
| **Up/Down arrows** | Cycle through command history |
| **Ctrl + C** | KILL the current command (it's stuck? Ctrl+C) |
| **Ctrl + L** | Clear the screen (like a broom for your terminal) |
| **Ctrl + A** | Go to beginning of line |
| **Ctrl + E** | Go to end of line |
| **Ctrl + R** | Search command history (type part of a previous command) |
| **Tab** | Auto-complete |

#### Aliases — Shortcuts for Your Shortcuts

Typing `git checkout -b new-feature` gets old. Aliases let you create shortcuts:

```bash
# Create a permanent alias
alias gs="git status"           # Mac/Linux
Set-Alias gs git status         # Windows PowerShell

# Now just type:
gs    # Instead of: git status
```

#### Your Turn: Terminal Workout

Open your terminal and do this without looking up the answers:

1. Create a folder called `terminal-practice`
2. Go into it
3. Create a file: `echo "hello terminal" > hello.txt`
4. List files with details (flags)
5. Read the file: `cat hello.txt` or `type hello.txt`
6. Create another folder INSIDE `terminal-practice` called `sub-folder`
7. Copy hello.txt into sub-folder
8. Use Tab completion to navigate back up
9. Clear the screen
10. Delete everything: go up, then `rm -rf terminal-practice` (or `rmdir /s terminal-practice` on Windows)

If you can do all 10, you know enough terminal to survive. The rest you'll learn by doing — one Google search at a time.

---

## 4. HTML — The Language Your Browser Speaks

### What is HTML?

HTML stands for **HyperText Markup Language**. 

It's not a "programming language" — it doesn't have logic or calculations. It's a "markup language" — you use it to *describe* content.

Think of HTML like a restaurant menu:
- The dish names are headings (`<h1>`)
- The descriptions are paragraphs (`<p>`)
- The prices are... well, prices (also `<p>`)

**If HTML were a person:** It would be the architect who draws the blueprint. "Here's where the living room goes. Here's where the kitchen goes. Here's where the door is."

### Every HTML Page Has the Same Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My First Page</title>
</head>
<body>
  <!-- Everything the user sees goes here -->
</body>
</html>
```

Let's break this down:

| Part | What it does |
|---|---|
| `<!DOCTYPE html>` | Tells the browser: "Hey, this is HTML5!" |
| `<html>` | The root — everything lives inside this |
| `<head>` | Settings and metadata (not visible to users) |
| `<title>` | Text that shows in the browser tab |
| `<body>` | Everything that's visible on the page |

**Pro tip:** Memorize this structure. You'll type it hundreds of times. VS Code can generate it for you: in a new `.html` file, type `!` and press Enter.

### 4.1 HTML Elements

HTML uses **tags** — words surrounded by angle brackets:

```html
<tagname>Content goes here</tagname>
```

Most tags come in pairs:
- **Opening tag:** `<p>`
- **Closing tag:** `</p>` (notice the forward slash)

Some tags are self-closing (no content inside):
```html
<br>      <!-- Line break -->
<img>     <!-- Image -->
<input>   <!-- Input field -->
<hr>      <!-- Horizontal rule (a line) -->
```

### 4.2 Your First Real HTML Page

Let's build a profile page. Create `profile.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Profile</title>
</head>
<body>

  <h1>Hi, I'm Alex! 👋</h1>

  <p>I'm learning web development and I love building things that live on the internet.</p>

  <h2>Things I Enjoy</h2>
  <ul>
    <li>Coding (obviously)</li>
    <li>Coffee (also obviously)</li>
    <li>Hiking (nature is the original UI)</li>
  </ul>

  <h2>My Favorite Website</h2>
  <a href="https://google.com">Click here to visit Google</a>

  <h2>A Picture</h2>
  <img src="https://placekitten.com/400/300" alt="A cute kitten">

</body>
</html>
```

**Your Turn:** Create this page, open it with Live Server, and see your first real webpage. Then change something — new heading, new list item, whatever. Save and watch it update.

### 4.3 The Most Common HTML Tags (Cheat Sheet)

#### Text

```html
<h1>Biggest Heading</h1>
<h2>Section Heading</h2>
<h3>Sub-section</h3>
<h4>Smaller</h4>
<h5>Even Smaller</h5>
<h6>Tiny Heading</h6>

<p>Regular paragraph text goes here.</p>
<p>This is another paragraph. Notice the space between them.</p>

<strong>Bold text</strong>
<em>Italic text</em>
<br>   <!-- Line break (self-closing) -->
<hr>   <!-- Horizontal line (self-closing) -->
```

#### Links and Images

```html
<!-- Link to another page -->
<a href="https://example.com">Clickable text</a>

<!-- Link that opens in a new tab -->
<a href="https://example.com" target="_blank">Open in new tab</a>

<!-- Link to somewhere on the same page -->
<a href="#section-2">Jump to Section 2</a>

<!-- Image -->
<img src="photo.jpg" alt="Description of the photo">

<!-- Image that's also a link -->
<a href="https://example.com">
  <img src="photo.jpg" alt="Clickable photo">
</a>
```

**Always use `alt`** on images — it helps screen readers (accessibility) and shows when images don't load.

#### Lists

```html
<!-- Unordered list (bullet points) -->
<ul>
  <li>Apples</li>
  <li>Bananas</li>
  <li>Cherries</li>
</ul>

<!-- Ordered list (numbered) -->
<ol>
  <li>First step</li>
  <li>Second step</li>
  <li>Third step</li>
</ol>

<!-- Nested list -->
<ul>
  <li>Fruits
    <ul>
      <li>Apples</li>
      <li>Oranges</li>
    </ul>
  </li>
  <li>Vegetables
    <ul>
      <li>Carrots</li>
      <li>Broccoli</li>
    </ul>
  </li>
</ul>
```

#### Forms — How Users Send You Data

```html
<form action="/submit-form" method="POST">
  <label for="name">Your Name:</label>
  <input type="text" id="name" name="name" placeholder="Enter your name" required>

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" placeholder="you@example.com">

  <label for="message">Message:</label>
  <textarea id="message" name="message" rows="5"></textarea>

  <label for="country">Country:</label>
  <select id="country" name="country">
    <option value="">-- Select --</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
    <option value="jp">Japan</option>
  </select>

  <button type="submit">Send Message</button>
</form>
```

**Input types you'll use most:**

| Type | Looks like | Use for |
|---|---|---|
| `text` | Text field | Names, short text |
| `email` | Text field with @ validation | Email addresses |
| `password` | Dots instead of letters | Passwords |
| `number` | Numbers only, with up/down arrows | Quantities |
| `checkbox` | Checkbox | Yes/no options |
| `radio` | Radio button (circle) | Choosing one from many |
| `file` | File picker | Uploading files |
| `date` | Date picker | Dates |
| `color` | Color picker | Colors |
| `hidden` | Invisible | Data that users shouldn't see |

#### Container Tags (The Building Blocks)

```html
<div>     <!-- Generic block container (takes full width) -->
<span>    <!-- Generic inline container (stays in line) -->
<header>  <!-- Top of a page or section -->
<nav>     <!-- Navigation links -->
<main>    <!-- Main content area -->
<section> <!-- Thematic group of content -->
<article> <!-- Self-contained content (blog post, news) -->
<aside>   <!-- Sidebar, related content -->
<footer>  <!-- Bottom of a page or section -->
```

**Why use `<div>` vs `<section>`?** They look the same visually, but semantic tags (section, article, nav) tell browsers and screen readers what your content *means*.

### 4.4 HTML Attributes — Extra Settings

Tags can have attributes that give more information:

```html
<element attribute="value">Content</element>
```

| Attribute | Used on | Purpose |
|---|---|---|
| `id` | Any element | Unique identifier — one per page |
| `class` | Any element | Group identifier — many elements can share |
| `src` | `<img>`, `<script>` | File path |
| `href` | `<a>`, `<link>` | URL destination |
| `alt` | `<img>` | Image description |
| `style` | Any element | Inline CSS (avoid when possible) |
| `data-*` | Any element | Custom data storage for JavaScript |
| `disabled` | `<button>`, `<input>` | Makes it unclickable |
| `readonly` | `<input>` | Can see but can't edit |

### 4.5 IDs vs Classes — The Great Distinction

```html
<!-- ID: unique, like a passport number -->
<div id="main-header">...</div>
<div id="main-header">...</div>  <!-- ❌ ERROR! IDs must be unique -->

<!-- Class: can be reused, like a team jersey -->
<div class="card">...</div>
<div class="card">...</div>     <!-- ✅ Multiple elements can share a class -->
<div class="card featured">...</div>  <!-- ✅ Can have multiple classes -->
```

**Pro tip:** Use IDs for JavaScript hooks (`document.getElementById`). Use classes for CSS styling.

### Your Turn — Mini Project: Build a Recipe Page

Create a new file called `recipe.html`. It should have:
1. A title (the recipe name)
2. An image of the dish (use `placekitten.com` or `picsum.photos`)
3. A list of ingredients (unordered)
4. A list of steps (ordered)
5. A link to a similar recipe on another site
6. A footer with your name

Try to write it without looking at the cheat sheet above. Use Google if you forget a tag. This is how real developers work!

---

## 5. CSS — Making Things Look Good

### What is CSS?

CSS = **Cascading Style Sheets**. It's the makeup department for your HTML.

**If HTML is the skeleton, CSS is the clothes, makeup, lighting, and photo filter.**

### The CSS Syntax

```css
selector {
  property: value;
  property: value;
}
```

Example:
```css
p {
  color: blue;
  font-size: 18px;
}
```

This says: "Every paragraph on my page should have blue text at 18 pixels tall."

### Three Ways to Add CSS

**Bad way** (inline — on the element itself):
```html
<p style="color: red; font-size: 20px;">Hello</p>
```

**Okay way** (in the `<head>`):
```html
<head>
  <style>
    p { color: blue; }
  </style>
</head>
```

**Good way** (external file — separate your concerns):
```html
<!-- index.html -->
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

```css
/* style.css */
p {
  color: blue;
}
```

**Always use the external file method.** It keeps your HTML clean and your CSS reusable across multiple pages.

### 5.1 CSS Selectors — How to Target Elements

```css
/* Element selector — targets ALL <p> tags */
p {
  color: red;
}

/* Class selector — targets elements with class="highlight" */
.highlight {
  background: yellow;
}

/* ID selector — targets the element with id="banner" */
#banner {
  font-size: 24px;
}

/* Descendant selector — targets <span> inside <p> */
p span {
  color: green;
}

/* Direct child selector — only direct children of <div> */
div > p {
  margin: 10px;
}

/* Multiple selectors — comma means "and also" */
h1, h2, h3 {
  font-family: Arial;
}

/* Attribute selector — inputs with type="text" */
input[type="text"] {
  border: 1px solid gray;
}

/* Pseudo-class — special state */
button:hover {
  background: darkblue;
}

button:disabled {
  opacity: 0.5;
}

/* Pseudo-element — part of an element */
p::first-line {
  font-weight: bold;
}
```

### 5.2 The Cascade — Which Style Wins?

When multiple CSS rules target the same element, there's a priority system called **specificity**:

```
1. Inline styles  (style="" attribute)       ← Wins first
2. ID selector    (#myId)
3. Class selector (.myClass)
4. Element selector (div, p)                  ← Loses last
```

Plus the special card: `!important` (but use it like a fire extinguisher — only in emergencies):

```css
p {
  color: red !important;  /* This will beat everything */
}
```

**Pro tip:** Avoid `!important` whenever possible. It makes debugging a nightmare.

### 5.3 Colors in CSS

```css
/* Named colors */
color: red;
color: blue;
color: tomato;
color: rebeccapurple;
/* ...147 named colors in total */

/* Hex codes (most common) */
color: #ff0000;    /* Red */
color: #00ff00;    /* Green */
color: #0000ff;    /* Blue */
color: #2b6cb0;    /* Dark blue */
color: #333333;    /* Dark gray (short: #333) */

/* RGB */
color: rgb(255, 0, 0);       /* Red */
color: rgba(255, 0, 0, 0.5); /* Red at 50% opacity */

/* HSL (Hue, Saturation, Lightness) */
color: hsl(0, 100%, 50%);    /* Red */
```

**Getting colors:** Use a color picker (VS Code has one built-in — hover over a color in CSS), or use sites like [coolors.co](https://coolors.co) for palettes.

### 5.4 Units — Pixels, Percentages, and Friends

| Unit | Relative to | Example | Good for |
|---|---|---|---|
| `px` | Nothing (absolute) | `width: 100px` | Borders, images |
| `%` | Parent element | `width: 50%` | Layout widths |
| `rem` | Root font size | `font-size: 1.5rem` | **Font sizes** (accessibility!) |
| `em` | Current element's font size | `padding: 2em` | Spacing relative to text |
| `vw` | Viewport width (1vw = 1%) | `width: 100vw` | Full-width sections |
| `vh` | Viewport height (1vh = 1%) | `height: 90vh` | Hero sections |
| `fr` | Fraction (CSS Grid) | `grid-template: 1fr 2fr` | Grid layouts |

**Critical pro tip:** Use `rem` for font sizes, not `px`. Why? Users can change their browser's base font size. If you use `px`, your text won't scale. If you use `rem`, it respects user preferences. This is accessibility.

### 5.5 The Box Model — THE MOST IMPORTANT CSS CONCEPT

Every single element on a web page is a rectangle. Each rectangle has layers:

```
┌───────────────────────────────────────────────────┐
│                    MARGIN                          │
│   (Invisible space OUTSIDE the border)            │
│                                                     │
│   ┌───────────────────────────────────────────┐   │
│   │              BORDER                        │   │
│   │   (Visible or invisible line around the   │   │
│   │    element)                               │   │
│   │                                             │   │
│   │   ┌───────────────────────────────────┐   │   │
│   │   │           PADDING                 │   │   │
│   │   │  (Space INSIDE the border,        │   │   │
│   │   │   outside the content)            │   │   │
│   │   │                                     │   │   │
│   │   │   ┌───────────────────────────┐   │   │   │
│   │   │   │        CONTENT            │   │   │   │
│   │   │   │   (Text, images, etc.)    │   │   │   │
│   │   │   └───────────────────────────┘   │   │   │
│   │   └───────────────────────────────────┘   │   │
│   └───────────────────────────────────────────┘   │
└───────────────────────────────────────────────────┘
```

```css
.box {
  /* Content dimensions */
  width: 300px;
  height: 200px;

  /* Padding — space INSIDE the box */
  padding-top: 10px;
  padding-right: 15px;
  padding-bottom: 10px;
  padding-left: 15px;

  /* Shorthand: top right bottom left */
  padding: 10px 15px 10px 15px;

  /* Even shorter: top/bottom left/right */
  padding: 10px 15px;

  /* Even shorter: same on all sides */
  padding: 15px;

  /* Border */
  border-width: 2px;
  border-style: solid;
  border-color: black;

  /* Shorthand */
  border: 2px solid black;

  /* Only bottom border */
  border-bottom: 3px dashed #ccc;

  /* Rounded corners */
  border-radius: 8px;         /* All corners */
  border-radius: 50%;         /* Circle! */

  /* Margin — space OUTSIDE the box */
  margin-bottom: 20px;
  margin: 0 auto;             /* Center horizontally */
}
```

#### The Gotcha — `width` Doesn't Include Padding or Border

By default, if you say `width: 300px`, that's the *content* width. Padding and border are ADDED on top.

```css
.box {
  width: 300px;
  padding: 20px;
  border: 5px solid;
}
/* Actual width = 300 + 20 + 20 + 5 + 5 = 350px */
```

**Fix it with box-sizing:**

```css
* {
  box-sizing: border-box;
  /* Now width INCLUDES padding and border */
}
/* Actual width = 300px (content shrinks to fit) */
```

**Every professional developer adds this to their CSS.** Do it from day one.

### 5.6 Flexbox — The Swiss Army Knife of Layout

Before Flexbox, centering things was a nightmare. Developer lore says centering a div was once a rite of passage that took years to master. People posted forum threads at 3 AM. Therapists made a fortune.

Then Flexbox arrived. And now centering is two lines:

```css
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

Congrats. You just solved what broke our ancestors.

**Flexbox is like a god-tier IKEA organizer.** It looks at a container, looks at its items, and arranges them perfectly — equal spacing, centering, wrapping, whatever. You just tell it the rules.

#### How Flexbox Thinks

Every flex container has two axes:

```
flex-direction: row
──────────────────────────────────────────
  MAIN AXIS  ──────────────────────────>
  (justify-content controls this)
  
  CROSS AXIS  ↓
  (align-items controls this)

flex-direction: column
──────────────────────────────────────────
  CROSS AXIS  ──────────────────────────>
  (align-items controls this)
  
  MAIN AXIS   ↓
  (justify-content controls this)
```

**Mental model:** Imagine a cafeteria tray line. The main axis is the direction the trays move. The cross axis is the side-to-side. `justify-content` spaces things along the tray line. `align-items` positions them on the tray.

#### Flexbox Directions

```css
.flex-row {
  display: flex;
  flex-direction: row;         /* → → →  items left to right */
}

.flex-column {
  display: flex;
  flex-direction: column;      /* ↓ ↓ ↓  items top to bottom */
}

.flex-row-reverse {
  display: flex;
  flex-direction: row-reverse; /* ← ← ←  right to left */
}
```

#### The Parent Properties — What YOU Control

```css
.parent {
  display: flex;

  /* Where items sit on the main axis */
  justify-content: flex-start;    /* Pack to start (default) */
  justify-content: flex-end;      /* Pack to end */
  justify-content: center;        /* Squeeze together in the middle */
  justify-content: space-between; /* First & last at edges, rest equal */
  justify-content: space-around;  /* Equal space around each item */
  justify-content: space-evenly;  /* Truly equal everything */

  /* Where items sit on the cross axis */
  align-items: stretch;     /* Stretch to fill height (default) */
  align-items: flex-start;  /* Stick to top */
  align-items: flex-end;    /* Stick to bottom */
  align-items: center;      /* Vertically centered */

  /* Should items wrap or squeeze? */
  flex-wrap: nowrap;    /* All in one line, even if they overflow */
  flex-wrap: wrap;      /* Wrap to next line if no space */

  /* Gap between items */
  gap: 16px;            /* Space between flex children */
  gap: 1rem;            /* Responsive gap */
}
```

**Real talk:** You'll use `justify-content: center`, `space-between`, and `align-items: center` for about 90% of your flexbox layouts. The rest is for special occasions.

#### The Child Properties — Letting Items Be Individuals

```css
.child {
  /* Grow to fill available space — the "greedy" property */
  flex: 1;       /* Take up equal remaining space */

  /* Three values: grow shrink basis */
  flex: 0 0 200px;  /* Don't grow, don't shrink, stay 200px wide */

  /* Don't grow OR shrink */
  flex: none;

  /* Override align-items for THIS specific child */
  align-self: center;
  align-self: stretch;

  /* Reorder (like priority boarding) */
  order: 2;        /* Default is 0. Higher = later */
  order: -1;       /* Show this FIRST */
}
```

**`flex: 1` is the single most useful flex property for children.** It says "take whatever space is left over." Multiple children with `flex: 1` share the space equally. It's the platonic ideal of fair distribution.

#### Real-World Flexbox Patterns

**1. Nav Bar — Logo left, links right:**
```css
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

**2. Card row that wraps on mobile:**
```css
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
.card {
  flex: 1 1 300px;  /* Grow, shrink, base width 300px */
}
```

**3. Holy grail — fixed sidebar, flexible content:**
```css
.layout {
  display: flex;
}
.sidebar {
  flex: 0 0 250px;  /* Fixed 250px sidebar */
}
.main {
  flex: 1;           /* Fills everything else */
}
```

**4. Vertical centering — the "hero section":**
```css
.hero {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;   /* Full viewport height */
}
```

#### Your Turn

Build a card layout:
1. Container with 6 cards, `display: flex`, `flex-wrap: wrap`, `gap: 16px`
2. Each card: `flex: 1 1 280px`, padding, border, shadow
3. Add a nav bar with logo on left, three links on right

### 5.7 CSS Grid — 2D Layouts Made Easy

**Flexbox is for one direction (row OR column). Grid is for both directions at once (row AND column).**

Think of Flexbox as a single line of people waiting for coffee. Grid is the entire seating chart of the coffee shop — rows AND columns, with some tables spanning multiple spots.

```css
.grid-container {
  display: grid;

  /* Define your columns */
  grid-template-columns: 200px 1fr 200px;  /* Three columns: fixed, flexible, fixed */
  grid-template-columns: repeat(3, 1fr);   /* Three equal columns */

  /* Define your rows */
  grid-template-rows: auto 1fr auto;       /* Header auto-height, content fills, footer auto */

  /* Gap between cells */
  gap: 20px;
}
```

#### The `fr` Unit — Flexbox's Cousin Moved In

`fr` = **fraction of available space**. Like `flex: 1` but for grid.

```css
grid-template-columns: 1fr 2fr 1fr;
/* 4 fractions total: first takes 1/4, second takes 2/4 (half), third takes 1/4 */
```

| Value | Meaning |
|---|---|
| `1fr` | One fraction of remaining space |
| `repeat(3, 1fr)` | Three equal columns — shorthand |
| `auto` | Size to content (text length, image width) |
| `200px` | Fixed size — will never change |
| `minmax(200px, 1fr)` | At least 200px, then grow if space |

**Smart responsive pattern — no media queries needed:**
```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 16px;
}
```

This says: "Put as many 250px-wide columns as fit, and make them grow to fill the screen." Resize the browser — it just works. No `@media` lines, no breakpoints, no drama.

#### Grid Template Areas — The Cheat Code

Instead of counting columns, name your areas and draw the layout:

```css
.layout {
  display: grid;
  grid-template-areas:
    "header  header  header"
    "sidebar content content"
    "sidebar content content"
    "footer  footer  footer";
  grid-template-columns: 200px 1fr 1fr;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
  gap: 4px;
}

header  { grid-area: header; }
aside   { grid-area: sidebar; }
main    { grid-area: content; }
footer  { grid-area: footer; }
```

**This is a full-page layout in 15 lines of CSS.** No flexbox nesting, no hacks. It reads like a blueprint.

```
┌────────────────────────────────────┐
│             header                  │
├──────────┬─────────────────────────┤
│          │                         │
│ sidebar  │       content           │
│          │                         │
├──────────┴─────────────────────────┤
│             footer                  │
└────────────────────────────────────┘
```

#### Spanning Items Across Multiple Cells

Some items deserve more space:

```css
.featured-card {
  grid-column: span 2;  /* This card takes TWO columns */
  grid-row: span 2;     /* And TWO rows */
}

.full-width-banner {
  grid-column: 1 / -1;  /* Start at column 1, end at the LAST column */
}
```

#### Grid vs Flexbox — The Honest Showdown

| Situation | Pick |
|---|---|
| A row of nav links | **Flexbox** |
| A column of stacked sections | **Flexbox** |
| Centering a thing | **Flexbox** |
| Image gallery (rows AND columns) | **Grid** |
| Full page layout (header + sidebar + content + footer) | **Grid** |
| Cards that wrap to next line | **Flexbox** (or Grid with `auto-fit`) |
| Dashboard / analytics panels | **Grid** |
| You're fighting with Flexbox for 20 minutes | **Switch to Grid** |

**The 80/20 rule:** Use Flexbox for 80% of your layouts. That remaining 20% — page layouts, galleries, dashboards — is what Grid was born for.

#### Your Turn

1. Create the full-page layout from the diagram above using `grid-template-areas`
2. Build an image gallery with `auto-fit minmax(200px, 1fr)` — add 8 placeholder images
3. Make one image span 2 columns and 2 rows like a featured photo

### 5.8 Responsive Design — Making Your Site Work on Phones

More than 60% of web traffic is on mobile. If your site doesn't work on a phone, half your visitors leave.

#### The Viewport Meta Tag (Required for Mobile)

```html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

**Without it:** Your site looks zoomed out on mobile (like a tiny version of the desktop site).

**With it:** Your site uses the actual screen width.

#### Media Queries — Different Styles for Different Screens

```css
/* Default styles are for desktop first */

/* Tablet and below */
@media (max-width: 768px) {
  .sidebar {
    display: none;
  }
  .content {
    width: 100%;
  }
}

/* Phone and below */
@media (max-width: 480px) {
  body {
    font-size: 14px;
  }
  .nav-links {
    flex-direction: column;
  }
}
```

**Mobile-First vs Desktop-First**

```css
/* Mobile-First Approach */
/* Base styles = phone */
body { font-size: 14px; }

/* Tablet */
@media (min-width: 768px) {
  body { font-size: 16px; }
}

/* Desktop */
@media (min-width: 1024px) {
  body { font-size: 18px; }
}
```

**Pro tip:** Start with mobile styles (they're simpler), then add complexity for larger screens.

### 5.9 Common CSS Patterns You'll Use Every Day

#### Centering (THE most asked question)

```css
/* Center text */
text-align: center;

/* Center a block element horizontally */
margin: 0 auto;

/* Center everything inside a flex container */
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

#### Card Component

```css
.card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  /* That 4-value shadow: x-offset y-offset blur color */
}
```

#### Sticky Header

```css
header {
  position: fixed;       /* Stays at the top when scrolling */
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;          /* Stays on top of other content */
  background: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

body {
  padding-top: 60px;     /* Prevent content from hiding under the header */
}
```

#### Full-Page Hero Section

```css
.hero {
  height: 100vh;            /* Full viewport height */
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to right, #667eea, #764ba2);
  color: white;
}
```

### Your Turn — Mini Project: Style Your Recipe Page

Take the recipe page from Chapter 4 and add CSS:
1. A nice background color (not white)
2. Cards for the ingredients and steps sections
3. The title centered and in a nice color
4. Rounded corners on the image
5. The list items should have some spacing
6. Add a hover effect on links
7. Make it look good on mobile (add a media query)

### 5.10 CSS Animations & Transitions — Making Things Move

CSS can move, fade, pulse, and transform elements. Two main tools:

**Transitions** — smooth changes between states (like hover). **Animations** — multi-step keyframe sequences that can loop.

#### Transitions: The Easy Path

```css
.button {
  background: blue;
  transition: all 0.3s ease;  /* property duration timing-function */
}
.button:hover {
  background: darkblue;
  transform: scale(1.05);      /* Grows slightly on hover */
}
```

Without `transition`, the color change is instant (jarring). With it, it fades smoothly over 0.3 seconds. The `ease` means "start slow, speed up, end slow" — the most natural feel.

**Common `transition` properties:**
- `opacity` — great for fade in/out
- `transform` — for movement, scaling, rotation
- `background-color` — for hover effects
- `box-shadow` — for "lift" effects

```css
.card {
  transition: transform 0.2s, box-shadow 0.2s;
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgba(0,0,0,0.15);
}
```

#### Keyframe Animations: Full Control

For more complex sequences, use `@keyframes`:

```css
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero-title {
  animation: fadeIn 1s ease forwards;
  /* name duration timing-fn fill-mode */
}
```

`forwards` means "keep the final state" (so it stays visible after the animation ends).

**Multi-step example:**

```css
@keyframes pulse {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.05); }
  100% { transform: scale(1); }
}

.notification {
  animation: pulse 2s ease infinite;  /* infinite = loops forever */
}
```

**Animation properties:**
- `animation-name` — the keyframes name
- `animation-duration` — how long (0.5s, 2s, etc.)
- `animation-timing-function` — ease, linear, ease-in-out
- `animation-delay` — wait before starting
- `animation-iteration-count` — 1, 3, infinite
- `animation-direction` — normal, reverse, alternate (back and forth)
- `animation-fill-mode` — forwards (keep end), backwards (use start before delay)

#### Best Practices

| Do | Don't |
|---|---|
| Animate `transform` and `opacity` (GPU-accelerated) | Animate `width`, `height`, `top`, `left` (slow) |
| Keep animations short (0.2s-0.5s) | Use 2+ second transitions |
| Use `prefers-reduced-motion` for accessibility | Forget people with motion sensitivity |
| Test on mobile (60fps is harder there) | Animate 10 things at once |

**Accessibility snippet:**
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

This turns off animations for users who've set their OS to reduce motion. Every production site should include this.

#### Your Turn

Add to your recipe page:
1. A fade-in animation on page load for the main heading
2. Hover effect on the recipe card (slight lift)
3. A pulse animation on a "NEW" badge
4. Use `prefers-reduced-motion` to disable all if needed

Don't worry if it's not beautiful — you're learning. Every CSS master started with ugly websites.

---

## 6. JavaScript — Bringing Your Site to Life

### What is JavaScript?

HTML is the body, CSS is the clothes, JavaScript is the **brain**.

Without JavaScript, a website is just a poster — you can look at it but that's it. JavaScript makes things happen when you click, type, scroll, or breathe on the page.

### 6.1 JavaScript is Everywhere

```
JavaScript in the browser (client-side):
  - Animations
  - Button clicks
  - Form validation
  - Fetching data from servers
  - Games

JavaScript on the server (Node.js):
  - Building APIs
  - Processing data
  - Talking to databases
  - Authentication

JavaScript on your phone (React Native):
  - Mobile apps

JavaScript on your desktop (Electron):
  - VS Code is written in JavaScript!
  - Slack, Discord, Spotify Desktop
```

### 6.2 Adding JavaScript to Your Page

```html
<!-- Inline (bad for anything beyond one line) -->
<button onclick="alert('Hello!')">Click</button>

<!-- In a script tag (okay for small examples) -->
<body>
  <button id="myBtn">Click</button>
  <script>
    document.getElementById('myBtn').addEventListener('click', () => {
      alert('Hello!');
    });
  </script>
</body>

<!-- External file (best practice) -->
<body>
  <button id="myBtn">Click</button>
  <script src="app.js"></script>
</body>
```

**Where to put your script tag?** Right before `</body>`. Why? Because JavaScript runs IMMEDIATELY when the browser encounters it. If you put it in `<head>`, the HTML hasn't loaded yet and your JS can't find any elements.

Alternative (modern): add `defer` to your script tag in `<head>`:

```html
<head>
  <script src="app.js" defer></script>
</head>
```

`defer` says: "Download the script but don't run it until the page is fully loaded."

### 6.3 Variables — Storing Information

Variables are labeled boxes where you put data.

```javascript
// Three ways to create a variable:

let name = 'Alice';        // Can change later
const birthYear = 1998;     // Can NEVER change
var oldWay = 'Avoid this'; // Outdated, don't use
```

**The golden rule:** Use `const` by default. Only use `let` if you KNOW the value will change.

```javascript
const name = 'Alice';
name = 'Bob';  // ❌ Error! Can't reassign a const

let age = 25;
age = 26;      // ✅ OK! Let can be reassigned
```

### 6.4 Data Types — What Kind of Box?

```javascript
// Strings (text) — use quotes
const name = 'Alice';
const greeting = "Hello";
const template = `Hi, ${name}!`;  // Template literal (backticks!)

// Numbers
const age = 25;
const price = 19.99;
const negative = -5;

// Booleans (true/false)
const isLoggedIn = true;
const isAdmin = false;

// Arrays (lists)
const fruits = ['apple', 'banana', 'orange'];
const mixed = [1, 'hello', true];  // Arrays can hold any type
const matrix = [[1, 2], [3, 4]];   // Nested arrays

// Objects (key-value pairs)
const person = {
  name: 'Alice',
  age: 25,
  isStudent: true,
  greet: function() {
    console.log(`Hello, I'm ${this.name}`);
  }
};

// Null (intentionally empty)
const nothing = null;

// Undefined (declared but not assigned)
let something;
console.log(something);  // undefined
```

**Template literals (backticks) are your friend:**

```javascript
const name = 'Alice';
const age = 25;

// Old way (concatenation):
console.log('My name is ' + name + ' and I am ' + age + ' years old.');

// New way (template literal):
console.log(`My name is ${name} and I am ${age} years old.`);
```

### 6.5 The `console` — Your Debugging Best Friend

```javascript
console.log('Hello!');           // Print a message
console.log('Value:', x);        // Print a label and value
console.error('Something broke'); // Print in red (for errors)
console.warn('Be careful');      // Print in yellow (for warnings)
console.table(array);             // Print as a table

// You can write any expression inside console.log:
console.log(2 + 2);              // 4
console.log('Hello'.toUpperCase()); // 'HELLO'
```

**Pro tip:** You can type any JavaScript directly into your browser's console (F12 → Console tab) and see immediate results. It's a playground.

### 6.6 Operators — Doing Things With Data

```javascript
// Arithmetic
5 + 3     // 8  (addition)
10 - 4    // 6  (subtraction)
3 * 4     // 12 (multiplication)
15 / 3    // 5  (division)
17 % 5    // 2  (modulo — remainder)
2 ** 3    // 8  (exponent — 2 to the power of 3)

// Comparison (always return true or false)
5 === 5   // true  (strict equal — checks type too)
5 === '5' // false (number vs string)
5 !== 5   // false (not equal)
5 > 3     // true
5 >= 5    // true
5 < 3     // false

// AVOID these (loose comparison):
5 == '5'  // true  (bad — JavaScript converts types for you)
5 != '5'  // false (bad)

// Logical
true && false   // false (AND — both must be true)
true || false   // true  (OR — at least one true)
!true           // false (NOT — flips true to false)

// Assignment shortcuts
let x = 10;
x += 5;   // x = x + 5 → 15
x -= 3;   // x = x - 3 → 12
x *= 2;   // x = x * 2 → 24
x++;      // x = x + 1 → 25
x--;      // x = x - 1 → 24
```

### 6.7 Conditionals — Making Decisions

```javascript
const age = 18;

// if / else if / else
if (age >= 18) {
  console.log('You can vote');
} else if (age >= 16) {
  console.log('You can drive but not vote');
} else {
  console.log('Too young for both');
}
// Output: "You can vote"

// Multiple conditions
const isWeekend = true;
const isHoliday = false;

if (isWeekend || isHoliday) {
  console.log('No work today!');
} else {
  console.log('Time to work');
}

// Truthy and Falsy
// Values that act like "false" in conditions:
// false, 0, "" (empty string), null, undefined, NaN

const name = '';
if (name) {
  console.log('Hello, ' + name);
} else {
  console.log('No name provided');
}
// Output: "No name provided"

// Ternary operator — shorthand if/else
const age = 20;
const canVote = age >= 18 ? 'Yes' : 'No';
//                      │      │       │
//                 condition  if true  if false
console.log(canVote); // "Yes"

// Switch statement — many conditions
const day = 3;
let dayName;

switch (day) {
  case 1:
    dayName = 'Monday';
    break;
  case 2:
    dayName = 'Tuesday';
    break;
  case 3:
    dayName = 'Wednesday';
    break;
  // ...etc
  default:
    dayName = 'Unknown';
}
```

### 6.8 Loops — Doing Things Over and Over

```javascript
// For loop — when you know how many times
for (let i = 0; i < 5; i++) {
  console.log(i);  // 0, 1, 2, 3, 4
}

// Breaking down the for loop:
// for (start; condition; step)
//   let i = 0;     → start here
//   i < 5;         → keep going while this is true
//   i++            → do this after each iteration

// Looping through an array
const fruits = ['apple', 'banana', 'orange', 'grape'];

// Old way:
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}

// Modern way (for...of):
for (const fruit of fruits) {
  console.log(fruit);
}

// While loop — when you don't know how many times
let count = 0;
while (count < 5) {
  console.log(count);
  count++;
}

// Do...while — runs at least once
let x = 10;
do {
  console.log(x);
  x++;
} while (x < 5);
// Output: 10 (runs once even though condition is false)
```

### 6.9 Functions — Reusable Blocks of Code

```javascript
// Function declaration (hoisted — can be called before definition)
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet('Alice'));  // "Hello, Alice!"

// Function with multiple parameters
function add(a, b) {
  return a + b;
}
console.log(add(5, 3));  // 8

// Default parameters
function greet(name = 'stranger') {
  return `Hello, ${name}!`;
}
console.log(greet());      // "Hello, stranger!"
console.log(greet('Bob')); // "Hello, Bob!"

// Arrow functions (modern, shorter)
const greet = (name) => {
  return `Hello, ${name}!`;
};

// Even shorter — single parameter, no parentheses needed
const greet = name => `Hello, ${name}!`;

// Multiple parameters with arrow
const add = (a, b) => a + b;

// Function without return (returns undefined)
function logMessage(msg) {
  console.log(msg);
  // No return statement → returns undefined
}

const result = logMessage('Hi');
console.log(result);  // undefined
```

**Functions vs Arrow Functions — The Real Difference:**

```javascript
// Regular function
function regular() {
  console.log(arguments);  // ✅ Has arguments object
  console.log(this);       // ✅ Has its own this
}

// Arrow function
const arrow = () => {
  console.log(arguments);  // ❌ Error, no arguments object
  console.log(this);       // ✅ Inherits this from surrounding scope
};
```

For 95% of what you'll do, arrow functions work perfectly. Use them by default.

### 6.10 Arrays — Working with Lists

Arrays are the workhorses of JavaScript. Learn these methods:

```javascript
const fruits = ['apple', 'banana', 'orange'];

// Adding and removing
fruits.push('grape');         // Add to end → ['apple', 'banana', 'orange', 'grape']
const last = fruits.pop();    // Remove from end → last = 'grape'
fruits.unshift('kiwi');       // Add to beginning
const first = fruits.shift(); // Remove from beginning

// Finding things
fruits.indexOf('banana');     // 1 (position)
fruits.includes('apple');     // true
fruits.find(f => f.startsWith('b')); // 'banana' (first match)
fruits.findIndex(f => f === 'orange'); // 2

// Filtering (creates new array)
const numbers = [1, 2, 3, 4, 5, 6];
const evens = numbers.filter(n => n % 2 === 0);
// [2, 4, 6]

// Transforming (creates new array)
const doubled = numbers.map(n => n * 2);
// [2, 4, 6, 8, 10, 12]

// Checking
numbers.some(n => n > 5);     // true (at least one matches)
numbers.every(n => n > 0);    // true (all match)
numbers.every(n => n > 3);    // false

// Reducing (accumulate values)
const sum = numbers.reduce((total, current) => total + current, 0);
// 21

// Sorting
fruits.sort();                // Alphabetical: ['apple', 'banana', 'orange']
numbers.sort((a, b) => a - b); // Numeric ascending
numbers.sort((a, b) => b - a); // Numeric descending

// Slicing and splicing
numbers.slice(1, 4);  // [2, 3, 4] (from index 1 to 4, not including 4)
numbers.splice(2, 1); // Remove 1 item at index 2

// Joining
fruits.join(', ');    // 'apple, banana, orange'

// Spreading (copy and combine)
const moreFruits = [...fruits, 'mango'];        // Copy + add
const combined = [...fruits, ...moreFruits];    // Merge two arrays
```

**Pro tip:** In modern JavaScript, you'll rarely use `for` loops for arrays. Use `map`, `filter`, `find`, and `forEach` instead. They're cleaner and less error-prone.

### 6.11 Objects — Grouping Related Data

```javascript
const user = {
  name: 'Alice',
  age: 25,
  email: 'alice@example.com',
  isAdmin: false,
  hobbies: ['reading', 'coding', 'hiking']
};

// Accessing properties
console.log(user.name);      // 'Alice'  (dot notation)
console.log(user['name']);   // 'Alice'  (bracket notation — useful for dynamic keys)

// Modifying
user.age = 26;
user['email'] = 'alice@new.com';

// Adding new properties
user.phone = '555-1234';
user['address'] = '123 Main St';

// Deleting
delete user.isAdmin;

// Checking if property exists
console.log('name' in user);     // true
console.log(user.phone !== undefined); // true

// Getting all keys or values
Object.keys(user);     // ['name', 'age', 'email', 'hobbies', 'phone', 'address']
Object.values(user);   // ['Alice', 26, 'alice@new.com', [...], '555-1234', '123 Main St']
Object.entries(user);  // [['name', 'Alice'], ['age', 26], ...]

// Looping through an object
for (const key of Object.keys(user)) {
  console.log(`${key}: ${user[key]}`);
}

// Destructuring — extract properties into variables
const { name, age, email } = user;
console.log(name);  // 'Alice'
// Equivalent to:
// const name = user.name;
// const age = user.age;
// const email = user.email;
```

### 6.12 The DOM — JavaScript Meets HTML

The **Document Object Model** is the bridge between your JavaScript and your HTML. When you write HTML, the browser creates a tree-like structure:

```
document
 └── html
      ├── head
      │    ├── title ─── "My Page"
      │    ├── meta
      │    └── link
      └── body
           ├── h1 ─── "Hello World"
           ├── p  ─── "This is a paragraph"
           └── div ─── class="container"
                ├── button ─── id="myBtn" ─── "Click"
                └── input ─── type="text"
```

JavaScript can walk this tree, find elements, and change them.

```javascript
// === SELECTING ELEMENTS ===

// Find by ID (fastest, most common)
const header = document.getElementById('header');

// Find by CSS selector (returns first match)
const firstCard = document.querySelector('.card');

// Find by CSS selector (returns all matches)
const allCards = document.querySelectorAll('.card');
// Returns a NodeList — loop with forEach
allCards.forEach(card => console.log(card));

// Find by class name (older)
const cards = document.getElementsByClassName('card');

// === MANIPULATING ELEMENTS ===

// Change text
header.textContent = 'New Header Text';

// Change HTML (be careful with this — security risk)
header.innerHTML = 'New <em>HTML</em> Content';

// Change styles
header.style.color = 'red';
header.style.fontSize = '24px';
header.style.backgroundColor = 'blue';
// CSS property names become camelCase in JavaScript:
// background-color → backgroundColor
// font-size → fontSize
// margin-top → marginTop

// Add/remove/toggle classes
header.classList.add('highlight');
header.classList.remove('dim');
header.classList.toggle('active');

// Check if element has a class
header.classList.contains('highlight');  // true or false

// Change attributes
header.setAttribute('data-id', '123');
console.log(header.getAttribute('data-id'));  // '123'
header.removeAttribute('data-id');

// === CREATING AND REMOVING ELEMENTS ===

// Create a new element
const newParagraph = document.createElement('p');
newParagraph.textContent = 'I was created by JavaScript!';

// Add it to the page
document.body.appendChild(newParagraph);     // At the end
document.body.prepend(newParagraph);         // At the beginning
document.querySelector('.container').appendChild(newParagraph); // Inside container

// Insert before another element
const reference = document.querySelector('.existing');
document.body.insertBefore(newParagraph, reference);

// Remove an element
const oldElement = document.getElementById('old');
oldElement.remove();  // Modern
// OR: oldElement.parentNode.removeChild(oldElement);  // Old way
```

### 6.13 Events — Making Things Interactive

Events are things that happen in the browser. JavaScript can listen for them and react.

```javascript
// === CLICK EVENTS ===

const button = document.getElementById('myBtn');

// The modern way
button.addEventListener('click', (event) => {
  console.log('Button was clicked!');
  console.log('Event target:', event.target);       // The element clicked
  console.log('Event type:', event.type);           // 'click'
  console.log('Coordinates:', event.clientX, event.clientY);  // Mouse position
});

// === FORM EVENTS ===

const form = document.getElementById('myForm');
form.addEventListener('submit', (event) => {
  event.preventDefault();  // →— VERY IMPORTANT — stops page from reloading

  const nameInput = document.getElementById('name');
  console.log('Submitted value:', nameInput.value);
});

// === INPUT EVENTS ===

const searchInput = document.getElementById('search');
searchInput.addEventListener('input', (event) => {
  console.log('Typing:', event.target.value);
  // This fires on EVERY keystroke — great for live search
});

// === KEYBOARD EVENTS ===

document.addEventListener('keydown', (event) => {
  console.log('Key pressed:', event.key);
  if (event.key === 'Enter') {
    console.log('You pressed Enter!');
  }
  if (event.key === 'Escape') {
    console.log('You pressed Escape!');
  }
});

// === MOUSE EVENTS ===

element.addEventListener('mouseenter', () => console.log('Mouse entered'));
element.addEventListener('mouseleave', () => console.log('Mouse left'));
element.addEventListener('mousemove', (e) => console.log(e.clientX, e.clientY));

// === SCROLL EVENTS ===

window.addEventListener('scroll', () => {
  console.log('Scrolled:', window.scrollY);
});

// === PAGE EVENTS ===

// When the page loads
document.addEventListener('DOMContentLoaded', () => {
  console.log('Page is ready!');
});

// === EVENT OBJECT PROPERTIES ===

element.addEventListener('click', (e) => {
  e.target         // The element that was actually clicked
  e.currentTarget  // The element the listener is attached to
  e.preventDefault()  // Stop default behavior (like form submitting)
  e.stopPropagation() // Stop event from bubbling up
  e.clientX, e.clientY  // Mouse position relative to viewport
  e.key             // Which key was pressed (for keyboard events)
});
```

### 6.14 Event Delegation — One Listener to Rule Them All

If you have 100 buttons, do you add 100 event listeners? **No.** You add ONE on their parent.

```javascript
// ❌ BAD — 100 listeners for 100 buttons
document.querySelectorAll('.delete-btn').forEach(btn => {
  btn.addEventListener('click', () => deleteItem());
});

// ✅ GOOD — 1 listener for all buttons
document.querySelector('.list').addEventListener('click', (e) => {
  const button = e.target.closest('.delete-btn');
  if (!button) return; // Wasn't a delete button, ignore
  deleteItem(button.dataset.id);
});
```

**Why event delegation?**
- Uses less memory (one listener vs hundreds)
- Works for FUTURE elements (add a new button dynamically and it works automatically)
- Cleaner code

### 6.15 Async/Await — Waiting for Things

Some operations take time: fetching data from a server, reading a file, waiting 3 seconds. JavaScript doesn't wait (it's "non-blocking" by default). `async/await` makes it wait gracefully.

```javascript
// === THE PROBLEM ===

function fetchData() {
  // This takes time...
  return 'data';
}

const result = fetchData();
console.log(result);  // Works because it's instant

// But what if it's not instant?

// === THE SOLUTION: async/await ===

// An async function always returns a Promise
async function fetchData() {
  // Simulate a 2-second delay
  await new Promise(resolve => setTimeout(resolve, 2000));
  return 'data';
}

// You must await an async function
async function main() {
  const result = await fetchData();
  console.log(result); // 'data' (after 2 seconds)
}

main();

// === REAL EXAMPLE: Fetching from an API ===

async function getUsers() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Failed to fetch users:', error);
    return [];
  }
}

// === THREE WAYS TO WRITE THE SAME THING ===

// Old way: Promises with .then()
fetch('/api/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Modern way: async/await
async function getData() {
  try {
    const response = await fetch('/api/data');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Parallel requests: Promise.all
async function getMultipleData() {
  const [users, posts, comments] = await Promise.all([
    fetch('/api/users').then(r => r.json()),
    fetch('/api/posts').then(r => r.json()),
    fetch('/api/comments').then(r => r.json()),
  ]);
  // All three requests happen AT THE SAME TIME
  // Much faster than doing them one by one
}
```

**Remember:** `await` can only be used inside `async` functions. Think of it like a "pause here until you get a result" button.

### 6.16 Error Handling — Try/Catch

Things go wrong. The internet goes down. Users type letters in number fields. Servers crash. `try/catch` keeps your app from exploding:

```javascript
async function getData() {
  try {
    // Try this code...
    const response = await fetch('https://api.example.com/data');
    
    if (!response.ok) {
      throw new Error(`Server returned ${response.status}`);
    }
    
    return await response.json();
    
  } catch (error) {
    // If ANYTHING in try block throws an error, run this:
    console.error('Something went wrong:', error.message);
    
    // Show user a friendly message instead of a blank page
    document.getElementById('error-message').textContent = 
      'Could not load data. Please check your connection.';
    
    return null; // Return a safe default
  } finally {
    // This runs whether it succeeded or failed (optional)
    console.log('Request finished');
  }
}
```

**Pro tip:** Always, ALWAYS handle errors when fetching data. A failed API call should never crash your entire app.

### Your Turn — Mini Project: Interactive To-Do List

Create a to-do list app with:
1. An input field and "Add" button
2. Clicking "Add" creates a new item in the list
3. Clicking an item toggles it as completed (strikethrough)
4. A "Delete" button next to each item
5. A count showing how many items are left

Don't worry about saving data yet (no database) — just get it working in the browser.

---

## 7. The Backend — What Happens Behind the Scenes

So far, everything has been happening in the browser. Now we're going to build something that lives on a server.

### 7.1 What is a Server?

A server is just a computer that's always on, connected to the internet, and running software that responds to requests.

Your laptop can be a server. The computer in your basement can be a server. A machine at Amazon (AWS) that costs pennies per hour can be a server.

**When you visit a website:**

```
Your Browser                    The Server
    │                               │
    │  "Give me the homepage"       │
    │ ──────────────────────────>   │
    │                               │
    │  "Here's the HTML/CSS/JS"     │
    │ <──────────────────────────   │
    │                               │
    │  "Oh wait, I need user data"  │
    │ ──────────────────────────>   │
    │                               │
    │  "Here's the JSON data"       │
    │ <──────────────────────────   │
```

### 7.2 Node.js — JavaScript on the Server

You already installed Node.js in Chapter 3. Now let's use it.

**Node.js lets you run JavaScript outside the browser.** This means:
- No `document.getElementById` (there's no browser)
- No `window` or `alert`
- But you DO have file system access, networking, etc.

### 7.3 Your First Server

**Step 1:** Create a new folder and open it in VS Code:

```bash
mkdir my-first-server
cd my-first-server
code .
```

**Step 2:** Initialize npm:

```bash
npm init -y
```

This creates `package.json` — your project's ID card. It includes:
- Name, version, description
- Dependencies (what libraries you installed)
- Scripts (custom commands)

**Step 3:** Install Express:

```bash
npm install express
```

Express is a framework that makes building servers much, much easier. Think of it like pre-built rooms for your restaurant — you don't have to build the kitchen from scratch.

**Step 4:** Create `server.js`:

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

// When someone visits http://localhost:3000/
app.get('/', (req, res) => {
  res.send('Hello, World! This is my first server!');
});

// When someone visits http://localhost:3000/about
app.get('/about', (req, res) => {
  res.send('This is a simple web server built with Express.');
});

// Start the server
app.listen(PORT, () => {
  console.log(`Server is running at http://localhost:${PORT}`);
});
```

**Step 5:** Run it:

```bash
node server.js
```

Open `http://localhost:3000` in your browser. You should see "Hello, World!".

**Congratulations — you just built a web server from scratch!**

### 7.4 Express Routing — Different URLs, Different Responses

```javascript
const express = require('express');
const app = express();

// ── GET routes ──

// Homepage
app.get('/', (req, res) => {
  res.send('Welcome to my site!');
});

// Static page
app.get('/contact', (req, res) => {
  res.send('Contact us at hello@example.com');
});

// Dynamic routes (the :id part is a variable)
app.get('/users/:id', (req, res) => {
  const userId = req.params.id;
  res.send(`You requested user ${userId}`);
});

// Multiple parameters
app.get('/posts/:year/:month/:slug', (req, res) => {
  const { year, month, slug } = req.params;
  res.send(`Post from ${year}/${month}: ${slug}`);
});

// Query parameters (URL: /search?q=javascript&page=2)
app.get('/search', (req, res) => {
  const query = req.query.q;
  const page = req.query.page || 1;
  res.send(`Searching for "${query}" on page ${page}`);
});

// ── POST routes (receiving data) ──

// IMPORTANT: Tell Express to understand JSON
app.use(express.json());

app.post('/users', (req, res) => {
  const { name, email } = req.body;
  console.log('Received:', name, email);
  res.status(201).json({ message: 'User created!', name, email });
});

// ── Response Methods ──

res.send('Plain text');
res.json({ name: 'Alice' });      // JSON response (most common for APIs)
res.status(404).send('Not found'); // Custom status code
res.redirect('/new-location');      // Redirect to another URL
res.sendFile('/path/to/file.html'); // Send a file
res.render('template', data);       // Render a template (with view engine)
```

### 7.5 The Request-Response Cycle in Detail

Every time a client (browser, app, another server) talks to your server, this happens:

```
REQUEST
───────────────────────────────────────
Method:    GET / POST / PUT / DELETE
URL:       /users/123
Headers:   Content-Type, Authorization, etc.
Body:      (data, for POST/PUT)
Params:    /users/:id → id = 123
Query:     ?sort=asc&page=2

                │
                ▼

            YOUR SERVER
         (Express route handler)

                │
                ▼

RESPONSE
───────────────────────────────────────
Status:    200 / 404 / 500 (etc.)
Headers:   Content-Type, etc.
Body:      JSON / HTML / File
```

### 7.6 Middleware — Things That Run Between Request and Response

Middleware is like a conveyor belt. Each piece processes the request before passing it to the next:

```
Request → [Logger] → [Authenticator] → [Route Handler] → Response
              │              │                │
         "Logged request"  "User is valid"  "Process data"
```

```javascript
const express = require('express');
const app = express();

// Middleware that runs for EVERY request
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url} - ${new Date().toISOString()}`);
  next(); // Pass to the next middleware or route
});

// Body parser middleware (needed for POST/PUT)
app.use(express.json());

// Server static files from a "public" folder
app.use(express.static('public'));

// Middleware that runs only for /api routes
app.use('/api', (req, res, next) => {
  const apiKey = req.headers['x-api-key'];
  if (!apiKey) {
    return res.status(401).json({ error: 'API key required' });
  }
  next();
});

// Route-specific middleware
function requireAdmin(req, res, next) {
  if (req.headers['role'] !== 'admin') {
    return res.status(403).json({ error: 'Admins only' });
  }
  next();
}

app.delete('/users/:id', requireAdmin, (req, res) => {
  // Only runs if requireAdmin calls next()
  res.json({ message: 'User deleted' });
});
```

### 7.7 Environment Variables — Keeping Secrets Safe

Imagine you're a spy. Your mission, should you choose to accept it: build an app that connects to a secret database. Somewhere in your code, there's a password.

**If you write that password in your code, and push to GitHub, the whole world sees it.** Hackers scrape GitHub for passwords 24/7. They find them in minutes.

So you do what spies do: keep secrets OUT of the code.

#### The Problem

```javascript
// ❌ NEVER DO THIS
const DB_PASSWORD = "sup3r-s3cr3t-p@ssword";
```

This is bad because:
- You WILL accidentally commit it to GitHub (everyone does at least once)
- Anyone who sees your screen at a coffee shop has your password
- Your code is now a liability, not a product

#### The Solution: Environment Variables

Environment variables are values stored OUTSIDE your code, in the operating system or a special file. Your code reads them at runtime but never contains them.

**Think of it like a locker at the gym.** Your code has a key, but the actual valuables (passwords, API keys) are locked away. Even if someone steals your gym bag (your code), they don't get the locker contents.

#### How to Use .env Files

```bash
# Install dotenv — reads .env files into your app
npm install dotenv
```

Create a `.env` file in your project root:

```
# .env — THIS FILE NEVER GOES TO GITHUB
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/myapp
SECRET_KEY=my-super-secret-key-that-no-one-knows
API_KEY=abc123def456
```

Then in your code:

```javascript
// server.js — at the VERY TOP (before ANY other code)
require('dotenv').config();

const PORT = process.env.PORT || 3000;
const SECRET = process.env.SECRET_KEY;
const DB_URL = process.env.DATABASE_URL;

console.log(`Running on port ${PORT}`);
```

**Rules of .env files:**
- No quotes around values (they become part of the string)
- No spaces around `=` (they become part of the name)
- No trailing commas or semicolons
- Lines starting with `#` are comments

#### The Golden Rule: .env Goes in .gitignore

```gitignore
# .gitignore
.env
node_modules/
```

**If `.env` is NOT in `.gitignore`, one careless `git add .` leaks all your secrets forever.**

#### The Template Trick: .env.example

Commit a TEMPLATE to GitHub instead:

```
# .env.example — safe to share, no real secrets
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/myapp
SECRET_KEY=change-this-to-a-random-string
API_KEY=get-your-own-api-key-from-the-dashboard
```

New developers clone your project and run:
```bash
cp .env.example .env
# Then edit .env with their own values
```

#### Frontend vs Backend — Different Rules

**Backend (Node.js):** Env vars are natural. `process.env.PORT` works everywhere.

**Frontend (React, Vite, Next.js):** The browser can't access `process.env` directly. Why? If it could, any website could read your environment variables. That'd be a security nightmare.

Each framework has its own convention:

```bash
# Vite — env vars must start with VITE_
VITE_API_URL=https://api.example.com
VITE_STRIPE_KEY=pk_test_abc123
```

```javascript
// In your React/Vue code:
const apiUrl = import.meta.env.VITE_API_URL;
```

```bash
# Next.js — env vars must start with NEXT_PUBLIC_
NEXT_PUBLIC_API_URL=https://api.example.com
```

```javascript
// In your Next.js code:
const apiUrl = process.env.NEXT_PUBLIC_API_URL;
```

**Important:** Any env var prefixed for the frontend is BUNDLED into your JavaScript. Users can see it if they open DevTools. Never put real secrets in frontend env vars — only things like API URLs or public Stripe keys.

#### Different Environments, Different .env Files

```bash
.env              # Used everywhere (committed as example only)
.env.local        # Local overrides (never committed)
.env.development  # Dev server
.env.production   # Production server
```

Environment-specific files override `.env`. This lets you have `DATABASE_URL=localhost` in development and `DATABASE_URL=supabase-production-url` in production.

#### How Hosting Platforms Handle Env Vars

**Vercel, Render, Netlify, Railway** — you don't upload `.env`. Instead:

1. Go to your project dashboard
2. Find "Environment Variables" in settings
3. Type each one in a web form
4. The platform injects them at runtime

```bash
# On Render's dashboard, you'd set:
NODE_ENV=production
DATABASE_URL=postgresql://prod-url...
SECRET_KEY=actually-secret-now
```

No `.env` file needed in production. The platform handles it.

#### Common Mistakes

| Mistake | Why It's Bad | Fix |
|---|---|---|
| Spaces around `=` | `PORT = 3000` creates env var named ` PORT ` (with spaces) | `PORT=3000` (no spaces) |
| Committing .env | Everyone sees your passwords forever | Add to .gitignore NOW |
| Not restarting the server | `process.env` is read at startup | Kill and restart after changing .env |
| Using env vars in frontend without prefix | Vite/Next won't expose them | Add `VITE_` or `NEXT_PUBLIC_` prefix |
| Putting real secrets in frontend env | Anyone can read them in DevTools | Only use public keys in frontend |

#### Your Turn

1. Add `dotenv` to your project and create a `.env` with `PORT=4000`
2. Change your server to use `process.env.PORT`
3. Create `.env.example` with a fake secret
4. Add `.env` to `.gitignore`
5. Run the server — it should use port 4000
6. Change the port in `.env` and restart — it should change

### 7.8 Serving Static Files

Right now, your frontend (HTML/CSS/JS) is separate from your backend. In production, you'll often serve them from the same place:

```javascript
const express = require('express');
const path = require('path');
const app = express();

// Serve everything in the "public" folder as static files
app.use(express.static('public'));

// Now visiting http://localhost:3000/index.html
// will serve public/index.html

// Or serve a specific folder
app.use(express.static(path.join(__dirname, '../frontend')));

// The catch-all: for any route not matched, serve index.html
// (important for single-page apps with client-side routing)
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, '../frontend/index.html'));
});
```

---

## 8. Databases — Remembering Things

So far, all our data disappears when the server restarts. We need a place to store things permanently. That's a database.

### 8.1 SQL vs NoSQL — The Great Debate

```
SQL Databases                    NoSQL Databases
────────────────────────────────────────────────
Tables with rows/columns         Collections of documents
Like Excel spreadsheets          Like a folder of JSON files
Schema is fixed                  Schema is flexible
Data is strongly related         Data is less relational

Examples:                        Examples:
  PostgreSQL                       MongoDB
  MySQL                            Firebase Firestore
  SQLite                           CouchDB
```

**For beginners: start with SQL.** Why?
1. It's structured and predictable
2. The skills transfer to any SQL database
3. Most real-world apps use SQL
4. It forces you to think about your data structure

### 8.2 SQL — Structured Query Language

SQL is the language you use to talk to relational databases.

#### Creating a Table

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  email TEXT NOT NULL UNIQUE,
  age INTEGER,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

This says: "Create a table called `users` with these columns, and enforce these rules."

| Column | Type | Rules |
|---|---|---|
| `id` | Integer | Primary key (unique identifier), auto-increments |
| `name` | Text | NOT NULL (required) |
| `email` | Text | NOT NULL (required), UNIQUE (no duplicates) |
| `age` | Integer | Optional (no NOT NULL) |
| `created_at` | DateTime | Defaults to current timestamp if not provided |

#### CRUD Operations

```sql
─── CREATE (INSERT) ───

INSERT INTO users (name, email, age)
VALUES ('Alice', 'alice@example.com', 25);

─── READ (SELECT) ───

-- All users, all columns
SELECT * FROM users;

-- Specific columns
SELECT name, email FROM users;

-- With conditions
SELECT * FROM users WHERE age >= 18;

-- With ordering
SELECT * FROM users ORDER BY name ASC;
SELECT * FROM users ORDER BY created_at DESC;

-- With limits
SELECT * FROM users LIMIT 10;

-- Search
SELECT * FROM users WHERE name LIKE '%ali%';

-- Count
SELECT COUNT(*) FROM users;
SELECT COUNT(*) FROM users WHERE age > 20;

─── UPDATE ───

UPDATE users SET age = 26 WHERE id = 1;

─── DELETE ───

DELETE FROM users WHERE id = 1;
DELETE FROM users;  -- ❌ Be careful! This deletes ALL users
```

#### Relationships — The Power of SQL

The real power of SQL is connecting data across tables:

```sql
CREATE TABLE posts (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  title TEXT NOT NULL,
  content TEXT,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Get all posts with the author's name
SELECT posts.title, posts.content, users.name
FROM posts
JOIN users ON posts.user_id = users.id;

-- Get users with their post count
SELECT users.name, COUNT(posts.id) as post_count
FROM users
LEFT JOIN posts ON users.id = posts.user_id
GROUP BY users.id;
```

### 8.3 Connecting Express to SQLite

SQLite is perfect for learning — no server setup, just a file on your computer.

```bash
npm install better-sqlite3
```

```javascript
// database.js
const Database = require('better-sqlite3');
const path = require('path');

// Create/open a database file
const db = new Database(path.join(__dirname, 'app.db'));

// Enable WAL mode (better performance)
db.pragma('journal_mode = WAL');

// Create tables
db.exec(`
  CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT NOT NULL UNIQUE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
  )
`);

module.exports = db;
```

```javascript
// server.js
const express = require('express');
const db = require('./database');

const app = express();
app.use(express.json());

// GET all users
app.get('/users', (req, res) => {
  const users = db.prepare('SELECT * FROM users ORDER BY name').all();
  res.json(users);
});

// GET one user
app.get('/users/:id', (req, res) => {
  const user = db.prepare('SELECT * FROM users WHERE id = ?').get(req.params.id);
  if (!user) return res.status(404).json({ error: 'User not found' });
  res.json(user);
});

// POST create user
app.post('/users', (req, res) => {
  const { name, email } = req.body;
  
  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email are required' });
  }

  try {
    const result = db.prepare(
      'INSERT INTO users (name, email) VALUES (?, ?)'
    ).run(name, email);
    
    const newUser = db.prepare('SELECT * FROM users WHERE id = ?').get(result.lastInsertRowid);
    res.status(201).json(newUser);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});

// PUT update user
app.put('/users/:id', (req, res) => {
  const { name, email } = req.body;
  const existing = db.prepare('SELECT * FROM users WHERE id = ?').get(req.params.id);
  
  if (!existing) return res.status(404).json({ error: 'User not found' });

  db.prepare('UPDATE users SET name = ?, email = ? WHERE id = ?')
    .run(name || existing.name, email || existing.email, req.params.id);
  
  const updated = db.prepare('SELECT * FROM users WHERE id = ?').get(req.params.id);
  res.json(updated);
});

// DELETE user
app.delete('/users/:id', (req, res) => {
  const result = db.prepare('DELETE FROM users WHERE id = ?').run(req.params.id);
  
  if (result.changes === 0) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  res.status(204).send();
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

**Key SQLite methods:**
- `.run()` — for INSERT, UPDATE, DELETE (returns `{ changes, lastInsertRowid }`)
- `.get()` — for single row (returns object or undefined)
- `.all()` — for multiple rows (returns array)
- The `?` placeholders — ALWAYS use these instead of string concatenation to prevent SQL injection

### Your Turn — Mini Challenge

1. Start the server above
2. Use Postman (or `curl`) to create 3 users via POST
3. Get all users via GET
4. Update one user via PUT
5. Delete one user via DELETE
6. Verify the changes by getting all users again

---

## 9. Building Your First Full Stack App

Now we'll build a complete Notes App — frontend AND backend AND database. By the end, you'll have a working app that you can deploy and share.

### Project Structure

```
notes-app/
├── backend/
│   ├── server.js
│   ├── database.js
│   ├── package.json
│   └── .env
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── app.js
└── README.md
```

### 9.1 Setup

```bash
mkdir notes-app
cd notes-app
mkdir backend frontend
cd backend
npm init -y
npm install express better-sqlite3 cors dotenv
```

### 9.2 Backend — The API

#### `backend/database.js`

```javascript
const Database = require('better-sqlite3');
const path = require('path');

const db = new Database(path.join(__dirname, 'notes.db'));
db.pragma('journal_mode = WAL');

db.exec(`
  CREATE TABLE IF NOT EXISTS notes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    content TEXT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
  )
`);

module.exports = db;
```

#### `backend/server.js`

```javascript
require('dotenv').config();
const express = require('express');
const cors = require('cors');
const path = require('path');
const db = require('./database');

const app = express();
const PORT = process.env.PORT || 3001;

// Middleware
app.use(cors());
app.use(express.json());

// Serve frontend in production
if (process.env.NODE_ENV === 'production') {
  app.use(express.static(path.join(__dirname, '../frontend')));
}

// ─── API ROUTES ───

// GET /api/notes — Get all notes
app.get('/api/notes', (req, res) => {
  try {
    const notes = db.prepare('SELECT * FROM notes ORDER BY updated_at DESC').all();
    res.json(notes);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// GET /api/notes/:id — Get one note
app.get('/api/notes/:id', (req, res) => {
  try {
    const note = db.prepare('SELECT * FROM notes WHERE id = ?').get(req.params.id);
    if (!note) return res.status(404).json({ error: 'Note not found' });
    res.json(note);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// POST /api/notes — Create a note
app.post('/api/notes', (req, res) => {
  try {
    const { title, content } = req.body;
    if (!title || !content) {
      return res.status(400).json({ error: 'Title and content are required' });
    }

    const result = db.prepare(
      'INSERT INTO notes (title, content) VALUES (?, ?)'
    ).run(title, content);

    const note = db.prepare('SELECT * FROM notes WHERE id = ?').get(result.lastInsertRowid);
    res.status(201).json(note);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// PUT /api/notes/:id — Update a note
app.put('/api/notes/:id', (req, res) => {
  try {
    const { title, content } = req.body;
    const existing = db.prepare('SELECT * FROM notes WHERE id = ?').get(req.params.id);
    if (!existing) return res.status(404).json({ error: 'Note not found' });

    db.prepare(
      'UPDATE notes SET title = ?, content = ?, updated_at = CURRENT_TIMESTAMP WHERE id = ?'
    ).run(title, content, req.params.id);

    const note = db.prepare('SELECT * FROM notes WHERE id = ?').get(req.params.id);
    res.json(note);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// DELETE /api/notes/:id — Delete a note
app.delete('/api/notes/:id', (req, res) => {
  try {
    const result = db.prepare('DELETE FROM notes WHERE id = ?').run(req.params.id);
    if (result.changes === 0) {
      return res.status(404).json({ error: 'Note not found' });
    }
    res.status(204).send();
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Start server
app.listen(PORT, () => {
  console.log(`Notes API running at http://localhost:${PORT}`);
  console.log(`Environment: ${process.env.NODE_ENV || 'development'}`);
});
```

### 9.3 Frontend — The User Interface

#### `frontend/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Notes App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <header>
      <h1>📝 Notes</h1>
      <p>Write down your thoughts. They'll be here when you come back.</p>
    </header>

    <form id="note-form" class="note-form">
      <input
        type="text"
        id="note-title"
        placeholder="Note title..."
        required
        maxlength="100"
      >
      <textarea
        id="note-content"
        placeholder="Write your note here..."
        required
        rows="4"
      ></textarea>
      <div class="form-actions">
        <button type="submit" id="submit-btn">Add Note</button>
        <button type="button" id="cancel-btn" class="btn-secondary hidden">Cancel</button>
      </div>
    </form>

    <div id="notes-list" class="notes-list"></div>
  </div>

  <script src="app.js"></script>
</body>
</html>
```

#### `frontend/style.css`

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  padding: 20px;
}

.container {
  max-width: 700px;
  margin: 0 auto;
}

header {
  color: white;
  text-align: center;
  margin-bottom: 30px;
}

header h1 {
  font-size: 2.5rem;
  margin-bottom: 8px;
}

header p {
  opacity: 0.9;
  font-size: 1.1rem;
}

.note-form {
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  margin-bottom: 30px;
}

.note-form input,
.note-form textarea {
  width: 100%;
  padding: 12px;
  margin-bottom: 12px;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  font-size: 16px;
  font-family: inherit;
  transition: border-color 0.2s;
}

.note-form input:focus,
.note-form textarea:focus {
  outline: none;
  border-color: #667eea;
}

.note-form textarea {
  resize: vertical;
  min-height: 100px;
}

.form-actions {
  display: flex;
  gap: 10px;
}

button {
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

button:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

button:active {
  transform: translateY(0);
}

#submit-btn {
  background: #667eea;
  color: white;
  flex: 1;
}

#cancel-btn {
  background: #e2e8f0;
  color: #4a5568;
}

.hidden {
  display: none;
}

.notes-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.note-card {
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.2s;
  animation: slideIn 0.3s ease;
}

.note-card:hover {
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
}

.note-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 8px;
}

.note-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: #2d3748;
  flex: 1;
  margin-right: 12px;
}

.note-content {
  color: #4a5568;
  line-height: 1.6;
  margin-bottom: 12px;
  white-space: pre-wrap;
  word-wrap: break-word;
}

.note-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 12px;
  border-top: 1px solid #e2e8f0;
}

.note-date {
  font-size: 0.85rem;
  color: #a0aec0;
}

.note-actions {
  display: flex;
  gap: 8px;
}

.btn-edit {
  background: #38a169;
  color: white;
  padding: 6px 14px;
  font-size: 14px;
}

.btn-delete {
  background: #fc8181;
  color: white;
  padding: 6px 14px;
  font-size: 14px;
}

.empty-state {
  text-align: center;
  color: white;
  padding: 40px 20px;
}

.empty-state p {
  font-size: 1.2rem;
  opacity: 0.9;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 600px) {
  header h1 {
    font-size: 1.8rem;
  }

  .note-form {
    padding: 15px;
  }

  .note-card {
    padding: 15px;
  }
}
```

#### `frontend/app.js`

```javascript
// ─── Configuration ───
const API_URL = 'http://localhost:3001/api/notes';

// ─── DOM References ───
const form = document.getElementById('note-form');
const titleInput = document.getElementById('note-title');
const contentInput = document.getElementById('note-content');
const submitBtn = document.getElementById('submit-btn');
const cancelBtn = document.getElementById('cancel-btn');
const notesList = document.getElementById('notes-list');

// ─── State ───
let editingId = null;

// ─── Initialize ───
document.addEventListener('DOMContentLoaded', fetchNotes);

// ─── Event Listeners ───

// Form submit
form.addEventListener('submit', async (e) => {
  e.preventDefault();
  const title = titleInput.value.trim();
  const content = contentInput.value.trim();

  if (!title || !content) return;

  try {
    if (editingId) {
      await updateNote(editingId, title, content);
    } else {
      await createNote(title, content);
    }
    resetForm();
  } catch (err) {
    alert('Failed to save note. Check your connection.');
  }
});

// Cancel button
cancelBtn.addEventListener('click', resetForm);

// ─── API Functions ───

async function fetchNotes() {
  try {
    const res = await fetch(API_URL);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    const notes = await res.json();
    renderNotes(notes);
  } catch (err) {
    notesList.innerHTML = `
      <div class="empty-state">
        <p>❌ Failed to load notes. Is the server running?</p>
        <p style="font-size:0.9rem;margin-top:8px;">Make sure you've started the backend with <code>node server.js</code></p>
      </div>`;
  }
}

async function createNote(title, content) {
  const res = await fetch(API_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ title, content }),
  });
  if (!res.ok) throw new Error('Create failed');
  await fetchNotes();
}

async function updateNote(id, title, content) {
  const res = await fetch(`${API_URL}/${id}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ title, content }),
  });
  if (!res.ok) throw new Error('Update failed');
  await fetchNotes();
}

async function deleteNote(id) {
  if (!confirm('Delete this note forever?')) return;

  try {
    const res = await fetch(`${API_URL}/${id}`, { method: 'DELETE' });
    if (!res.ok) throw new Error('Delete failed');
    await fetchNotes();
  } catch (err) {
    alert('Failed to delete note.');
  }
}

// ─── Edit Mode ───

function editNote(id, title, content) {
  editingId = id;
  titleInput.value = title;
  contentInput.value = content;
  submitBtn.textContent = 'Update Note';
  cancelBtn.classList.remove('hidden');
  titleInput.focus();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function resetForm() {
  form.reset();
  editingId = null;
  submitBtn.textContent = 'Add Note';
  cancelBtn.classList.add('hidden');
}

// ─── Render ───

function renderNotes(notes) {
  if (notes.length === 0) {
    notesList.innerHTML = `
      <div class="empty-state">
        <p style="font-size:2rem;margin-bottom:10px;">📝</p>
        <p>No notes yet. Write your first one above!</p>
      </div>`;
    return;
  }

  notesList.innerHTML = notes.map(note => `
    <div class="note-card">
      <div class="note-header">
        <div class="note-title">${escapeHtml(note.title)}</div>
      </div>
      <div class="note-content">${escapeHtml(note.content)}</div>
      <div class="note-meta">
        <span class="note-date">
          ${new Date(note.updated_at).toLocaleDateString('en-US', {
            year: 'numeric', month: 'short', day: 'numeric',
            hour: '2-digit', minute: '2-digit'
          })}
        </span>
        <div class="note-actions">
          <button class="btn-edit" onclick="editNote(${note.id}, '${escapeHtml(note.title).replace(/'/g, "\\'")}', '${escapeHtml(note.content).replace(/'/g, "\\'")}')">
            Edit
          </button>
          <button class="btn-delete" onclick="deleteNote(${note.id})">
            Delete
          </button>
        </div>
      </div>
    </div>
  `).join('');
}

// ─── Helper: XSS Protection ───

function escapeHtml(text) {
  const div = document.createElement('div');
  div.textContent = text;
  return div.innerHTML;
}
```

### 9.4 Running the Full Stack App

**Terminal 1 — Backend:**
```bash
cd notes-app/backend
node server.js
```

**Terminal 2 — Frontend:**
If you're using Live Server for the frontend (recommended for development):
- Open `notes-app/frontend/index.html`
- Right-click → Open with Live Server

Or, serve frontend through Express (change `API_URL` to relative path `/api/notes` and run only the backend).

### Your Turn

1. Create a note
2. Create another note
3. Edit the first note
4. Delete the second note
5. Refresh the page — your notes are still there (database!)

---

## 10. APIs — How Frontend and Backend Talk

### 10.1 What is an API?

API = **Application Programming Interface**.

An API is a waiter:
- You (the frontend) tell the waiter what you want
- The waiter goes to the kitchen (the server)
- The kitchen does the work (queries the database)
- The waiter brings back your food (the response)

```
Frontend (Browser)          API (Waiter)            Backend (Kitchen)
      │                         │                        │
      │  "I want users"         │                        │
      │ ─── GET /api/users ──>  │                        │
      │                         │  "Fetch all users"     │
      │                         │ ────────────────────>  │
      │                         │                        │
      │                         │  "Here's the data"     │
      │                         │ <────────────────────  │
      │  <─── JSON response ──── │                        │
```

### 10.2 REST — The Most Common API Style

REST = **Representational State Transfer**

A REST API uses:
- **Resources** (nouns): `/users`, `/notes`, `/products`
- **HTTP Methods** (verbs): GET, POST, PUT, DELETE
- **Status Codes**: 200, 201, 404, 500

```
REST API Structure:
───────────────────

GET    /api/users          → List all users
GET    /api/users/123      → Get user 123
POST   /api/users          → Create a new user
PUT    /api/users/123      → Update user 123
DELETE /api/users/123      → Delete user 123

GET    /api/users/123/notes     → Get notes for user 123
POST   /api/users/123/notes     → Create a note for user 123
```

### 10.3 Calling APIs from Frontend

```javascript
// GET — Read data
async function getUsers() {
  const res = await fetch('/api/users');
  const users = await res.json();
  return users;
}

// POST — Create data (send data in body)
async function createUser(name, email) {
  const res = await fetch('/api/users', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name, email }),
  });
  return res.json();
}

// PUT — Update data
async function updateUser(id, data) {
  const res = await fetch(`/api/users/${id}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data),
  });
  return res.json();
}

// DELETE — Delete data
async function deleteUser(id) {
  const res = await fetch(`/api/users/${id}`, {
    method: 'DELETE',
  });
  if (res.status === 204) return true; // Deleted successfully
  throw new Error('Delete failed');
}
```

### 10.4 The Fetch API — Your Gateway to the Internet

```javascript
// ─── GET with Headers ───
async function getData() {
  const res = await fetch('/api/protected-data', {
    headers: {
      'Authorization': `Bearer ${token}`,
      'X-API-Key': 'abc123',
    },
  });

  if (!res.ok) {
    const error = await res.json();
    throw new Error(error.message);
  }

  return res.json();
}

// ─── POST with Different Content Types ───

// JSON (most common)
fetch('/api/data', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ key: 'value' }),
});

// Form data (for file uploads)
const formData = new FormData();
formData.append('name', 'Alice');
formData.append('avatar', fileInput.files[0]);

fetch('/api/upload', {
  method: 'POST',
  body: formData, // No Content-Type header — browser sets it automatically
});

// ─── URL Search Params (for GET queries) ───
const params = new URLSearchParams({
  search: 'javascript',
  page: 2,
  limit: 20,
});

fetch(`/api/search?${params}`);
// Result: /api/search?search=javascript&page=2&limit=20
```

### 10.5 CORS — The Browser's Security Guard

**The problem:** Your frontend runs on `http://localhost:5500` (Live Server). Your backend runs on `http://localhost:3001`. The browser says:

> "Whoa there. These are two different places. I'm not sure it's safe to let them talk."

**CORS (Cross-Origin Resource Sharing)** is the browser's security mechanism. It blocks requests from one origin to another unless the server explicitly allows it.

**Fix on the server (Express):**

```bash
npm install cors
```

```javascript
const cors = require('cors');

// Allow ALL origins (fine for development, not for production)
app.use(cors());

// Allow specific origins only (production)
app.use(cors({
  origin: 'https://my-frontend-domain.com',
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization'],
}));
```

**Better solution for production:** Serve your frontend and backend from the same domain. Then CORS isn't needed at all.

---

## 11. Deploying — Showing Your Work to the World

### 11.1 Deploying the Frontend (Static Sites)

These platforms host HTML/CSS/JS for free. Push to GitHub and they auto-deploy.

#### Vercel (Recommended for beginners)

1. Push your code to GitHub
2. Go to [vercel.com](https://vercel.com) and sign up with GitHub
3. Click **Add New → Project**
4. Find your repo and click **Import**
5. Leave settings default → **Deploy**
6. Done. Your site is at `https://project-name.vercel.app`

#### Netlify

1. Push to GitHub
2. Go to [netlify.com](https://netlify.com)
3. Click **Add new site → Import an existing project**
4. Connect your GitHub repo
5. Deploy settings: Branch `main`, Build command: none, Publish directory: `frontend`
6. **Deploy**

### 11.2 Deploying the Backend (Server)

These platforms run your Node.js server in the cloud.

#### Render (Free tier available)

1. Create `backend/Procfile` (no extension):
```
web: node server.js
```

2. Update `backend/server.js` — use `process.env.PORT`:
```javascript
const PORT = process.env.PORT || 3001;
```

3. Push to GitHub

4. Go to [render.com](https://render.com)
5. **New Web Service**
6. Connect your GitHub repo
7. Settings:
   - Name: `notes-app-api`
   - Root Directory: `backend`
   - Build Command: `npm install`
   - Start Command: `node server.js`
   - Plan: Free
8. **Deploy**

#### Railway (Easiest)

1. Push to GitHub
2. Go to [railway.app](https://railway.app)
3. **New Project → Deploy from GitHub**
4. Select your repo
5. Done. Railway auto-detects Node.js

### 11.3 Connecting Deployed Frontend to Deployed Backend

Once both are live, update the `API_URL` in your frontend:

```javascript
const API_URL = 'https://notes-app-api.onrender.com/api/notes';
```

**For production**, configure it via environment variable:

```html
<script>
  const API_URL = window.API_URL || 'http://localhost:3001/api/notes';
</script>
```

Or better: serve frontend from the same domain as the backend (using `express.static`), so you can use relative URLs like `/api/notes`.

### 11.4 Custom Domains

**Option 1: Free subdomain**
- Vercel: `your-app.vercel.app`
- Render: `your-app.onrender.com`

**Option 2: Custom domain (buy one)**
- Buy a domain from Namecheap/Cloudflare/Google Domains ($8-15/year)
- In Vercel: Project → Settings → Domains → Add
- Point your domain's DNS to Vercel's nameservers

### 11.5 Deployment Troubleshooting

Things WILL go wrong when you deploy. Here's how to fix the most common issues.

#### Frontend (Vercel) Problems

**"Page loads blank / white screen"**
- Open DevTools → Console. See any errors?
- Most common: your JavaScript is looking for files at the wrong path. Check that your script `<script src="...">` uses relative paths (`./js/app.js`) not absolute (`/js/app.js` if your site isn't at the root)
- **Next.js fix:** Make sure your `build` command runs without errors. Check the Vercel build logs.

**"404 on page refresh"** (client-side routing)
- Vercel automatically handles this if you use Next.js. For vanilla JS SPAs, add a `vercel.json` in your project root:
```json
{
  "rewrites": [{"source": "/(.*)", "destination": "/index.html"}]
}
```

**"My API calls don't work"**
- Check the browser's Network tab. What URL is it calling?
- Is it `http://localhost:...`? That's your local server, not your deployed backend. Update the URL to your deployed backend URL.
- **CORS error** (`No 'Access-Control-Allow-Origin' header`)? Your backend isn't configured to accept requests from your frontend domain. Add `cors()` middleware on the backend and configure allowed origins.

**"Changes aren't showing up"**
- Hard refresh (`Ctrl+Shift+R` / `Cmd+Shift+R`) to bypass cache.
- In Vercel: check the Deployments tab → is the latest build successful? If not, check the build logs.

#### Backend (Render) Problems

**"Internal Server Error (500)"**
- Check your Render logs (Dashboard → your service → Logs).
- Common cause: environment variables not set. Did you set your `PORT`, `DATABASE_URL`, or API keys in Render's Environment section?
- File system errors: Render uses ephemeral storage. Files written to disk (like SQLite `.db` files) are DELETED every time your server restarts. Use a hosted database (Supabase, MongoDB Atlas) instead.

**"Server crashes on deploy"**
- Your `start` script in `package.json` is wrong. It should be something like `node server.js` or `node backend/server.js`.
- Missing dependencies: Did you run `npm install`? Check package-lock.json is committed to git.

**"Database file not found / write errors"**
- With SQLite on Render: SQLite files are deleted on every restart. **You need a cloud database** (Supabase, Neon, Railway PostgreSQL). Add a chapter about this after you've practiced with SQLite locally.

#### General Debugging Workflow

1. **Check the logs** — Vercel: Build logs + Function logs. Render: Service logs.
2. **Check environment variables** — Are all the secrets (`API_KEY`, `DATABASE_URL`) set in the deployment dashboard?
3. **Check the URL** — Are frontend and backend URLs correct? Don't use `localhost` in production.
4. **Check the browser console** — Network tab shows all requests. Console tab shows errors.
5. **Reproduce locally** — Can you make it work on your computer? If yes, the issue is deployment-specific.

**The golden rule:** Break the problem in half. Is it a frontend issue? Backend issue? Database issue? Network issue? Isolate one at a time.

---

## 12. Git & GitHub — Time Travel for Your Code

### 12.1 Why Git?

Imagine writing a 10-page essay without an Undo button. One wrong delete and hours of work are gone.

Git is **infinite Undo** for your code. You can:
- Go back to any previous version
- Try experimental features without risk
- Collaborate without overwriting each other's work

### 12.2 Git Basics

```bash
# Configure Git (do this once)
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Start tracking a project
cd my-project
git init

# Check status
git status

# Stage files (prepare to save)
git add index.html          # Stage one file
git add .                   # Stage all changed files

# Commit (save a snapshot)
git commit -m "Add homepage with navigation"

# See history
git log                     # Full log
git log --oneline           # Compact log
git log --graph             # With branch visualization
```

### 12.3 GitHub — Git in the Cloud

GitHub is where your code lives online. It's like Google Drive for Git repos.

```bash
# Create a repo on GitHub first (no README, no .gitignore)

# Connect your local repo
git remote add origin https://github.com/your-username/notes-app.git

# Push your code
git branch -M main
git push -u origin main

# Later, push new changes
git add .
git commit -m "Add delete functionality"
git push
```

### 12.4 Branches — Parallel Universes

Branches let you work on features without affecting the main code:

```
main:     ●──●────────────────────●──────────
               \                  /
feature-login   ●──●──●──●──●──●──
```

```bash
# Create and switch to a new branch
git switch -c add-login-page

# Make changes and commit
git add .
git commit -m "Add login form"

# Switch back to main
git switch main

# Merge your feature
git merge add-login-page

# Delete the branch (after merging)
git branch -d add-login-page
```

### 12.5 The Developer's Daily Workflow

```bash
# 1. Start your day: get latest code
git switch main
git pull

# 2. Create a branch for your task
git switch -c fix-login-bug

# 3. Work, work, work...
# 4. Save your progress
git add .
git commit -m "Fix login button not working on mobile"

# 5. Push to GitHub
git push -u origin fix-login-bug

# 6. On GitHub: create a Pull Request
# 7. After review: merge to main
# 8. Delete the branch
```

### 12.6 The `.gitignore` — Don't Commit These

```gitignore
# Dependencies
node_modules/

# Environment variables
.env

# Database files
*.db
*.sqlite

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Build output
dist/
build/

# Logs
*.log
```

---

## 13. Your Learning Roadmap

### Month 1: Foundation

```
Week 1: HTML
  ├── Learn all common tags
  ├── Build a personal profile page
  └── Build a recipe page

Week 2: CSS
  ├── Box model, colors, fonts
  ├── Flexbox (practice for 2 days straight)
  ├── Responsive design with media queries
  └── Style your profile and recipe pages

Week 3: JavaScript Basics
  ├── Variables, data types, operators
  ├── Conditionals and loops
  ├── Functions and arrays
  └── Build a calculator

Week 4: JavaScript DOM
  ├── Selecting and manipulating elements
  ├── Events (click, submit, input)
  ├── Build a to-do list
  └── Build a simple quiz app
```

### Month 2: Backend

```
Week 5: Node.js & Express
  ├── What is a server?
  ├── Routes and responses
  ├── Middleware
  └── Build a simple API (without database)

Week 6: Databases
  ├── SQL basics (SELECT, INSERT, UPDATE, DELETE)
  ├── SQLite with better-sqlite3
  └── Connect your API to a database

Week 7: Full Stack Project
  ├── Build the Notes App
  ├── Frontend + Backend + Database
  ├── Test everything
  └── Deploy it

Week 8: Git & Deployment
  ├── Git basics (add, commit, push, pull)
  ├── GitHub
  ├── Deploy to Vercel/Render
  └── Share your Notes App with someone
```

### Month 3: Level Up

```
Week 9: React Fundamentals
  ├── Components, props, state
  ├── JSX
  └── Build a React to-do list

Week 10: Authentication
  ├── How login works (JWT tokens)
  ├── Register, login, protected routes
  └── Add auth to your Notes App

Week 11: TypeScript
  ├── Types, interfaces
  ├── Why TypeScript saves you from bugs
  └── Convert your project to TypeScript

Week 12: Polish & Portfolio
  ├── Testing with Jest
  ├── Performance optimization
  ├── Build a portfolio site
  └── Apply for jobs / freelance
```

### Learning Resources

| Resource | Best for |
|---|---|
| [MDN Web Docs](https://developer.mozilla.org) | The official documentation (free, authoritative) |
| [freeCodeCamp](https://freecodecamp.org) | Interactive exercises (free) |
| [The Odin Project](https://theodinproject.com) | Full curriculum (free, project-based) |
| [JavaScript.info](https://javascript.info) | Deep JavaScript tutorials (free) |
| [Frontend Mentor](https://frontendmentor.io) | Practice with real designs (free) |
| [CSS Tricks](https://css-tricks.com) | CSS guides and tips (free) |

---

## 14. Intro to React

### What is React?

React is a **JavaScript library for building user interfaces**. Think of it as a smarter way to build the frontend:

| Vanilla JS | React |
|---|---|
| You manually update the DOM | React updates the DOM for you |
| You track all state yourself | React tracks state and re-renders when it changes |
| You re-create HTML with `innerHTML` | You write JSX (HTML-like syntax in JS) |
| Hard to manage complex UIs | Built for complex UIs |

**The core idea:** Your UI is a **function of your state**. When state changes, React automatically re-renders the parts that changed. You don't have to manually find the right `<div>` and update it.

### Components

Everything in React is a **component** — a reusable piece of UI. Think of them like custom HTML elements:

```jsx
// A component is just a function that returns JSX
function Greeting() {
  return <h1>Hello, World!</h1>;
}
```

JSX looks like HTML but isn't. It gets compiled into JavaScript `createElement` calls. You can mix JS inside `{}`:

```jsx
function Welcome({ name }) {
  const hour = new Date().getHours();
  const greeting = hour < 12 ? 'Good morning' : 'Good afternoon';
  return <h2>{greeting}, {name}!</h2>;
}
```

### Props — Passing Data to Components

Props (properties) are like function arguments for components:

```jsx
function Card({ title, children }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      <div className="card-content">{children}</div>
    </div>
  );
}

// Usage:
<Card title="My Project">
  <p>This is the card body.</p>
</Card>
```

**Key rule:** Props are read-only. A component should never modify its props.

### State — Data That Changes

State is data that can change over time. When state changes, the component re-renders:

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  // count: the current value
  // setCount: function to update it
  // useState(0): initial value is 0

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}
```

`useState` is a **hook** — a function that "hooks into" React's internals. Hooks always start with `use`.

**Why `useState` instead of a regular variable?** React needs to know when state changes so it can re-render. A regular variable change wouldn't trigger a re-render.

### The Virtual DOM — How React Is So Fast

When state changes, React:
1. **Creates a virtual DOM** (a lightweight JavaScript object representation of the real DOM)
2. **Compares** it to the previous virtual DOM (diffing)
3. **Calculates** the minimum changes needed (reconciliation)
4. **Applies** only those changes to the real DOM

This is why you don't need to manually update the DOM. React figures out exactly what changed.

### Effects — Running Code After Render

Use `useEffect` for side effects (fetching data, setting up timers, etc.):

```jsx
import { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => setUser(data));
  }, [userId]);
  // The [userId] means: re-run this effect only when userId changes

  if (!user) return <p>Loading...</p>;
  return <h1>{user.name}</h1>;
}
```

**Key `useEffect` rules:**
- Runs AFTER the component renders (doesn't block the UI)
- The dependency array `[ ]` controls when it re-runs:
  - `[ ]` — runs once on mount
  - `[userId]` — re-runs when `userId` changes
  - no array — runs on EVERY render (usually a bug)
- Return a cleanup function to prevent memory leaks

### Conditional Rendering

```jsx
function Status({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <Dashboard /> : <LoginButton />}
    </div>
  );
}
```

### Lists with `.map()`

```jsx
function ItemList({ items }) {
  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

**Always give list items a unique `key` prop** (use the item's ID, not the index).

### Creating a React App

The standard way:

```bash
npx create-react-app my-app
cd my-app
npm start
```

This creates a full project structure and a development server with hot reload.

**Newer alternative (Vite):**
```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```
Vite is faster than Create React App and is now the recommended approach.

### File Structure of a React App

```
my-app/
├── public/          # Static files
│   └── index.html   # The single HTML file
├── src/             # Your code
│   ├── App.jsx      # Main component
│   ├── index.jsx    # Entry point (renders App into DOM)
│   └── components/  # Your components
├── package.json
└── vite.config.js   # (if using Vite)
```

The `index.html` has a `<div id="root">`, and `index.jsx` renders your React app into it:

```jsx
import { createRoot } from 'react-dom/client';
import App from './App';

createRoot(document.getElementById('root')).render(<App />);
```

### Your First React Component Tree

```
App
├── Header (logo, nav links)
├── Main
│   ├── PostList
│   │   ├── Post (× many)
│   │   │   ├── PostTitle
│   │   │   ├── PostBody
│   │   │   └── CommentList
│   │   └── LoadMoreButton
│   └── Sidebar
│       ├── UserCard
│       └── TrendingTopics
└── Footer
```

Each component is its own function in its own file. This modularity is the main benefit of React.

### Key Differences from Vanilla JS

| Concept | Vanilla JS | React |
|---|---|---|
| Creating elements | `document.createElement('div')` | `<div>...</div>` (JSX) |
| Adding event listeners | `element.addEventListener(...)` | `onClick={handler}` |
| Updating text | `element.textContent = 'new'` | React does it when state changes |
| Styling | `.className` or `.style` | `className="..."` or `style={{}}` |
| Looping | `for` loop + `innerHTML` | `.map()` + JSX |
| Conditionals | `if` + DOM manipulation | ternary `?` in JSX |

### When to Use React

**Use React when:**
- Your UI has lots of interactive state (forms, modals, real-time updates)
- Multiple components need to share data
- You're building a complex single-page application (SPA)
- You want a component library for reuse

**Don't use React when:**
- You're building a mostly static site (use HTML/CSS or a static site generator)
- You just need a simple interactive page (vanilla JS is simpler)
- Your team doesn't know React (it adds complexity)

### Mini Project: Convert Your Portfolio to React

Take the portfolio from Project 1 and convert it to React components:
1. `App.jsx` — main layout
2. `Nav.jsx` — navigation
3. `Hero.jsx` — hero section
4. `About.jsx` — about section
5. `Projects.jsx` — project cards with `.map()`
6. `Contact.jsx` — contact section
7. `Footer.jsx` — footer

**Hint:** Move your CSS to `App.css` and import it in `App.jsx`.

### Your Turn

1. Create a React app (use Vite)
2. Delete the default code
3. Build a simple counter (increase, decrease, reset buttons)
4. Add a list where you can type items and add them (use `useState` with an array)
5. Fetch data from a public API (use `useEffect`) and display it

**If you get stuck:** The React docs at https://react.dev are excellent — read them before Googling.

---

## 15. The Complete Reference

### 15.1 HTML Quick Reference

```html
<!-- Document Structure -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
</head>
<body>
  <!-- Content -->
</body>
</html>

<!-- Text -->
<h1> to <h6>  Headings
<p>            Paragraph
<strong>       Bold
<em>           Italic
<br>           Line break
<hr>           Horizontal rule

<!-- Links -->
<a href="url">Link text</a>
<a href="url" target="_blank">New tab</a>
<a href="#section">Jump within page</a>

<!-- Media -->
<img src="url" alt="description">
<audio src="file.mp3" controls></audio>
<video src="file.mp4" controls></video>

<!-- Lists -->
<ul><li>Item</li></ul>         Unordered
<ol><li>Item</li></ol>         Ordered

<!-- Forms -->
<form action="/submit" method="POST">
  <input type="text">
  <input type="email">
  <input type="password">
  <input type="number">
  <input type="checkbox">
  <input type="radio" name="group">
  <textarea rows="4"></textarea>
  <select>
    <option value="1">Option 1</option>
  </select>
  <button type="submit">Submit</button>
</form>

<!-- Containers -->
<div>          Block container
<span>         Inline container
<header>       Page/section header
<nav>          Navigation
<main>         Main content
<section>      Thematic group
<article>      Self-contained content
<aside>        Sidebar
<footer>       Page/section footer
```

### 15.2 CSS Quick Reference

```css
/* Selectors */
element { }        /* All <element> tags */
.class { }         /* class="class" */
#id { }            /* id="id" */
parent child { }   /* child inside parent */
element.class { }  /* <element class="class"> */
selector1, selector2 { }  /* Multiple selectors */

/* Box Model */
width, height
padding: 10px;                        /* All sides */
padding: 10px 20px;                   /* Top/bottom Left/right */
padding: 10px 15px 20px 25px;         /* Top Right Bottom Left */
margin: 10px;
margin: 0 auto;                       /* Center horizontally */
border: 1px solid black;
border-radius: 8px;
border-radius: 50%;                   /* Circle */
box-sizing: border-box;               /* Include padding in width */

/* Display */
display: block;
display: inline;
display: inline-block;
display: none;                        /* Hide */
display: flex;
display: grid;

/* Flexbox (parent) */
display: flex;
flex-direction: row | column;
justify-content: flex-start | center | space-between | space-around;
align-items: stretch | center | flex-start | flex-end;
flex-wrap: wrap;
gap: 10px;

/* Flexbox (child) */
flex: 1;                              /* Grow equally */
flex: 0 0 200px;                      /* Fixed width */
align-self: center;

/* Text */
color, font-size, font-weight, font-family
text-align, text-decoration, line-height

/* Background */
background-color, background-image, background-size
background: linear-gradient(to right, blue, purple);

/* Position */
position: static | relative | fixed | absolute | sticky;
top, right, bottom, left;
z-index: 10;

/* Responsive */
@media (max-width: 768px) { ... }
@media (min-width: 1024px) { ... }

/* Animation */
transition: all 0.3s ease;
@keyframes name { from { } to { } }
animation: name 1s ease;
```

### 15.3 JavaScript Quick Reference

```javascript
// Variables
let x = 5;          // Can reassign
const y = 10;       // Cannot reassign

// Data Types
'string', 42, true, [1, 2, 3], { key: 'value' }, null, undefined

// Functions
function name(params) { return value; }
const name = (params) => value;

// Arrays
[1, 2, 3].map(fn)        // Transform
[1, 2, 3].filter(fn)     // Filter
[1, 2, 3].find(fn)       // Find first
[1, 2, 3].forEach(fn)    // Loop
[1, 2, 3].some(fn)       // Any match?
[1, 2, 3].every(fn)      // All match?
[1, 2, 3].includes(2)    // Contains?
[1, 2, 3].push(4)        // Add to end
[1, 2, 3].pop()          // Remove from end

// DOM
document.getElementById('id')
document.querySelector('.class')
document.querySelectorAll('div')
element.textContent = 'text'
element.innerHTML = '<em>html</em>'
element.style.color = 'red'
element.classList.add('class')
element.classList.remove('class')
element.classList.toggle('class')
document.createElement('tag')
parent.appendChild(child)
element.remove()
element.addEventListener('click', fn)

// Async
async function fetchData() {
  try {
    const res = await fetch('/api/data');
    const data = await res.json();
    return data;
  } catch (err) {
    console.error(err);
  }
}

// Fetch
fetch('/api/data', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ key: 'value' }),
});
```

### 15.4 Express Quick Reference

```javascript
const express = require('express');
const app = express();
app.use(express.json());

// Routes
app.get('/path', (req, res) => { });
app.post('/path', (req, res) => { });
app.put('/path/:id', (req, res) => { });
app.delete('/path/:id', (req, res) => { });

// Request
req.params    // URL parameters (e.g., :id)
req.query     // Query string (?search=term)
req.body      // POST/PUT body (requires express.json())
req.headers   // Headers

// Response
res.json(obj)           // Send JSON
res.status(404)         // Set status code
res.send('text')        // Send text
res.redirect('/url')    // Redirect
res.sendFile('path')    // Send file

// Middleware
app.use(fn);
app.use('/api', fn);

// Start
app.listen(PORT, () => console.log(`Running on ${PORT}`));
```

---

## 16. Troubleshooting — When Things Break

Building software means things break. Constantly. This is normal. Here's how to fix them.

### "Module not found" / "Cannot find module 'express'"

```bash
npm install            # Install all dependencies from package.json
npm install express    # Or install a specific package
```

Also check: are you in the right directory? Your `node_modules` folder must be where your `package.json` is.

### "Port 3000 is already in use"

Something is already running on that port:

```bash
# Find what's using the port
netstat -ano | findstr :3000

# Kill the process (replace PID with the number)
taskkill /PID 1234 /F
```

Or just use a different port:
```javascript
const PORT = process.env.PORT || 3001;
```

### "Cannot GET /api/notes"

Your route isn't defined or there's a typo:
- Check that the route exists in `server.js`
- Check the URL for typos (is it `/api/notes` or `/api/note`?)
- Check that the HTTP method matches (GET vs POST)

### Network Error / CORS Error

```
Access to fetch at 'http://localhost:3001' from origin 'http://localhost:5500'
has been blocked by CORS policy
```

Solutions:
1. Make sure CORS middleware is installed and used: `app.use(cors())`
2. Make sure the backend server is actually running
3. Make sure the URL is correct (including port number)

### "Cannot read property 'map' of undefined"

You're trying to loop over something that isn't an array. The API returned `undefined` or `null`:

```javascript
// ❌ Wrong
data.map(item => ...)  // If data is undefined, this crashes

// ✅ Right
(data || []).map(item => ...)  // Safe: use empty array if data is falsy

// Even better:
if (!data) return [];
return data.map(item => ...);
```

### "Unexpected token '<'" 

Your API returned HTML instead of JSON. This usually means:
- The URL is wrong and you hit a 404 HTML page
- The server sent HTML instead of JSON
- You forgot to set `Content-Type: application/json`

Check what the server is actually returning (open the URL in your browser and look).

### "NaN" (Not a Number)

You're doing math with something that isn't a number:

```javascript
console.log(5 + undefined);  // NaN
console.log(parseInt('abc')); // NaN

// Fix: validate your inputs
const num = parseInt(value) || 0;
```

### "undefined is not a function"

You tried to call something as a function that isn't one:

```javascript
// Common cause: forgetting 'new' with constructors
// Or: the function hasn't loaded yet (script order!)

// Fix: check script loading order in HTML
```

### "Cannot set property 'innerHTML' of null"

JavaScript can't find the element you're looking for:

```javascript
// This happens when:
// 1. The element doesn't exist in HTML
// 2. Your script runs BEFORE the element loads

// Fix: put script at bottom of body, or use DOMContentLoaded
document.addEventListener('DOMContentLoaded', () => {
  const el = document.getElementById('myElement');
  // This will work now
});
```

### My changes aren't showing up

1. **Hard refresh:** `Ctrl+Shift+R` (bypasses cache)
2. **Check the right file:** Are you editing the file the server is serving?
3. **Restart the server:** If you changed `server.js`, you need to restart Node
4. **Clear browser cache:** Settings → Clear browsing data → Cached images and files

### The golden rule of debugging

**Change one thing at a time, then test.**

If you change 10 things and it breaks, you don't know which change caused it. Change one line, test, change another line, test.

### The debugger's checklist

When something breaks, go through this order:

```
1. Check the browser console (F12) — is there a red error?
2. Check the network tab — what status codes?
3. Check the server terminal — any error messages?
4. Is the server running? (Did it crash?)
5. Is the URL correct? (No typos?)
6. Are the file paths correct? (../ vs ./)
7. Is the data format correct? (JSON vs string)
8. Did you restart the server after changing server code?
9. Did you hard refresh the browser?
10. Ask someone. Seriously. Fresh eyes see things you miss.
```

### Browser DevTools — The Superpower You Didn't Know You Had

Every browser comes with built-in developer tools. They're like an MRI machine for your website — you can see inside, inspect every part, and diagnose exactly what's wrong.

**Open DevTools:**
- **Windows/Linux:** `F12` or `Ctrl + Shift + I`
- **Mac:** `Cmd + Option + I`

#### The Elements Tab — Your Live HTML/CSS Editor

Right-click anything on a page and click "Inspect." The Elements tab opens showing the HTML tree. Click any element to see its CSS styles.

**You can edit CSS live!** Click a CSS property value and type a new number. Watch the page change instantly. This is the BEST way to design — tweak in DevTools, then copy the working CSS to your file.

**What to do here:**
- Click elements to see their box model (margin, border, padding, content)
- Toggle CSS properties on/off (checkboxes) to see what each one does
- Change colors, sizes, fonts — see results immediately
- Click the `+` button to add new CSS rules

```css
/* 👇 DevTools shows you this for the selected element */
/* Element: <h1 class="title"> */
/* Styles panel on the right */
h1.title {
  font-size: 32px;   ← Click this number, type "48", see it grow
  color: #333;        ← Click the color swatch, pick a new color
}
```

**Pro tip:** The "Computed" tab shows you the FINAL rendered value of every CSS property after all cascading, inheritance, and specificity wars are resolved. If your element is 342px wide and you have NO idea why, Computed tab is your detective.

#### The Console Tab — Talk to Your Page in Real Time

The Console is a JavaScript REPL (Read-Eval-Print Loop) — type any JS, press Enter, it runs immediately.

```javascript
// Type these in the Console:
document.title = "Hacked!"  // Changes the page title
console.log("hello from the console")  // Your console.log output appears here
document.querySelector('h1').style.color = 'red'  // Changes an element live
```

**When something breaks, the console tells you why:**
```
Uncaught TypeError: Cannot read properties of undefined (reading 'length')
```
This means you tried to access `.length` on something that doesn't exist. Look at the line number — that's where the bug is.

**Console API you'll use daily:**
```javascript
console.log("debug value:", someVariable);    // Basic logging
console.error("something broke:", error);     // Red error (stands out)
console.warn("this might be a problem", val); // Yellow warning
console.table(arrayOfObjects);                // Shows arrays as tables
console.time("myTimer");                      // Start a timer
// ... code ...
console.timeEnd("myTimer");                   // Prints "myTimer: 342ms"
```

#### The Network Tab — Watch Every Request

The Network tab shows ALL HTTP requests your page makes — API calls, images, CSS files, everything.

**How to use it:**
1. Open the Network tab
2. Refresh the page (or trigger an API call)
3. Watch the requests fly in

**What to look for:**
- **Red items** = failed requests (4xx or 5xx status)
- **Status codes** — 200 is good, 404 means wrong URL, 500 means server crashed
- **Timing** — how long each request took
- **Preview/Response** — see what the server actually sent back

**You are debugging an API call that returns empty data. What do you do?**
1. Open Network tab
2. Find the API request in the list
3. Click it → see the Response tab
4. Read what the server actually returned
5. Now you know: is the bug in your code (wrong URL, bad parsing) or the server (empty response)?

#### The Sources Tab — Debug Like a Pro

Set breakpoints — pause code execution at a specific line and inspect EVERY variable:

1. Open Sources tab
2. Find your JavaScript file
3. Click the line number where you want to pause
4. Reload the page or trigger the action

When execution hits your breakpoint:
- Hover over variables to see their values
- Step through line by line with the arrow buttons
- Watch variables change in real time

**The Step Over button (▶️ with a dot)** — runs the current line and stops at the next. If your function returns the wrong value, step through it line by line and watch when it goes wrong.

#### The Application Tab — Storage, Cookies, Cache

See everything your website has stored in the browser:

- **Local Storage** — data stored per origin
- **Session Storage** — clears when tab closes
- **Cookies** — small data sent with every request
- **IndexedDB** — larger client-side database
- **Cache Storage** — cached API responses and assets

**Quick fix for "my app is acting weird":** Application tab → Clear site data. Often fixes weird state bugs.

#### The Performance Tab — Why Is It Slow?

Record your page loading and see a flame chart of everything the browser did. Green bars = painting, yellow = JavaScript, purple = layout. Long bars = slow code.

**Don't worry about this tab yet.** Just know it exists for when you eventually need to fix a slow page.

#### Lighthouse Tab — The Report Card

Audit your site for performance, accessibility, SEO, and best practices. It gives you a score (0-100) and tells you exactly how to fix each problem.

1. Open Lighthouse tab
2. Click "Analyze page load"
3. Wait 30 seconds
4. Read your report — fix anything below 90

#### The 80/20 of DevTools

| Tab | When to Use It |
|---|---|
| **Elements** | When CSS isn't doing what you expect |
| **Console** | Always — keep it open. Errors appear here. |
| **Network** | When API calls fail or data doesn't load |
| **Sources** | When a function returns the wrong value |
| **Application** | When localStorage, cookies, or cache are misbehaving |
| **Lighthouse** | Before deploying to production |

#### Your Turn

1. Open any website, inspect an element, change its text in the HTML panel
2. Type `document.title = "My First Hack"` in the console
3. Open the Network tab, refresh — find all the 200s and any 404s
4. Find a JavaScript file in Sources, put a breakpoint on line 5, reload
5. Open Application → Local Storage, see what's stored
6. Run a Lighthouse audit on your own project page

Do this for 15 minutes. You'll feel like you have x-ray vision into every website.

### The Essentials (Bookmark These)

| Site | URL | Why |
|---|---|---|
| **MDN Web Docs** | https://developer.mozilla.org | The official web documentation. HTML, CSS, JS — everything is here. |
| **JavaScript.info** | https://javascript.info | Best in-depth JavaScript tutorials. Read the whole thing. |
| **CSS-Tricks** | https://css-tricks.com | Flexbox guide, Grid guide, and a million useful CSS articles. |
| **Can I Use** | https://caniuse.com | Check if a browser feature is supported before using it. |
| **DevDocs** | https://devdocs.io | Offline-capable documentation browser. All docs in one place. |
| **Node.js Docs** | https://nodejs.org/docs/latest/api/ | Official Node.js documentation. |
| **Express Docs** | https://expressjs.com | Official Express.js documentation and guides. |

### Practice & Learning Platforms

| Site | What it's good for |
|---|---|
| **freeCodeCamp** | https://freecodecamp.org — Interactive HTML/CSS/JS curriculum, free certification |
| **The Odin Project** | https://theodinproject.com — Full stack curriculum, project-based |
| **Frontend Mentor** | https://frontendmentor.io — Real designs to code up, get feedback |
| **Codecademy** | https://codecademy.com — Interactive lessons (free and paid) |
| **Exercism** | https://exercism.org — Practice coding challenges with mentorship |

### Tools You'll Use Daily

| Tool | Link | What it does |
|---|---|---|
| **VS Code** | https://code.visualstudio.com | Your code editor (you already have this) |
| **Live Server** | VS Code Extensions → search "Live Server" | Auto-refresh browser on save |
| **Prettier** | VS Code Extensions → search "Prettier" | Auto-format your code |
| **Postman** | https://postman.com | Test APIs without writing frontend code |
| **JSON Formatter** | Chrome extension | Makes JSON readable in the browser |
| **React DevTools** | Chrome extension | Debug React apps |
| **Color Hunt** | https://colorhunt.co | Color palette inspiration |
| **Coolors** | https://coolors.co | Generate color schemes |
| **Font Awesome** | https://fontawesome.com | Icons for your site |
| **Google Fonts** | https://fonts.google.com | Free fonts for your site |

### Cheat Sheets (Print These)

| Topic | What it covers |
|---|---|
| **HTML Cheat Sheet** | See separate file: `Full Stack Web Development - HTML Cheat Sheet and Poster.md` |
| **CSS Flexbox** | https://css-tricks.com/snippets/css/a-guide-to-flexbox/ |
| **CSS Grid** | https://css-tricks.com/snippets/css/complete-guide-grid/ |
| **ES6 Cheat Sheet** | https://devhints.io/es6 |
| **Git Cheat Sheet** | https://education.github.com/git-cheat-sheet-education.pdf |
| **HTTP Status Codes** | https://httpstatuses.com |

### Free Hosting & Deployment

| Service | For | Free tier limits |
|---|---|---|
| **Vercel** | Frontend (static sites) | Unlimited, generous |
| **Netlify** | Frontend (static sites) | Unlimited, generous |
| **Render** | Backend (Node.js) | 512MB RAM, sleeps after inactivity |
| **Railway** | Backend (Node.js) | $5 credit/month (usually free for small apps) |
| **GitHub Pages** | Frontend (static sites) | Unlimited, 1GB storage |
| **Supabase** | Database (PostgreSQL) | 500MB database, free |
| **MongoDB Atlas** | Database (MongoDB) | 512MB storage, free |
| **Cloudflare Pages** | Frontend (static sites) | Unlimited, generous |

### YouTube Channels to Follow

| Channel | Best for |
|---|---|
| **Traversy Media** | Full stack tutorials, project-based |
| **Web Dev Simplified** | Clear, focused explanations |
| **Fireship** | Short, high-energy code explanations |
| **The Net Ninja** | Complete playlists (React, Node, Firebase, etc.) |
| **Academind** | In-depth tutorials with great explanations |
| **Kevin Powell** | CSS mastery — best CSS channel on YouTube |
| **Fun Fun Function** | JavaScript concepts with personality |

### The "I'm Stuck" Protocol

1. Read the error message carefully (it usually tells you exactly what's wrong)
2. Copy-paste the error into Google
3. Check **Stack Overflow** (99% of errors have been solved there)
4. Ask in a community:
   - **r/learnprogramming** (Reddit)
   - **r/webdev** (Reddit)
   - **Stack Overflow** (search first, then ask)
   - **Discord servers** for the specific tech you're using
5. Take a 15-minute break. Walk away. The answer often appears when you stop looking.

---

## 17. Glossary

A quick-reference dictionary of terms used throughout this guide, in plain English.

| Term | Plain English Definition | See Also |
|---|---|---|
| **API** (Application Programming Interface) | A waiter between two programs. You tell it what you want, it brings the response. Like a menu — you don't need to know the kitchen. | Chapter 10 |
| **Backend** | The part of a web app that runs on a server. Handles logic, databases, authentication. The "kitchen" of the restaurant analogy. | Chapter 7 |
| **CORS** (Cross-Origin Resource Sharing) | A browser security rule. If your frontend (domain A) tries to talk to an API on domain B, the browser blocks it unless the server says "it's OK." | Chapter 10, Chapter 11.5 |
| **CSS** (Cascading Style Sheets) | The language that makes HTML look good — colors, layout, fonts, animations. The "plating" of the restaurant analogy. | Chapter 5 |
| **Database** | A structured place to store data permanently. Like a filing cabinet for your app. SQLite stores data in a single file; Supabase is cloud-based. | Chapter 8 |
| **DNS** (Domain Name System) | The phonebook of the internet. Converts `google.com` into an IP address like `142.250.80.14`. | Chapter 2 |
| **DOM** (Document Object Model) | The browser's internal representation of your HTML. JavaScript can read and modify it. Think of it as a tree of elements. | Chapter 6.12 |
| **Endpoint** | A specific URL on an API. Like `/api/users` or `/api/login`. Each endpoint does one thing. | Chapter 10 |
| **Express** | A Node.js framework for building servers. Like a pre-built kitchen with all the tools ready. | Chapter 7 |
| **Fetch** | A browser function for making HTTP requests from JavaScript. `fetch('/api/data')` sends a request and returns a Promise. | Chapter 6.15 |
| **Frontend** | The part of a web app that runs in the browser (HTML, CSS, JS). What the user sees and interacts with. The "dining room." | Chapters 4-6 |
| **Full Stack** | Building both frontend AND backend. Full stack developers can build an entire web app themselves. | Chapter 1 |
| **Git** | A tool that tracks changes to your code over time. Like "Track Changes" in Word, but for code. | Chapter 12 |
| **GitHub** | A website that stores Git repositories online. Like Google Drive but for code. | Chapter 12 |
| **Hook** (React) | A function that lets you "hook into" React features (state, effects, etc.). Always starts with `use`. | Chapter 14 |
| **HTML** (HyperText Markup Language) | The structure language of web pages. Headings, paragraphs, links, images — all defined with HTML tags. | Chapter 4 |
| **HTTP** (HyperText Transfer Protocol) | The protocol browsers and servers use to communicate. Every web request is an HTTP request. | Chapter 2 |
| **HTTPS** | HTTP with encryption (SSL/TLS). The padlock icon in your browser. All production sites should use it. | Chapter 11 |
| **JavaScript** | The programming language of the web. Runs in browsers (frontend) and on servers (Node.js). | Chapter 6 |
| **JSX** | An HTML-like syntax used in React. Gets compiled into JavaScript. Example: `<h1>Hello</h1>` inside a `.jsx` file. | Chapter 14 |
| **JSON** | A text format for data exchange. Looks like: `{"name": "Alice", "age": 30}`. APIs use JSON for sending/receiving data. | Chapter 10 |
| **Middleware** | Functions that run in the middle of a request-response cycle. Used for logging, authentication, parsing, etc. | Chapter 7.6 |
| **Node.js** | A runtime that lets you run JavaScript on your computer (not just in browsers). Used for building servers. | Chapter 3, 7 |
| **NPM** (Node Package Manager) | A library of free code packages. `npm install express` downloads Express and all its dependencies. | Chapter 7 |
| **Promise** | Represents a value that will be available in the future (async). Has `.then()` and `.catch()` methods. | Chapter 6.15 |
| **Props** (React) | Data passed from a parent component to a child. Read-only. Like function arguments for components. | Chapter 14 |
| **Render** | The process of converting code into pixels on screen. Or a cloud hosting service (Render.com). | Chapter 11 |
| **Responsive Design** | Making a website work on all screen sizes (phone, tablet, desktop) using CSS media queries and flexible layouts. | Chapter 5.8 |
| **REST** | A style of building APIs. Uses HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations on resources. | Chapter 10 |
| **Server** | A computer that runs 24/7 and responds to requests. When you deploy, your code runs on a server. | Chapter 7 |
| **SQL** (Structured Query Language) | The language for talking to databases. `SELECT * FROM users WHERE id = 1` means "get user with ID 1." | Chapter 8 |
| **State** (React) | Data that changes over time and affects what's displayed. Managed with `useState` hook. | Chapter 14 |
| **URL** (Uniform Resource Locator) | A web address. `https://example.com/page?q=hello#section` — protocol, domain, path, query, fragment. | Chapter 2 |
| **Vercel** | A cloud platform for deploying frontend apps. Free tier available. Recommended for deploying in this guide. | Chapter 11 |

### How to Use This Glossary

When you encounter an unfamiliar term while reading:
1. Look it up here first
2. Check the "See Also" column for the relevant chapter
3. If it's not here, Google "what is [term] in web development"

---

## 18. Practice Projects

The gap between "I read the tutorial" and "I can build things" is filled by **doing**. These 5 projects are ordered by difficulty. Do them in order. Don't skip.

### Before You Start: How to Approach Projects

**The single biggest mistake beginners make:** reading the whole guide, then trying to build a project from memory. That's not how it works.

**The right way:**
1. Read the project description
2. Try to write the code yourself
3. Get stuck? Look at the hint. Try again.
4. Still stuck? Look at the solution code. Understand each line before moving on.
5. After finishing, build it again from scratch without looking.

**This is called "active learning."** It's slower but 10x more effective.

> **Solutions available** at `solutions/` alongside this guide. Open the corresponding solution file ONLY when you're truly stuck — and understand every line before moving on.

---

### Project 1: Personal Portfolio Site

**Difficulty:** HTML + CSS only  
**What you'll learn:** Structuring a page, styling, responsive design, deploying

#### File Structure

```
portfolio/
├── index.html
└── style.css
```

#### Step 1: Plan it

Draw your page on paper first. A portfolio usually has:
- A hero section (your name, tagline, a button)
- An about section
- A projects section (cards with descriptions)
- A contact section (email link or form)
- A footer

```
┌─────────────────────────────────┐
│           NAV BAR               │
│  Home | About | Projects | Contact
├─────────────────────────────────┤
│                                 │
│         HERO SECTION            │
│   "Hi, I'm [Your Name]"         │
│   "I build things for the web"  │
│       [See My Work]             │
│                                 │
├─────────────────────────────────┤
│           ABOUT                 │
│   A photo + a paragraph about   │
│   yourself and what you do.     │
│                                 │
├─────────────────────────────────┤
│          PROJECTS               │
│  ┌──────┐ ┌──────┐ ┌──────┐    │
│  | Proj | | Proj | | Proj |    │
│  |  1   | |  2   | |  3   |    │
│  └──────┘ └──────┘ └──────┘    │
│                                 │
├─────────────────────────────────┤
│          CONTACT                │
│   "Say hello at me@email.com"   │
├─────────────────────────────────┤
│            FOOTER               │
│   © 2026 Your Name              │
└─────────────────────────────────┘
```

#### Step 2: HTML structure

Create `index.html`. Use a `<nav>` for navigation, a `<section>` for each section (hero, about, projects, contact), and a `<footer>`. Style it with `style.css`. Write your own CSS using what you learned in Chapter 5.

**Hint:** Use a fixed nav with `position: fixed`, a full-viewport hero with `min-height: 100vh`, a CSS Grid for the project cards, and media queries for mobile.

#### Step 3: CSS (Try yourself first!)

Write your own styles. Use flexbox for the nav and about section, grid for the project cards. Make it responsive with `@media (max-width: 768px)`.

**Hint for the color scheme:** Use a gradient background for the hero (purple/blue like `linear-gradient(135deg, #667eea, #764ba2)`) and white cards with subtle shadows.

#### Step 4: Deploy

Push this to GitHub and deploy on Vercel (see Chapter 11). Send the link to a friend.

**When you're done:** You have a live website on the internet that you built from scratch. That's not nothing. That's everything.

#### Extension ideas:
- Add a dark mode toggle (JavaScript)
- Make the project cards come from a JavaScript array (data-driven)
- Add a contact form that sends you an email (needs backend)

---

### Project 2: Calculator

**Difficulty:** JavaScript DOM  
**What you'll learn:** Events, functions, string manipulation, state management

#### File Structure

```
calculator/
├── calculator.html
├── calc-style.css
└── calc.js
```

#### Step 1: Plan it

A calculator has:
- A display (shows the current number/result)
- Number buttons (0-9, decimal point)
- Operator buttons (+, -, ×, ÷)
- An equals button (=)
- A clear button (C)

Layout:
```
┌─────────────────┐
│        0        │  ← display
├───┬───┬───┬───┤
│ 7 │ 8 │ 9 │ ÷ │
├───┼───┼───┼───┤
│ 4 │ 5 │ 6 │ × │
├───┼───┼───┼───┤
│ 1 │ 2 │ 3 │ - │
├───┼───┼───┼───┤
│ 0 │ . │ C │ + │
└───┴───┴───┴───┘
```

#### Step 2: Build the HTML + CSS (your turn)

Create `calculator.html` with:
- A `<div class="display">` for the output
- Buttons inside a `<div class="buttons">` container
- Use `data-value` attributes on buttons to store their values

**Your Turn:** Write the CSS yourself. Make it look like a real calculator — dark background, rounded buttons, nice hover effects.

**Hint for the layout:** Use CSS Grid for the button grid (`grid-template-columns: repeat(4, 1fr)`). Make the equals button span 2 or 4 columns.

#### Step 3: The JavaScript

**Try to write this yourself first. Here's how to think about it:**

- You need to track: the current number being typed, the previous number, the selected operation, and whether you just pressed equals
- When a number is clicked: append it to the current number (unless it's a new calculation after equals)
- When an operator is clicked: store the current number, store the operator, reset for next number
- When equals is clicked: perform the calculation using the stored numbers and operator
- When C is clicked: reset everything

**The key insight:** The calculator has "state" — variables that change over time. Managing state is one of the most important skills in programming.

**Check your solution against these test cases:**
- `2 + 3 =` → 5
- `10 / 2 =` → 5
- `5 * 5 =` → 25
- `7 / 0 =` → "Error"

#### Step 4: Test it

**If something doesn't work:** Use `console.log()` to print your variables at each step. This is called "debug logging" and it's how professionals debug.

#### Extension ideas:
- Add keyboard support (press keys on your keyboard to type numbers)
- Add a backspace button
- Add a square root button
- Add memory (M+, M-, MR, MC)

---

### Project 3: Weather App

**Difficulty:** JavaScript + API consumption  
**What you'll learn:** Fetching data from a real API, handling async, displaying dynamic data

#### File Structure

```
weather-app/
├── weather-index.html
├── weather-style.css
└── weather.js
```

#### What we're building

A page where you type a city name and see the current weather: temperature, humidity, weather description, and an icon.

#### Step 1: Get a free API key

1. Go to [https://openweathermap.org/api](https://openweathermap.org/api)
2. Sign up for a free account
3. Go to your dashboard → API Keys
4. Copy your key (it looks like `abc123def456...`)
5. **Important:** The free plan allows 60 calls/minute — more than enough for learning

#### Step 2: HTML

Create `weather-index.html` with:
- An input field and a "Search" button
- A result area (hidden by default) to display city name, date, temperature, weather icon, description, humidity, wind, and feels-like
- An error message area (hidden by default)

**Hint:** Use `id` attributes on all the dynamic elements so you can reference them in JavaScript.

#### Step 3: CSS (Try yourself!)

Write the CSS to make it look like a weather app — clean, centered, with a gradient background. The weather result card should appear after searching.

**Hint:** Use a nice blue gradient background. Make the temperature very large (like 64px). Center everything.

#### Step 4: JavaScript

**Try to write this yourself first. Here's the structure you need:**

Store your API key in a constant and use `https://api.openweathermap.org/data/2.5/weather` as the API URL. Attach a click event to the search button and a `keydown` event for Enter on the input. The `getWeather` function should be `async`, use `fetch()` with `encodeURIComponent(city)`, and include `units=metric` and `appid=YOUR_KEY`. Handle errors: 404 (city not found), 401 (invalid key), and network errors. The `displayWeather` function should update all the DOM elements with data from the response.

**Response structure from the API:**
```
data.name         → "London"
data.sys.country  → "GB"
data.main.temp    → 15.2
data.main.humidity → 72
data.wind.speed   → 4.1
data.main.feels_like → 13.8
data.weather[0].description → "clear sky"
data.weather[0].icon → "01d"
```

**Icon URL pattern:** `https://openweathermap.org/img/wn/{icon}@2x.png`

#### Step 5: Test it

- Type "London" → see London's weather
- Type "Tokyo" → see Tokyo's weather
- Type "asdfgh" → see the error message
- Type your own city

**Common problem:** If it says "Invalid API key", you either didn't replace the placeholder with your actual key, or the key just needs a few minutes to activate.

#### Extension ideas:
- Add a 5-day forecast (use OpenWeatherMap's forecast endpoint)
- Add a "Use My Location" button (use the Geolocation API)
- Change the background based on weather (sunny = yellow, rainy = blue)
- Add a loading spinner while fetching

---

### Project 4: Blog with Comments

**Difficulty:** Full stack (frontend + backend + database with relationships)  
**What you'll learn:** Foreign keys, JOINs, related data, forms with validation

#### File Structure

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

#### What we're building

A blog where:
- Anyone can view posts and comments
- Anyone can create a post (title + content)
- Anyone can comment on a post
- Each comment shows the post it belongs to

#### Step 1: Backend setup

```bash
mkdir blog-app
cd blog-app
mkdir backend frontend
cd backend
npm init -y
npm install express better-sqlite3 cors
```

#### Step 2: Database with two related tables

Create `backend/database.js`. Use `better-sqlite3` to create a database with two tables:

```sql
CREATE TABLE posts (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  content TEXT NOT NULL,
  author TEXT NOT NULL DEFAULT 'Anonymous',
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE comments (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  post_id INTEGER NOT NULL,
  author TEXT NOT NULL DEFAULT 'Anonymous',
  body TEXT NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE
);
```

**Notice the relationship:** A `post` has many `comments`. The `post_id` in the comments table is a **foreign key** — it connects each comment to its parent post. The `ON DELETE CASCADE` means deleting a post automatically deletes its comments.

#### Step 3: API server

Create `backend/server.js`. Build these API endpoints:

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/posts` | Get all posts (with comment count) |
| GET | `/api/posts/:id` | Get single post + its comments |
| POST | `/api/posts` | Create a new post |
| DELETE | `/api/posts/:id` | Delete a post (cascades to comments) |
| POST | `/api/posts/:id/comments` | Add a comment to a post |
| DELETE | `/api/comments/:id` | Delete a comment |

**Hint for the GET all posts query:** Use a `LEFT JOIN` with `COUNT` and `GROUP BY` to include the comment count in each post.

#### Step 4: Frontend

**Your Turn:** Build the frontend yourself! Here's what it needs:

**Pages/views (all on one page):**
1. A list of all posts (title + author + comment count + date)
2. Click a post → show its full content + comments
3. A form to create a new post
4. A form to add a comment to a post

**HTML structure hint:**
```html
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
```

**JavaScript logic:**
- On load, fetch all posts and display them
- Clicking a post: hide the posts list, show the post view, fetch the post + comments
- The "Back" button: hide post view, show posts list
- Submit post form: POST to `/api/posts`, then refresh the list
- Submit comment form: POST to `/api/posts/:id/comments`, then refresh comments

**Try to write the JavaScript yourself.** You have all the pieces from Chapter 6 and 9. If you get stuck, look at the notes app code for reference — it uses the same patterns.

#### Step 5: Run it

```bash
cd backend
node server.js
```

Visit `http://localhost:3001` if you set up `express.static`, or open the frontend with Live Server and use `http://localhost:3001` as the API base.

#### Why this project matters

This is your first project with **related data** (posts have comments). This is how nearly every real app works:
- Twitter: users have tweets, tweets have likes
- Instagram: users have posts, posts have comments
- Amazon: products have reviews

**Understanding relationships is what separates beginners from intermediate developers.**

#### Extension ideas:
- Add an "Edit" button for posts
- Add a "Like" button on posts (new table: likes)
- Add user registration so only the author can edit/delete
- Add markdown support for post content (bold, italic, links)

---

### Project 5: URL Shortener

**Difficulty:** Full stack + redirects  
**What you'll learn:** URL redirection, generating unique codes, copy-to-clipboard

#### File Structure

```
url-shortener/
├── backend/
│   ├── database.js
│   ├── server.js
│   └── package.json
└── frontend/
    └── index.html
```

#### What we're building

A site like bit.ly: paste a long URL, get a short one like `http://localhost:3001/abc123`. Visiting the short URL redirects to the original.

#### How it works

```
User visits: http://localhost:3001/abc123
Server looks up "abc123" in the database
Found! The original URL is "https://very-long-url.com/..."
Server sends back: 302 Redirect → "https://very-long-url.com/..."
```

#### Step 1: The database

```sql
CREATE TABLE IF NOT EXISTS urls (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  code TEXT NOT NULL UNIQUE,
  original_url TEXT NOT NULL,
  clicks INTEGER DEFAULT 0,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

#### Step 2: Server

Create `backend/server.js`. You need:
- `POST /api/shorten` — accepts `{ url }`, validates the URL, generates a random 6-char code, stores it, returns `{ shortUrl, code, originalUrl }`
- `GET /:code` — looks up the code, redirects (302) to the original URL, increments click count
- `GET /api/stats/:code` — returns all data for a code (for checking click counts)

**Hint for generating the code:** Use `crypto.randomBytes(4).toString('base64url').slice(0, 6)`.

#### Step 3: Frontend

Build a single-page frontend with:
- An input for the long URL
- A "Shorten" button
- When clicked → show the short URL
- A "Copy" button that copies to clipboard

**Hint for copying:** `navigator.clipboard.writeText(text)` returns a Promise.

#### Step 4: Try it

1. Start the backend: `cd backend && node server.js`
2. Open `http://localhost:3001` in your browser
3. Paste a long URL (like `https://developer.mozilla.org/en-US/docs/Web/JavaScript`)
4. Click "Shorten"
5. Click the short URL — it should redirect you to the original page

#### The magic

When you click the short URL, the browser sends a GET request to `http://localhost:3001/abc123`. The server's `/:code` route catches it, looks up the code in the database, and sends a `302 Redirect` response. The browser follows the redirect to the original URL. All of this happens in a fraction of a second.

#### Extension ideas:
- Add a QR code generator for each short URL
- Show click statistics (how many times each URL was visited)
- Add expiration dates for short URLs
- Add custom short codes (user picks the code instead of random)

---

### What to Build Next (Ideas for After These Projects)

Once you're comfortable with the basics, here are complete project descriptions to push you further.

---

#### Expense Tracker

| Level | Beginner–Intermediate |
|---|---|
| Stack | Frontend + backend + database |
| New concepts | Date handling, filtering, aggregation |

Track your daily expenses.

**Features:**
- Add an expense (amount, category, date, note)
- Show a list of all expenses, newest first
- Filter by category (Food, Transport, Bills, etc.)
- Show total spent per category
- Delete/edit an expense

**File structure:**
```
expense-tracker/
├── backend/
│   ├── database.js
│   ├── server.js
│   └── package.json
└── frontend/
    ├── index.html
    ├── style.css
    └── app.js
```

**Database hint:**
```sql
CREATE TABLE expenses (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  amount REAL NOT NULL,
  category TEXT NOT NULL,
  note TEXT,
  date TEXT NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**API endpoints:**
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/expenses` | All expenses (optional `?category=food` filter) |
| POST | `/api/expenses` | Add an expense |
| DELETE | `/api/expenses/:id` | Delete an expense |
| GET | `/api/expenses/summary` | Total per category |

**Extensions:** Add a chart (Chart.js), monthly budget limits, recurring expenses, export to CSV.

---

#### Habit Tracker

| Level | Beginner–Intermediate |
|---|---|
| Stack | Frontend + backend + database |
| New concepts | Date math, streaks, progress visualization |

Track habits you want to build (exercise, reading, coding, etc.).

**Features:**
- Add a habit (name, goal frequency)
- Mark today's habit as done (one click)
- Show current streak (consecutive days)
- Calendar view showing which days were completed
- Dashboard with all habits and their streaks

**File structure:**
```
habit-tracker/
├── backend/
│   ├── database.js
│   ├── server.js
│   └── package.json
└── frontend/
    ├── index.html
    ├── style.css
    └── app.js
```

**Database schema:** Two tables — `habits` (id, name, created_at) and `habit_logs` (id, habit_id, date, FOREIGN KEY). A habit is "done" on a day if a `habit_logs` row exists for that habit + date.

**The streak logic:** Query the logs for a habit ordered by date descending. Count consecutive days starting from today (or yesterday if today isn't logged yet). Break the count at the first missing day.

**Extensions:** Push notifications, weekly report email, habit categories, shareable streaks.

---

#### Bookmark Manager

| Level | Beginner–Intermediate |
|---|---|
| Stack | Frontend + backend + database |
| New concepts | URL validation, tags, search |

Save and organize bookmarks with tags.

**Features:**
- Add a bookmark (URL, title, tags)
- Tags as comma-separated or individual chips
- Click a bookmark → opens in new tab
- Search bookmarks by title or tag
- Filter by tag
- Delete bookmarks

**Database hint:**
```sql
CREATE TABLE bookmarks (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  url TEXT NOT NULL,
  title TEXT NOT NULL,
  tags TEXT,  -- store as comma-separated "frontend,react,tutorial"
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**Search hint:** Use SQL `LIKE` for searching: `WHERE title LIKE '%search%' OR tags LIKE '%search%'`.

**Extensions:** Import from browser bookmarks (HTML file upload), screenshots of pages, folder organization, share collections.

---

#### Chat Room

| Level | Intermediate |
|---|---|
| Stack | Frontend + backend + WebSocket |
| New concepts | WebSocket (`socket.io`), real-time communication, message history |

A real-time chat room where anyone can send messages and see them appear instantly.

**Features:**
- Join with a username
- Send messages (appear in real-time to all connected users)
- Show who's currently in the room
- Message history (last 50 messages)
- Auto-scroll to newest message
- Timestamps on messages

**Setup:**
```bash
npm install express socket.io
```

**Key concept — WebSocket vs HTTP:** HTTP is like sending a letter (you ask, the server responds, connection closes). WebSocket is like a phone call — both sides can talk anytime, and the line stays open. Socket.IO is a library that makes WebSocket easy.

**Server skeleton:**
```javascript
const http = require('http');
const express = require('express');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server);

io.on('connection', (socket) => {
  // socket.on('message', ...) — receive message
  // socket.broadcast.emit(...) — send to everyone else
  // io.emit(...) — send to everyone including sender
});

server.listen(3000);
```

**Frontend hint:**
```javascript
const socket = io();  // connects to the server
socket.emit('message', { text: 'Hello!' });  // send
socket.on('message', (data) => { /* render */ });  // receive
```

**Extensions:** Private messages, multiple rooms, typing indicator, emoji reactions, message editing.

---

#### Authentication System

| Level | Intermediate |
|---|---|
| Stack | Frontend + backend + database + security |
| New concepts | Password hashing (bcrypt), JWT tokens, cookies, protected routes |

A login/signup system that protects certain pages.

**Features:**
- Sign up (username, email, password)
- Log in (email + password)
- Log out
- Protected "dashboard" page (redirects to login if not authenticated)
- "Remember me" checkbox (longer token expiry)
- Show current user's name in the header

**Setup:**
```bash
npm install express bcryptjs jsonwebtoken cors
```

**Password hashing:**
```javascript
const bcrypt = require('bcryptjs');
const hash = await bcrypt.hash('user-password', 10);  // store hash
const match = await bcrypt.compare('user-password', hash);  // compare
```

**JWT flow:**
1. User logs in → server creates a JWT token (`jwt.sign({ userId }, SECRET, { expiresIn })`)
2. Server sends token to client (in a cookie or response body)
3. Client stores token (localStorage or cookie)
4. Client sends token with every protected request (Authorization header)
5. Server verifies token (`jwt.verify(token, SECRET)`)

**Database:**
```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  username TEXT NOT NULL UNIQUE,
  email TEXT NOT NULL UNIQUE,
  password_hash TEXT NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**Extensions:** OAuth (Login with Google/GitHub), email verification, password reset, 2FA, rate limiting.

---

#### Image Uploader

| Level | Intermediate |
|---|---|
| Stack | Frontend + backend + file handling |
| New concepts | File uploads, `multer`, serving static files, image preview |

Upload images and get a shareable URL.

**Features:**
- Drag-and-drop or click to select image
- Preview before uploading
- Upload button → stores image on server
- Show a shareable URL after upload
- Gallery page showing all uploaded images
- Click image → full-size view

**Setup:**
```bash
npm install express multer sharp
```

**Server upload handling (multer):**
```javascript
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });

app.post('/api/upload', upload.single('image'), (req, res) => {
  res.json({ url: `/uploads/${req.file.filename}` });
});
```

**Image processing (sharp):**
```javascript
const sharp = require('sharp');
await sharp(req.file.path)
  .resize(800)
  .jpeg({ quality: 80 })
  .toFile(`uploads/thumb-${req.file.filename}`);
```

**Extensions:** Image resize options, album organization, user-specific galleries (add auth), EXIF data display, delete images.

---

#### E-Commerce Store

| Level | Advanced |
|---|---|
| Stack | Full stack + shopping cart + payments |
| New concepts | Shopping cart session, checkout flow, payment integration (Stripe) |

A small store where users can browse products, add to cart, and "check out."

**Features:**
- Product listing page (name, price, image, add-to-cart button)
- Product detail page (description, larger image, quantity selector)
- Shopping cart (shows items, quantities, total price)
- Checkout form (name, address, payment)
- Order confirmation page

**Key design decisions:**
- Cart can be stored in the frontend (localStorage) or backend (session/database). Start with localStorage for simplicity.
- Products can be hardcoded or stored in a database.
- Don't implement real payments — use a "simulated" checkout that just confirms the order.

**Database:**
```sql
CREATE TABLE products (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  price REAL NOT NULL,
  description TEXT,
  image_url TEXT
);

CREATE TABLE orders (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  customer_name TEXT NOT NULL,
  customer_email TEXT NOT NULL,
  total REAL NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE order_items (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  order_id INTEGER NOT NULL,
  product_id INTEGER NOT NULL,
  quantity INTEGER NOT NULL,
  price REAL NOT NULL,
  FOREIGN KEY (order_id) REFERENCES orders(id),
  FOREIGN KEY (product_id) REFERENCES products(id)
);
```

**Extensions:** Stripe/PayPal integration, product categories, search, reviews and ratings, admin dashboard for managing products, inventory tracking.

---

#### Social Media Clone

| Level | Advanced |
|---|---|
| Stack | Full stack + relationships + feed |
| New concepts | Follow system, news feed algorithm, likes, notifications |

A mini social network where users post, follow each other, and see a feed.

**Features:**
- User profiles (avatar, bio, post count, followers/following)
- Follow/unfollow users
- Create posts (text, optional image)
- Like/unlike posts
- News feed showing posts from followed users (newest first)
- Notification when someone follows you or likes your post

**Database design (the hard part):**
```sql
CREATE TABLE users (...);
CREATE TABLE posts (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL REFERENCES users(id),
  content TEXT NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE follows (
  follower_id INTEGER NOT NULL REFERENCES users(id),
  followee_id INTEGER NOT NULL REFERENCES users(id),
  PRIMARY KEY (follower_id, followee_id)
);
CREATE TABLE likes (
  user_id INTEGER NOT NULL REFERENCES users(id),
  post_id INTEGER NOT NULL REFERENCES posts(id),
  PRIMARY KEY (user_id, post_id)
);
```

**Feed query (the key challenge):**
```sql
SELECT posts.*, users.username
FROM posts
JOIN users ON posts.user_id = users.id
WHERE posts.user_id IN (
  SELECT followee_id FROM follows WHERE follower_id = ?
)
OR posts.user_id = ?
ORDER BY posts.created_at DESC
LIMIT 50;
```

**Extensions:** Comments on posts, repost/share, direct messages, hashtags, image upload, infinite scroll, dark mode, mobile responsive.

---

#### Task Management App

| Level | Advanced |
|---|---|
| Stack | Full stack + drag-and-drop + project hierarchy |
| New concepts | Drag-and-drop (HTML5 or library), nested data, Kanban board |

A Trello-like app with projects, lists, and tasks.

**Features:**
- Create a project (name, description)
- Within a project: multiple lists (e.g., "To Do", "In Progress", "Done")
- Within each list: multiple tasks
- Drag tasks between lists (changes status)
- Edit task details (name, description, due date, assignee)
- Click a task → opens a detail modal

**Database (3-level hierarchy):**
```sql
CREATE TABLE projects (id, name, description, created_at);
CREATE TABLE lists (id, project_id, name, position, created_at);
CREATE TABLE tasks (id, list_id, title, description, due_date, position, created_at);
```

**Drag-and-drop:** Use the HTML5 Drag and Drop API:
```javascript
element.draggable = true;
element.addEventListener('dragstart', (e) => { e.dataTransfer.setData('text/plain', id); });
dropZone.addEventListener('dragover', (e) => e.preventDefault());
dropZone.addEventListener('drop', (e) => {
  const taskId = e.dataTransfer.getData('text/plain');
  // Move task to this list, update position
});
```

Or use a library like `SortableJS` for a smoother experience.

**Extensions:** Task comments, file attachments, labels/colors, search, calendar view, team collaboration (assign users to tasks), activity log.

---

### The Project Checklist

Before calling a project "done":

```
[ ] Does it work? (Test every feature)
[ ] Does it handle errors gracefully?
[ ] Does it work on mobile?
[ ] Is the code clean? (Indentation, naming, comments)
[ ] Is it deployed? (Can I share it?)
[ ] Did I learn something new?
```

The last one is the most important. If you learned something, the project succeeded.

If you've read through this entire guide, you now understand:

- How the web works (client-server, HTTP, DNS)
- HTML structure and semantics
- CSS styling, layout, and responsive design
- JavaScript programming (variables to async/await)
- Building a server with Node.js and Express
- Databases with SQL and SQLite
- Connecting frontend to backend
- Git version control
- Deploying to production
- How to debug when things break

**That's more than most people who call themselves "web developers" knew when they started.**

### What now?

1. **Build something.** Anything. A to-do list, a blog, a portfolio, a note-taking app. The only way to learn is to build.

2. **Break it.** Then fix it. You'll learn more from fixing a broken app than from building one that works perfectly the first time.

3. **Share it.** Deploy it. Show someone. Getting feedback (even "this is cool!") keeps you motivated.

4. **Repeat.** Build another thing. Slightly harder this time. And again. And again.

### Remember

- Every expert was once a beginner who didn't give up
- You don't need to know everything — you just need to know enough to build the next thing
- Google is your best friend. Even senior developers Google things every day
- The best code is code that works. Not clever code. Working code.
- Taking breaks is productive. If you're stuck, walk away, then come back
- Imposter syndrome is real. You belong here.

**Welcome to web development. You're a full stack developer now.**

---

## 19. Desktop Apps with Electron — Take Your Web Skills Beyond the Browser

### What is Electron?

Electron lets you build **desktop apps** (Windows, Mac, Linux) using HTML, CSS, and JavaScript. If you can build a website, you can build a desktop app.

Apps built with Electron: VS Code, Slack, Discord, Figma, Notion, Spotify Desktop, WhatsApp Desktop, Signal, Trello desktop, and many more.

**The magic:** Electron bundles a Chromium browser (your frontend runs in it) and Node.js (your backend runs in it) into a single `.exe` / `.dmg` / `.AppImage` file.

### Architecture

```
┌─────────────────────────────────────┐
│           Electron App              │
│  ┌──────────────┐  ┌──────────────┐ │
│  │ Main Process  │  │ Renderer     │ │
│  │ (Node.js)     │●─┤ Process      │ │
│  │ - File system │  │ (Chromium)   │ │
│  │ - OS APIs     │  │ - HTML/CSS   │ │
│  │ - Menus       │  │ - JS         │ │
│  │ - Tray icon   │  │ - React etc. │ │
│  └──────┬───────┘  └──────┬───────┘ │
│         └────────┬────────┘          │
│            IPC (Inter-Process        │
│            Communication)            │
└─────────────────────────────────────┘
```

- **Main process:** One Node.js process that manages windows, menus, the system tray, and native APIs
- **Renderer process:** One per window — each is essentially a Chromium tab running your web app
- **IPC:** They communicate via `ipcMain` (main) and `ipcRenderer` (renderer)

### Your First Electron App

#### Setup

```bash
mkdir my-desktop-app
cd my-desktop-app
npm init -y
npm install electron --save-dev
```

#### main.js (Main Process)

Create `main.js` in your project root:

```javascript
const { app, BrowserWindow } = require('electron');

function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false
    }
  });

  win.loadFile('index.html');
}

app.whenReady().then(createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit();
});

app.on('activate', () => {
  if (BrowserWindow.getAllWindows().length === 0) createWindow();
});
```

#### index.html (Renderer Process)

Create `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>My Desktop App</title>
  <style>
    body {
      font-family: -apple-system, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background: #1a1a1a;
      color: white;
    }
  </style>
</head>
<body>
  <h1>Hello from Electron! 🖥️</h1>
</body>
</html>
```

#### package.json

Add a start script:

```json
"scripts": {
  "start": "electron ."
}
```

#### Run it

```bash
npm start
```

A native desktop window appears with your HTML. It has a real menu bar, can be minimized/maximized, and lives in your taskbar. You just built a desktop app.

### IPC — Main ↔ Renderer Communication

The main process can do things the renderer can't (read files, access OS, show native dialogs). To do those things, the renderer sends a message via IPC:

**main.js:**
```javascript
const { ipcMain, dialog } = require('electron');

ipcMain.handle('pick-file', async () => {
  const result = await dialog.showOpenDialog({ properties: ['openFile'] });
  return result.filePaths[0];
});
```

**renderer.js (in your HTML):**
```javascript
const { ipcRenderer } = require('electron');

document.getElementById('pick-btn').addEventListener('click', async () => {
  const filePath = await ipcRenderer.invoke('pick-file');
  console.log('User picked:', filePath);
});
```

### Common Electron APIs

| API | What it does |
|---|---|
| `dialog.showOpenDialog()` | Native file picker |
| `dialog.showSaveDialog()` | Native save dialog |
| `Notification(title, body)` | OS notification |
| `clipboard.writeText(text)` | System clipboard |
| `shell.openExternal(url)` | Open URL in default browser |
| `Tray` | System tray icon |
| `Menu` | Custom application menu |
| `nativeImage` | Work with icons/images natively |

### Converting a Web App to Desktop

Take the **Calculator** from Project 2 and turn it into a desktop app:

1. Copy `calculator.html`, `calc-style.css`, `calc.js` into a new folder
2. Add `package.json` and `main.js` (pointing to `calculator.html`)
3. Run `npm install electron --save-dev`
4. Run `npm start`

That's it. Your web calculator is now a native Mac/Windows/Linux app.

### Tips for Electron Development

- **DevTools are built-in** — `Cmd+Shift+I` / `Ctrl+Shift+I` opens Chrome DevTools in your app window
- **Hot reload** — Use `npx electron-reload` or `nodemon` to auto-reload on file changes
- **Security:** For production, enable `contextIsolation: true` and use `preload.js` scripts instead of `nodeIntegration: true`
- **Large apps:** Consider `electron-forge` or `electron-builder` for packaging/distribution
- **Performance:** Each window is a full Chromium process — be mindful of memory usage

### Your Turn

Convert any project from this guide into a desktop app:
1. Take the Weather App — add a native notification when the weather loads
2. Take the Notes App — use `dialog.showSaveDialog()` to export notes as `.txt` files
3. Take the URL Shortener — add a system tray icon with quick-access menu

### Packaging for Distribution

```bash
npm install --save-dev @electron-forge/cli
npx electron-forge import
npm run make
```

This creates an installer in the `out/` folder. You can share it with anyone — they don't need Node.js or npm installed.

### Why Electron Matters

- **One codebase** for web + Windows + Mac + Linux
- **Your existing skills** transfer directly (HTML/CSS/JS/React)
- **Access to native APIs** (file system, notifications, system tray, menus)
- **Huge community** — most common issues are solved

**You are now not just a web developer, but a desktop application developer. Same skills, bigger canvas.**

---

## Ready for More? → AdvanceFSWD Guide

You just finished the beginner journey. There's a second guide that picks up where this one ends:

📘 **`advanceFSWDguide.md`** (in the same folder) — 27 chapters covering:

| Topic | What You'll Learn |
|---|---|---|
| **TypeScript** | Static types, interfaces, generics, tsconfig |
| **Next.js** | File-based routing, SSR, SSG, API routes |
| **Tailwind CSS** | Utility-first styling, responsive design system |
| **Auth in Depth** | JWT, OAuth, sessions, Supabase Auth, security |
| **Testing** | Unit, integration, E2E with Jest/Vitest + Playwright |
| **Web Security** | XSS, CSRF, SQL injection, HTTPS, CSP, Helmet |
| **Performance** | Core Web Vitals, lazy loading, code splitting, caching |
| **CI/CD** | GitHub Actions for automated testing + deployment |
| **Docker** | Containers, Dockerfiles, Docker Compose |
| **WebSockets** | Real-time bidirectional communication (Socket.IO) |
| **State Management** | Redux, Zustand, Context API patterns |
| **GraphQL** | Queries, mutations, Apollo Client + Server |
| **AWS / PlanetScale** | Cloud databases for production PostgreSQL |
| **Linux Basics** | SSH, file system, process management |
| **Monorepos** | Turborepo, Nx, shared packages |
| **Microservices** | Architecture patterns, communication, message queues |
| **Serverless** | Functions, edge compute, cold starts, vendors |
| **Web Components** | Custom elements, shadow DOM, slots |
| **Accessibility** | ARIA, keyboard nav, screen readers, a11y tree |
| **SEO** | Meta tags, structured data, sitemaps, Open Graph |
| **Package Managers** | npm vs yarn vs pnpm, workspaces |
| **Responsive Deep Dive** | Container queries, clamp(), logical properties |
| **Error Tracking** | Sentry, logging, health endpoints, alerting, observability |
| **i18n** | Translations, plural rules, RTL, date/number formatting |
| **Background Jobs** | Bull, Redis queues, retries, cron scheduling |
| **Feature Flags** | LaunchDarkly, canary releases, A/B testing, kill switches |
| **Mobile Strategies** | PWA, React Native, Flutter, Native — when to choose what |

> **Prerequisite:** You just completed this guide — you're ready.

---

*"The best time to plant a tree was 20 years ago. The second best time is now."*

*Start building.*


