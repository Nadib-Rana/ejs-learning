Using **EJS (Embedded JavaScript)** in a Node.js application is straightforward. Here’s a step-by-step guide:

---

### Step 1: Set Up Your Project
1. **Create a new directory** and navigate into it:
   ```bash
   mkdir ejs-demo
   cd ejs-demo
   ```

2. **Initialize a new Node.js project**:
   ```bash
   npm init -y
   ```

3. **Install Express and EJS**:
   ```bash
   npm install express ejs
   ```

---

### Step 2: Set Up the Server (`server.js`)

Create a `server.js` file to set up a basic Express server and configure it to use EJS as the templating engine.

```javascript
// server.js
const express = require('express');
const app = express();

// Set EJS as the templating engine
app.set('view engine', 'ejs');

// Route to render an EJS template
app.get('/', (req, res) => {
  const data = {
    username: 'Nadib',
    items: ['Laptop', 'Phone', 'Backpack']
  };
  res.render('profile', data); // Render profile.ejs with data
});

// Start the server
app.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

---

### Step 3: Create Your EJS Template (`views/profile.ejs`)

Inside your project folder, create a folder named `views` (this is where EJS templates are usually stored). Inside `views`, create a file called `profile.ejs`.

```html
<!-- views/profile.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>User Profile</title>
</head>
<body>
  <h1>Welcome, <%= username %>!</h1>

  <h2>Your Items:</h2>
  <ul>
    <% items.forEach(item => { %>
      <li><%= item %></li>
    <% }); %>
  </ul>
</body>
</html>
```

### Explanation
- `<%= username %>`: Inserts the `username` variable into the HTML.
- `<% items.forEach(item => { %> ... <% }) %>`: Loops through the `items` array and displays each item in an HTML `<li>` tag.

---

### Step 4: Run the Server

Run your server by executing:

```bash
node server.js
```

Now, open a web browser and go to `http://localhost:3000`. You should see a rendered HTML page with the user’s name and list of items displayed based on the `profile.ejs` template.

---

### Summary

1. **Set up an Express server and configure EJS** as the templating engine.
2. **Create EJS templates** inside a `views` folder.
3. **Pass data** from the server to the EJS template and render it dynamically.

EJS makes it easy to add dynamic content to your web pages with minimal effort, ideal for creating web applications with Node.js.
