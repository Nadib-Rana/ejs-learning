### Styling in EJS

Styling in EJS works similarly to how you would style a regular HTML file, but with the added flexibility of dynamic data and templating. You can use external CSS files, inline styles, or even style directly within the EJS template.

Here’s a guide on how to add styles to your EJS-based website.

---

### **1. Using External CSS**

You can link external CSS files to your EJS templates just like you would in regular HTML. It's a good practice to keep your CSS in a separate file to make it easier to manage and maintain.

#### Example:

1. **Create a CSS file** (e.g., `styles.css`) inside a `public` directory.

```css
/* public/styles.css */
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 0;
}

header {
  background-color: #333;
  color: white;
  padding: 20px;
  text-align: center;
}

footer {
  background-color: #333;
  color: white;
  padding: 10px;
  text-align: center;
}
```

2. **Link the CSS file** in your EJS layout (`layout.ejs`).

```html
<!-- views/layout.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title><%= title %></title>
  <link rel="stylesheet" href="/styles.css"> <!-- Linking external CSS -->
</head>
<body>
  <%- body %> <!-- This is where the page-specific content will go -->
</body>
</html>
```

3. **Serve the CSS file** from your Express server.

```javascript
// server.js
const express = require('express');
const app = express();

// Serve static files (CSS, images, etc.) from the "public" folder
app.use(express.static('public'));

// Your other routes here...
```

Now, when you navigate to any route in your app, the `styles.css` file will be applied to your EJS templates.

---

### **2. Inline Styles in EJS**

You can add styles directly inside your EJS template using the `<style>` tag. This is useful for small, page-specific styling.

#### Example:

```html
<!-- views/index.ejs -->
<%- include('partials/header') %>
<h2>Home Page</h2>
<p>Welcome to the home page!</p>

<style>
  h2 {
    color: #2d87f0;
  }
  p {
    font-size: 18px;
  }
</style>

<%- include('partials/footer') %>
```

This will apply styles only to the specific page (`index.ejs` in this case).

---

### **3. Dynamic Styles with EJS Variables**

You can also use EJS variables to dynamically inject styles into your templates. For example, you can pass a color or a font size from the server to change the appearance of the page based on user data or preferences.

#### Example:

1. **Pass Dynamic Style Data from the Server**:

```javascript
// server.js
app.get('/', (req, res) => {
  res.render('index', {
    title: 'Dynamic Styles',
    color: '#ff5733', // Passing dynamic color data
  });
});
```

2. **Use the Data in the EJS Template**:

```html
<!-- views/index.ejs -->
<%- include('partials/header') %>
<h2>Dynamic Styles Page</h2>
<p>This page has dynamic styles based on the server data.</p>

<style>
  h2 {
    color: <%= color %>; /* Injecting dynamic color */
  }
</style>

<%- include('partials/footer') %>
```

In this example, the color of the `<h2>` element is set dynamically based on the `color` variable passed from the server.

---

### **4. Styling with CSS Frameworks**

You can also use popular CSS frameworks like **Bootstrap**, **Tailwind CSS**, or **Bulma** in your EJS templates.

#### Example with Bootstrap:

1. **Include the Bootstrap CDN** in your layout:

```html
<!-- views/layout.ejs -->
<head>
  <meta charset="UTF-8">
  <title><%= title %></title>
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"> <!-- Bootstrap -->
</head>
```

2. **Use Bootstrap classes** in your EJS templates:

```html
<!-- views/index.ejs -->
<%- include('partials/header') %>

<div class="container">
  <h2 class="text-center">Home Page</h2>
  <p class="lead">Welcome to the home page, styled with Bootstrap!</p>
</div>

<%- include('partials/footer') %>
```

Now your app will have Bootstrap styles applied to it.

---

### **Summary**

1. **External CSS**: Keep your styles in separate files for easier maintenance. Serve these files using Express.
2. **Inline Styles**: Add styles directly to a specific EJS template for custom styling.
3. **Dynamic Styling**: Inject dynamic style data into your templates using EJS variables.
4. **CSS Frameworks**: Easily integrate CSS frameworks like Bootstrap or Tailwind CSS for ready-to-use, responsive styles.

By using these techniques, you can effectively style your EJS templates and make your web app visually appealing and responsive.
