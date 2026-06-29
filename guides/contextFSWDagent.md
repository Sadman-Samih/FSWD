# FSWD Guide — Context for AI Agents

## File Location
`D:\MD\CODE\Coding Guides\Guide Full Stack Web Development.md`

## Purpose
A comprehensive beginner's guide to full stack web development (HTML, CSS, JavaScript, Node.js/Express, SQL/SQLite, Git, deployment). Written for absolute beginners with zero assumed knowledge. Conversational, analogy-heavy style with "Your Turn" exercises.

## Length
~180KB, ~19 chapters

## Content Breakdown

| Chapter | Topics | Key Sections |
|---|---|---|
| 1 | What is full stack? | Frontend vs backend analogy (restaurant), what you'll build |
| 2 | How the web works | DNS, client-server model, HTTP status codes, URL anatomy |
| 3 | Setting up tools | VS Code, Live Server, Node.js/npm, Git, terminal basics |
| 4 | HTML | All common tags, attributes, IDs vs classes, forms, semantic tags, mini-project: recipe page |
| 5 | CSS | Selectors, cascade, colors, units, **box model (critical)**, flexbox, grid, responsive design, media queries, common patterns (centering, cards, sticky header, hero), mini-project: style recipe page |
| 6 | JavaScript | Variables, data types, operators, conditionals, loops, functions, arrays (map/filter/find/reduce), objects, **DOM manipulation**, **events & event delegation**, **async/await & fetch**, error handling, mini-project: to-do list |
| 7 | Backend | What is a server, Node.js, Express routing, request-response cycle, middleware, environment variables, serving static files |
| 8 | Databases | SQL vs NoSQL, SQL syntax (CREATE TABLE, CRUD), relationships (JOINs), **connecting Express to SQLite with better-sqlite3** |
| 9 | Full Stack Project | **Complete Notes App** with: database.js, server.js (full CRUD API), index.html, style.css (gradient UI), app.js (fetch/async/error handling). Runnable end-to-end. |
| 10 | APIs | REST principles, fetch API (GET/POST/PUT/DELETE), CORS |
| 11 | Deploying | Vercel (frontend), Render (backend), Railway, custom domains, connecting deployed frontend to backend |
| 12 | Git & GitHub | init, add, commit, push, branches, merge, .gitignore, daily workflow |
| 13 | Learning Roadmap | **12-week plan** (Month 1: HTML/CSS/JS, Month 2: Backend/Project, Month 3: React/Auth/TypeScript) |
| 14 | Intro to React | Components, JSX, props, useState, useEffect, virtual DOM, conditional rendering, lists with .map(), creating a React app (Vite/CRA), mini-project: convert portfolio to React. Written for vanilla JS developers transitioning to React. |
| 15 | The Complete Reference | Cheat sheets for HTML, CSS, JavaScript, Express |
| 16 | Troubleshooting | 12 common errors with fixes, debugger's checklist |
| 17 | Glossary | Plain English dictionary of 30+ web dev terms (API, CORS, DNS, JSON, REST, SQL, etc.) with "See Also" chapter references |
| 18 | Practice Projects | 5 projects with descriptions, hints, test cases, and **folder structures**. Portfolio (HTML/CSS), Calculator (JS DOM), Weather App (API + fetch), Blog with Comments (full stack + relationships), URL Shortener (redirects + clipboard API). Step-by-step walkthroughs with "try yourself first" approach. Solutions available in `solutions/` folder. |
| 19 | Desktop Apps (Electron) | What is Electron, architecture (main/renderer/IPC), first app walkthrough, common APIs, converting web apps to desktop, packaging with electron-forge, distribution. |

## Teaching Style
- Conversational, encouraging tone ("Hey, you. Let's build things.")
- Real-world analogies (restaurant = frontend/backend, house = structure/style/behavior, waiter = API)
- ASCII diagrams for visual concepts
- "Your Turn" exercises after each major section
- "Pro tip" callouts throughout
- Mini-projects: profile page, recipe page, to-do list, notes app

## Tech Stack Used in Guide
- **Frontend:** Vanilla HTML5, CSS3 (Flexbox, Grid, responsive), Vanilla JavaScript (ES6+)
- **Backend:** Node.js, Express.js
- **Database:** SQLite (via better-sqlite3)
- **Tools:** VS Code, Live Server, Git, npm
- **Deployment:** Vercel (frontend), Render/Railway (backend)

## When to Reference This Guide
- User asks about web development fundamentals
- User is a beginner who needs HTML/CSS/JS explained
- User needs backend (Node.js/Express) or database (SQL/SQLite) help
- User wants to build a full stack project
- User needs deployment or Git guidance
- User is debugging common web dev errors

## Related Files
- `D:\MD\CODE\Coding Guides\Attendance Tracker guide.md` — No-login attendance app (reference for a complete working project)
- `D:\CODING\Projects\2026\Attendees\` — Live production of the attendance app
- `D:\MD\CODE\Coding Guides\Full Stack Web Development - HTML Cheat Sheet and Poster.md` — Printable one-page reference for HTML, CSS, JS, Express, SQL, Git
- `D:\MD\CODE\Coding Guides\solutions\` — Complete solution code for all 5 Practice Projects (check only when stuck)
- `D:\MD\CODE\Coding Guides\advanceFSWDguide.md` — Advanced continuation guide (TypeScript, Next.js, Tailwind, Testing, Docker, etc.)
- `D:\MD\CODE\Coding Guides\contextAdvanceFSWDagent.md` — Agent context for the advanced guide

## Structure Convention
- Chapters use `##` headings
- Sub-sections use `###` headings
- Code blocks specify language (```html, ```css, ```javascript, ```sql, ```bash)
- Tables used for comparisons and references
- "Your Turn" sections are call-to-action exercises

## Agent Usage
When helping a user with web development:
1. Check if the relevant topic is covered in this guide
2. Reference the guide's explanation style (analogies, examples)
3. For code examples, follow the guide's patterns (ES6+ JS, Express structure, SQLite queries)
4. Direct the user to the relevant chapter for deeper reading
