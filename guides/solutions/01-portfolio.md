# Project 1: Personal Portfolio Site — Solution

## File Structure

```
portfolio/
├── index.html
└── style.css
```

## index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Your Name — Portfolio</title>
  <link rel="stylesheet" href="style.css">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
</head>
<body>

  <!-- Navigation -->
  <nav class="nav">
    <div class="nav-inner">
      <a href="#" class="logo">YourName</a>
      <ul class="nav-links">
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
  </nav>

  <!-- Hero -->
  <section class="hero">
    <div class="hero-content">
      <h1>Hi, I'm <span class="highlight">Your Name</span></h1>
      <p class="tagline">I build things for the web. I'm a full stack developer in training.</p>
      <a href="#projects" class="btn">See My Work</a>
    </div>
  </section>

  <!-- About -->
  <section id="about" class="section">
    <div class="container">
      <h2>About Me</h2>
      <div class="about-content">
        <img src="https://placekitten.com/300/300" alt="Your photo" class="about-img">
        <div class="about-text">
          <p>Hi! I'm learning web development and building cool things along the way. I love turning ideas into code and making things that people can actually use.</p>
          <p>When I'm not coding, you'll find me exploring new technologies, reading about design, or working on side projects.</p>
          <div class="skills">
            <span class="skill-tag">HTML</span>
            <span class="skill-tag">CSS</span>
            <span class="skill-tag">JavaScript</span>
            <span class="skill-tag">Node.js</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Projects -->
  <section id="projects" class="section bg-light">
    <div class="container">
      <h2>Projects</h2>
      <div class="project-grid">
        <div class="project-card">
          <div class="project-img" style="background:#667eea;"></div>
          <div class="project-info">
            <h3>Project One</h3>
            <p>A short description of what this project does and what you learned building it.</p>
            <div class="project-links">
              <a href="#" class="btn-small">Live Demo</a>
              <a href="#" class="btn-small btn-outline">GitHub</a>
            </div>
          </div>
        </div>

        <div class="project-card">
          <div class="project-img" style="background:#764ba2;"></div>
          <div class="project-info">
            <h3>Project Two</h3>
            <p>A short description of what this project does and what you learned building it.</p>
            <div class="project-links">
              <a href="#" class="btn-small">Live Demo</a>
              <a href="#" class="btn-small btn-outline">GitHub</a>
            </div>
          </div>
        </div>

        <div class="project-card">
          <div class="project-img" style="background:#38a169;"></div>
          <div class="project-info">
            <h3>Project Three</h3>
            <p>A short description of what this project does and what you learned building it.</p>
            <div class="project-links">
              <a href="#" class="btn-small">Live Demo</a>
              <a href="#" class="btn-small btn-outline">GitHub</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Contact -->
  <section id="contact" class="section">
    <div class="container">
      <h2>Get In Touch</h2>
      <p class="contact-text">I'm always open to new projects, collaborations, or just a chat.</p>
      <a href="mailto:your@email.com" class="btn">your@email.com</a>
    </div>
  </section>

  <!-- Footer -->
  <footer class="footer">
    <p>&copy; 2026 Your Name. Built from scratch with HTML & CSS.</p>
  </footer>

</body>
</html>
```

## style.css

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Inter', -apple-system, sans-serif;
  color: #1a1a1a;
  line-height: 1.6;
}

/* ── Navigation ── */

.nav {
  position: fixed;
  top: 0;
  width: 100%;
  background: white;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  z-index: 100;
}

.nav-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 15px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-weight: 700;
  font-size: 1.3rem;
  color: #667eea;
  text-decoration: none;
}

.nav-links {
  list-style: none;
  display: flex;
  gap: 30px;
}

.nav-links a {
  text-decoration: none;
  color: #555;
  font-weight: 500;
  transition: color 0.2s;
}

.nav-links a:hover {
  color: #667eea;
}

/* ── Hero ── */

.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.hero-content h1 {
  font-size: 3rem;
  margin-bottom: 15px;
}

.highlight {
  text-decoration: underline;
  text-decoration-color: rgba(255,255,255,0.4);
  text-underline-offset: 8px;
}

.tagline {
  font-size: 1.2rem;
  opacity: 0.9;
  margin-bottom: 30px;
}

.btn {
  display: inline-block;
  padding: 14px 32px;
  background: white;
  color: #667eea;
  text-decoration: none;
  font-weight: 600;
  border-radius: 8px;
  transition: all 0.2s;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0,0,0,0.2);
}

/* ── Sections ── */

.section {
  padding: 80px 20px;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
}

.section h2 {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 50px;
  color: #333;
  position: relative;
}

.section h2::after {
  content: '';
  display: block;
  width: 60px;
  height: 3px;
  background: #667eea;
  margin: 12px auto 0;
  border-radius: 2px;
}

.bg-light {
  background: #f8f9fa;
}

/* ── About ── */

.about-content {
  display: flex;
  gap: 50px;
  align-items: center;
}

.about-img {
  width: 250px;
  height: 250px;
  border-radius: 50%;
  object-fit: cover;
  box-shadow: 0 4px 20px rgba(0,0,0,0.15);
}

.about-text p {
  margin-bottom: 15px;
  color: #555;
  font-size: 1.05rem;
}

.skills {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 20px;
}

.skill-tag {
  padding: 6px 16px;
  background: #667eea;
  color: white;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 500;
}

/* ── Projects ── */

.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}

.project-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 15px rgba(0,0,0,0.08);
  transition: all 0.3s;
}

.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 30px rgba(0,0,0,0.15);
}

.project-img {
  height: 200px;
}

.project-info {
  padding: 20px;
}

.project-info h3 {
  margin-bottom: 10px;
  color: #333;
}

.project-info p {
  color: #666;
  font-size: 0.95rem;
  margin-bottom: 20px;
}

.project-links {
  display: flex;
  gap: 10px;
}

.btn-small {
  padding: 8px 20px;
  background: #667eea;
  color: white;
  text-decoration: none;
  border-radius: 6px;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.2s;
}

.btn-small:hover {
  background: #5a6fd6;
}

.btn-outline {
  background: transparent;
  border: 2px solid #667eea;
  color: #667eea;
}

.btn-outline:hover {
  background: #667eea;
  color: white;
}

/* ── Contact ── */

.contact-text {
  text-align: center;
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 30px;
}

/* ── Footer ── */

.footer {
  text-align: center;
  padding: 30px;
  background: #1a1a1a;
  color: #888;
  font-size: 0.9rem;
}

/* ── Responsive ── */

@media (max-width: 768px) {
  .hero-content h1 {
    font-size: 2rem;
  }

  .nav-links {
    gap: 15px;
  }

  .about-content {
    flex-direction: column;
    text-align: center;
  }

  .about-img {
    width: 180px;
    height: 180px;
  }

  .skills {
    justify-content: center;
  }

  .project-grid {
    grid-template-columns: 1fr;
  }
}
```


