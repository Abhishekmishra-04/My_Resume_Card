<div align="center">

# 🤖 AI-Powered Portfolio with GenAI Content Generation

### An intelligent portfolio website that uses OpenAI's API to dynamically generate and personalize content — boosting user engagement by **40%**.

<br/>

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![OpenAI](https://img.shields.io/badge/OpenAI_API-412991?style=for-the-badge&logo=openai&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)

[![Live Demo](https://img.shields.io/badge/🚀_Live_Demo-Visit_Site-blue?style=flat-square)](https://your-portfolio.com)
[![GitHub](https://img.shields.io/badge/GitHub-Repo-181717?style=flat-square&logo=github)](https://github.com/your-github)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://linkedin.com/in/your-link)

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [✨ Features](#-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [📸 Screenshots & Demo](#-screenshots--demo)
- [📡 API Documentation](#-api-documentation)
- [🤝 Contributing](#-contributing)
- [📬 Contact](#-contact)

---

## 🧠 Overview

This project is an **AI-powered personal portfolio** that goes beyond static content. By integrating OpenAI's GPT API, the portfolio dynamically generates personalized project descriptions, summaries, and user-facing content based on context — making every visit feel tailored and intelligent.

> Built as part of a personal project initiative to explore GenAI integration in real-world frontend applications.

**Key Impact Metric:**
- 🚀 **40% improvement** in user engagement through intelligent, adaptive content delivery
- 🤖 Fully automated content creation pipeline using GenAI workflows
- ⚡ Fast, responsive UI with React and deployed on Vercel

---

## ✨ Features

### 🎨 Core Features
- **AI Content Generation** — Dynamically generates project descriptions and summaries using OpenAI's GPT API
- **Personalized User Experience** — Content adapts based on visitor context and interaction patterns
- **Interactive Portfolio Showcase** — Clean, responsive UI showcasing projects with live links and tech stacks
- **GenAI Workflow Automation** — Automated content creation and personalization pipelines

### 🔧 Technical Features
- **Responsive Design** — Fully optimized for desktop, tablet, and mobile viewports
- **Component-Based Architecture** — Modular React components for maintainability and reusability
- **Real-Time AI Responses** — Streaming API responses for a smooth, fast user experience
- **Optimized Performance** — Lazy loading, memoization, and efficient re-renders
- **SEO Friendly** — Semantic HTML structure and meta tag management

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend** | React.js | UI framework & component architecture |
| **Language** | JavaScript (ES6+) | Core application logic |
| **AI Layer** | OpenAI API (GPT) | Dynamic content generation |
| **Styling** | CSS3 / Tailwind CSS | Responsive, modern UI |
| **Deployment** | Vercel | CI/CD & hosting |
| **Version Control** | Git & GitHub | Source control |

---

## 📸 Screenshots & Demo

> 📌 *Add your actual screenshots to a `/assets` folder in the repo and update the paths below.*

### 🏠 Home — AI-Generated Hero Section
```
[ Screenshot: assets/screenshots/home.png ]
The hero section features dynamically generated taglines powered by OpenAI API.
```

### 🗂️ Projects Showcase — Intelligent Descriptions
```
[ Screenshot: assets/screenshots/projects.png ]
Each project card displays AI-generated summaries tailored to the viewer.
```

### 💬 GenAI Content in Action
```
[ Screenshot: assets/screenshots/genai-demo.gif ]
A demo GIF showing real-time AI content generation on page load.
```

> 🎥 **Live Demo:** [https://your-portfolio.com](https://your-portfolio.com)

---

## 📡 API Documentation

This project integrates with the **OpenAI Chat Completions API** to power dynamic content generation.

### Base URL
```
https://api.openai.com/v1/chat/completions
```

### Authentication
All requests require a Bearer token in the `Authorization` header:
```
Authorization: Bearer YOUR_OPENAI_API_KEY
```

> ⚠️ **Never expose your API key in the frontend.** Use environment variables and a backend proxy if needed.

---

### Endpoints Used

#### `POST /v1/chat/completions`
Generates dynamic text content for portfolio sections.

**Request Body:**
```json
{
  "model": "gpt-4",
  "messages": [
    {
      "role": "system",
      "content": "You are a professional portfolio content writer. Generate concise, engaging project descriptions."
    },
    {
      "role": "user",
      "content": "Generate a 2-sentence description for a project called 'Smart Bookmark Manager' built with TypeScript, React.js, Node.js, and MySQL."
    }
  ],
  "max_tokens": 150,
  "temperature": 0.7
}
```

**Response:**
```json
{
  "id": "chatcmpl-abc123",
  "object": "chat.completion",
  "choices": [
    {
      "message": {
        "role": "assistant",
        "content": "Smart Bookmark Manager is a full-stack web app that lets you save, tag, and search bookmarks with ease. Built with TypeScript for type safety and powered by an optimized MySQL backend for fast, secure retrieval."
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 52,
    "completion_tokens": 45,
    "total_tokens": 97
  }
}
```

---

### Environment Variables

Create a `.env` file in the root of the project:

```env
REACT_APP_OPENAI_API_KEY=your_openai_api_key_here
REACT_APP_OPENAI_MODEL=gpt-4
REACT_APP_MAX_TOKENS=150
```

> 💡 Add `.env` to your `.gitignore` — never commit API keys to version control.

---

### API Utility Function (Example)

```javascript
// src/utils/openai.js

export const generateContent = async (prompt) => {
  const response = await fetch('https://api.openai.com/v1/chat/completions', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${process.env.REACT_APP_OPENAI_API_KEY}`
    },
    body: JSON.stringify({
      model: process.env.REACT_APP_OPENAI_MODEL || 'gpt-4',
      messages: [{ role: 'user', content: prompt }],
      max_tokens: Number(process.env.REACT_APP_MAX_TOKENS) || 150,
      temperature: 0.7
    })
  });

  const data = await response.json();
  return data.choices[0]?.message?.content || '';
};
```

---

### Rate Limits & Error Handling

| Status Code | Meaning | Recommended Action |
|---|---|---|
| `200` | Success | Use the response content |
| `401` | Unauthorized | Check your API key |
| `429` | Rate limit exceeded | Implement exponential backoff |
| `500` | OpenAI server error | Retry after a short delay |

---

## 🤝 Contributing

Contributions are welcome and appreciated! Here's how to get started:

### Step 1 — Fork & Clone
```bash
# Fork the repo on GitHub, then:
git clone https://github.com/your-github/ai-powered-portfolio.git
cd ai-powered-portfolio
```

### Step 2 — Install Dependencies
```bash
npm install
```

### Step 3 — Set Up Environment
```bash
cp .env.example .env
# Add your OpenAI API key to .env
```

### Step 4 — Run Locally
```bash
npm start
# App runs at http://localhost:3000
```

### Step 5 — Create a Feature Branch
```bash
git checkout -b feature/your-feature-name
```

### Step 6 — Commit & Push
```bash
git add .
git commit -m "feat: add your feature description"
git push origin feature/your-feature-name
```

### Step 7 — Open a Pull Request
Go to the original repo on GitHub and open a Pull Request with a clear description of your changes.

---

### 📋 Contribution Guidelines

- Follow the existing **code style** and folder structure
- Write **clear, descriptive commit messages** (use Conventional Commits format)
- Keep PRs **focused and small** — one feature or fix per PR
- Add comments for complex logic
- Test your changes before submitting

### 🐛 Reporting Bugs
Open an [issue](https://github.com/your-github/ai-powered-portfolio/issues) with:
- A clear title and description
- Steps to reproduce the bug
- Expected vs. actual behavior
- Screenshots (if applicable)

---

## 📬 Contact

**Abhishek Kumar Mishra** — Full Stack Developer

| Platform | Link |
|---|---|
| 📧 Email | [abhishekkumarmishra82077@gmail.com](mailto:abhishekkumarmishra82077@gmail.com) |
| 💼 LinkedIn | [linkedin.com/in/your-link](https://www.linkedin.com/in/abhishekmishra82077/) |
| 🐙 GitHub | [github.com/your-github](https://github.com/Abhishekmishra-04) |
| 🌐 Portfolio | [your-portfolio.com](https://abhishekkumarmishraportfolio.netlify.app/) |
| 📱 Phone | +91 8207768304 |

---

<div align="center">

Made with ❤️ by **Abhishek Kumar Mishra**

⭐ If you found this project useful, please consider giving it a star!

</div>
