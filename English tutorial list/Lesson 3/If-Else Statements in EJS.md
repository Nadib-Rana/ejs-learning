### **If-Else Statements in EJS**

In **EJS (Embedded JavaScript)**, **if-else** statements allow you to conditionally display content based on certain criteria, similar to JavaScript. Here’s an example with explanations:

```html
<!-- example.ejs -->
<% if (userLoggedIn) { %>
  <h1>Welcome, <%= username %>!</h1>
<% } else { %>
  <h1>Guest, please log in</h1>
<% } %>
```

- **Explanation**:
  - `<% if (userLoggedIn) { %>`: This checks if `userLoggedIn` is true. If it is, a welcome message with the `username` is displayed.
  - `<% } else { %>`: If `userLoggedIn` is false, a message prompting the user to log in is displayed.

---

### **Example with Multiple Conditions**

You can add **else if** statements for more complex conditions, allowing different responses based on variable values:

```html
<!-- status.ejs -->
<% if (role === 'admin') { %>
  <h1>Welcome to the Admin Panel!</h1>
<% } else if (role === 'member') { %>
  <h1>Welcome, Member!</h1>
<% } else { %>
  <h1>Welcome, Guest!</h1>
<% } %>
```

- **Explanation**:
  - The `role` variable determines which greeting to display: one for admins, another for members, and a general greeting for guests.

---

### **Summary**

- **`<% if (condition) { %> ... <% } else { %>`**: Basic if-else for conditional content display.
- **`<% } else if (condition) { %>`**: Additional conditions as needed.

Using **if-else** in EJS allows you to easily add dynamic, conditional content to your views, making your web pages more interactive and personalized!
