### **Looping in EJS**

In **EJS (Embedded JavaScript)**, you can use JavaScript loops to display lists or repeat HTML elements. The **for** and **forEach** loops are commonly used to iterate through arrays or collections and display each item dynamically within the HTML.

---

### **Example of a forEach Loop**

Suppose you have an array of items that you want to display as a list. Here’s how to use a **forEach** loop in EJS:

```html
<!-- items.ejs -->
<h2>Your Items:</h2>
<ul>
  <% items.forEach(item => { %>
    <li><%= item %></li>
  <% }); %>
</ul>
```

- **Explanation**:
  - `<% items.forEach(item => { %>`: Begins a `forEach` loop through the `items` array.
  - `<%= item %>`: Displays each `item` in the array as an `<li>` element.
  - `<% }); %>`: Ends the loop.

---

### **Example of a for Loop**

A **for** loop can also be used in EJS for more control over iteration (e.g., displaying items based on a condition):

```html
<!-- numbers.ejs -->
<h2>Numbers List:</h2>
<ul>
  <% for (let i = 0; i < numbers.length; i++) { %>
    <li><%= numbers[i] %></li>
  <% } %>
</ul>
```

- **Explanation**:
  - `<% for (let i = 0; i < numbers.length; i++) { %>`: Starts a standard JavaScript `for` loop.
  - `<%= numbers[i] %>`: Displays each number from the `numbers` array as a list item.
  - `<% } %>`: Ends the loop.

---

### **Example with Loop and Condition**

You can combine loops with **if** statements to conditionally display certain items:

```html
<!-- filteredItems.ejs -->
<h2>Available Items:</h2>
<ul>
  <% items.forEach(item => { %>
    <% if (item.inStock) { %>
      <li><%= item.name %></li>
    <% } %>
  <% }); %>
</ul>
```

- **Explanation**:
  - This example loops through each `item` in the `items` array.
  - The `if (item.inStock)` condition checks if the item is in stock before displaying it.

---

### **Summary**

- **forEach loop**: `<% items.forEach(item => { %> ... <% }); %>` — Iterates through an array.
- **for loop**: `<% for (let i = 0; i < array.length; i++) { %> ... <% } %>` — Standard loop for more control.
- **Loop + condition**: Combine loops with **if** statements for conditional rendering.

Using loops in EJS makes it easy to display lists of items or dynamically generate HTML content based on arrays or other collections.
