# ejs-learning

---

# 📘 EJS Guide for Node.js

---

## 📝 Table of Contents

1. [📖 Introduction to EJS](#-introduction-to-ejs)
2. [📊 Passing Data to EJS](#-passing-data-to-ejs)
3. [🔀 If-Else Statements in EJS](#-if-else-statements-in-ejs)
4. [🔄 Loop in EJS](#-loop-in-ejs)
5. [🖼️ Layout in EJS](#-layout-in-ejs)
6. [🎨 Styling](#-styling)

---

## 📖 Introduction to EJS

EJS is a simple templating language that enables embedding JavaScript in HTML. It’s often used with **Express.js** in **Node.js** applications to dynamically render pages.

---

## 📊 Passing Data to EJS

EJS allows you to pass data from your server to your views, making it easy to create dynamic content.

### Example:

```javascript
// server.js
app.get('/profile', (req, res) => {
  res.render('profile', { title: 'User Profile', username: 'Nadib' });
});
```

In your EJS file:

```html
<!-- profile.ejs -->
<h1><%= title %></h1>
<p>Welcome, <%= username %>!</p>
```

---

## 🔀 If-Else Statements in EJS

Use conditional statements to render different content based on data.

### Example:

```html
<% if (loggedIn) { %>
  <p>Welcome back, <%= username %>!</p>
<% } else { %>
  <p>Please log in to access your profile.</p>
<% } %>
```

---

## 🔄 Loop in EJS

EJS supports looping, allowing you to iterate over arrays and display lists of items.

### Example:

```javascript
// server.js
app.get('/items', (req, res) => {
  res.render('items', { items: ['Apple', 'Banana', 'Cherry'] });
});
```

In your EJS file:

```html
<ul>
  <% items.forEach(item => { %>
    <li><%= item %></li>
  <% }) %>
</ul>
```

---

## 🖼️ Layout in EJS

Layouts help maintain a consistent structure across multiple pages. You can define a main layout file and include it across views.

### Example:

Install `express-ejs-layouts`:

```bash
npm install express-ejs-layouts
```

In `app.js`:

```javascript
const expressLayouts = require('express-ejs-layouts');
app.use(expressLayouts);
app.set('layout', 'layouts/main');  // main layout file
```

Define your layout in `layouts/main.ejs`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title><%= title %></title>
</head>
<body>
  <%- body %>
</body>
</html>
```

---

## 🎨 Styling

Enhance your EJS pages with CSS for styling. Add custom styling to make pages visually appealing and match your brand.

---

## 🔗 Resources

- [EJS Documentation](https://ejs.co/)
- [Express.js Guide](https://expressjs.com/)
- [Node.js Official Site](https://nodejs.org/)

--- 

