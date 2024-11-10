Passing data to **EJS** involves sending dynamic information from your **Node.js** server to an **EJS template** to render personalized content. Here’s a step-by-step guide.

---

### Step 1: Setting Up the Server to Pass Data

In your Node.js file (e.g., `server.js`), set up a route and send data to the EJS template using `res.render()`.

```javascript
// server.js
const express = require('express');
const app = express();

// Set EJS as the templating engine
app.set('view engine', 'ejs');

// Route to render an EJS template and pass data
app.get('/', (req, res) => {
  const data = {
    name: 'Nadib',
    age: 25,
    hobbies: ['Coding', 'Reading', 'Gaming']
  };
  res.render('profile', data); // Render profile.ejs with the data object
});

// Start the server
app.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

- Here, an object `data` is created with `name`, `age`, and `hobbies` and passed to the EJS template named `profile.ejs`.

---

### Step 2: Accessing Data in the EJS Template

In your `views` folder, create an `EJS` file (e.g., `profile.ejs`) to receive and display the data.

```html
<!-- profile.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>User Profile</title>
</head>
<body>
  <h1>স্বাগতম, <%= name %>!</h1>
  <p>আপনার বয়স: <%= age %></p>

  <h2>আপনার শখ:</h2>
  <ul>
    <% hobbies.forEach(hobby => { %>
      <li><%= hobby %></li>
    <% }); %>
  </ul>
</body>
</html>
```

- **Explanation**:
  - `<%= name %>`: Displays the user’s name (e.g., "Nadib").
  - `<%= age %>`: Displays the age (e.g., 25).
  - `<% hobbies.forEach(hobby => { %> ... <% }); %>`: Loops through the `hobbies` array and displays each hobby in an `<li>` element.

---

### Summary of Steps

1. **Define data** in your Node.js server route.
2. **Pass the data** to `res.render()` when rendering the EJS template.
3. **Access data** in the EJS template using `<%= %>` for variables and `<% %>` for JavaScript control structures.

---

This method allows you to display personalized, dynamic content on your pages by passing data from Node.js to EJS.
