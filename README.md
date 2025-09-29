# Devops-class-activity
# Simple Blog Platform

A minimal full-stack blog application that allows you to view and add blog posts. The project consists of:

- A **static frontend** built with plain HTML and CSS for displaying blog posts.
- A **Node.js + Express backend** that provides a REST API for fetching and creating blog posts.
- An in-memory data store to keep the application simple and easy to run without database setup.

---

## Features

- Display a list of blog posts dynamically loaded from the backend.
- Add new posts via a REST API endpoint.
- Simple, clean UI with responsive-friendly design.
- Easy to set up and run locally.
- Ready for extension with a database or frontend framework.

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) installed on your machine.

### Installation

1. Clone the repository

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>/backend

###  Frontend (HTML/CSS)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Simple Blog</title>
  <style>
    /* Reset some default styles */
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f8f9fa;
      margin: 0;
      padding: 20px;
      color: #333;
    }

    header {
      text-align: center;
      margin-bottom: 40px;
    }

    header h1 {
      font-size: 2.5rem;
      margin: 0;
      color: #007bff;
    }

    .blog-post {
      background-color: #fff;
      border-radius: 8px;
      padding: 20px;
      margin-bottom: 20px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .blog-post h2 {
      margin-top: 0;
      color: #343a40;
    }

    .blog-post p {
      line-height: 1.6;
    }

    .blog-post .date {
      font-size: 0.9rem;
      color: #6c757d;
      margin-top: 10px;
    }

    footer {
      text-align: center;
      margin-top: 50px;
      color: #6c757d;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>

  <header>
    <h1>My Simple Blog</h1>
  </header>

  <section class="blog-post">
    <h2>Welcome to my blog!</h2>
    <p>This is the very first post. Here you can share your thoughts, ideas, or anything you'd like to write about.</p>
    <div class="date">Posted on September 29, 2025</div>
  </section>

  <section class="blog-post">
    <h2>Another Day, Another Post</h2>
    <p>Here's another example post. Feel free to customize and add more posts to your blog page!</p>
    <div class="date">Posted on September 28, 2025</div>
  </section>

  <footer>
    &copy; 2025 My Simple Blog. All rights reserved.
  </footer>

</body>
</html>

## Setup your backend project:
mkdir backend
cd backend
npm init -y
npm install express cors body-parser

## Backend(Node.js)
const express = require('express');
const cors = require('cors');
const bodyParser = require('body-parser');

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(bodyParser.json());

// In-memory "database"
let posts = [
  {
    id: 1,
    title: "Welcome to my blog!",
    content: "This is the very first post. Here you can share your thoughts, ideas, or anything you'd like to write about.",
    date: "September 29, 2025"
  },
  {
    id: 2,
    title: "Another Day, Another Post",
    content: "Here's another example post. Feel free to customize and add more posts to your blog page!",
    date: "September 28, 2025"
  }
];

// Get all posts
app.get('/api/posts', (req, res) => {
  res.json(posts);
});

// Add a new post
app.post('/api/posts', (req, res) => {
  const { title, content } = req.body;

  if (!title || !content) {
    return res.status(400).json({ error: "Title and content are required" });
  }

  const newPost = {
    id: posts.length + 1,
    title,
    content,
    date: new Date().toLocaleDateString("en-US", {
      year: "numeric",
      month: "long",
      day: "numeric"
    })
  };

  posts.unshift(newPost); // Add to beginning

  res.status(201).json(newPost);
});

// Start server
app.listen(PORT, () => {
  console.log(`Backend running on port ${PORT}`);
});

## How to run backend:
node index.js

## Future Improvements

Add persistent database storage (e.g., PostgreSQL, MongoDB).

Create a dynamic frontend with React or another framework.

Add user authentication and post management features.

Containerize the app using Docker for easy deployment.
