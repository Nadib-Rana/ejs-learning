### Layout in EJS

Using **layout** in EJS helps in managing the design of a web application more effectively by making parts of the page reusable (such as the header, footer, etc.). This allows you to have a consistent structure across multiple pages, without duplicating the same code in every single page.

---

### **How to Use Layout in EJS**

In EJS, you generally use **partials** (such as headers, footers) to break down the common parts of the layout. These partials can then be included in various pages to maintain consistency.

---

### **1. Create a Layout Template**

First, create a **layout.ejs** file where you will define the common parts of your page, such as the header and footer.

```html
<!-- views/layout.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title><%= title %></title>
</head>
<body>
  <header>
    <h1>My Website</h1>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  </header>

  <!-- This will include page-specific content -->
  <div>
    <%- body %>
  </div>

  <footer>
    <p>&copy; 2024 My Website</p>
  </footer>
</body>
</html>
```

- Here, `<%- body %>` is the placeholder where the specific content for each page will be injected.

---

### **2. Using Partials**

If you want to reuse parts like the header, footer, etc., you can create **partials** for them.

#### Header.partial.ejs
```html
<!-- views/partials/header.ejs -->
<header>
  <h1>My Website</h1>
  <nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
  </nav>
</header>
```

#### Footer.partial.ejs
```html
<!-- views/partials/footer.ejs -->
<footer>
  <p>&copy; 2024 My Website</p>
</footer>
```

These partials can be included across various pages.

---

### **3. Using Layout Engine (Express-ejs-layouts)**

EJS does not integrate directly with a layout engine, but you can use **express-ejs-layouts** to simplify layout usage.

#### Install `express-ejs-layouts`:

1. First, install `express-ejs-layouts`:
   ```bash
   npm install express-ejs-layouts
   ```

2. Then, use it in your **Express.js** server:

```javascript
// server.js
const express = require('express');
const ejsLayouts = require('express-ejs-layouts');
const app = express();

// Use layouts middleware
app.use(ejsLayouts);

// Set EJS as the view engine
app.set('view engine', 'ejs');

// Set default layout
app.set('layout', 'layout');  // layout.ejs will be used as the layout

// Create Routes
app.get('/', (req, res) => {
  res.render('index', { title: 'Home Page', body: 'This is the home page content.' });
});

app.get('/about', (req, res) => {
  res.render('about', { title: 'About Us', body: 'This is the about us page content.' });
});

app.listen(3000, () => {
  console.log('Server running at http://localhost:3000');
});
```

---

### **4. Rendering Layout and Partials**

When you render a page, the **layout** and **partials** will automatically be included.

```html
<!-- views/index.ejs -->
<%- include('partials/header') %>
<h2>Home Page</h2>
<p><%= body %></p>
<%- include('partials/footer') %>
```

Here, the `header` and `footer` partials will automatically be included into your page.

---

### **Summary**

1. **Layouts** help you manage common parts of your site (like the header and footer) in one place.
2. **Partials** allow you to reuse components like headers, footers, etc., across multiple pages.
3. Use **express-ejs-layouts** to manage your layout structure easily.

By using layouts in EJS, you can make your website structure more modular, reusable, and maintainable.
