### EJS-এ স্টাইলিং

EJS-এ স্টাইলিং ঠিক যেমন আপনি সাধারণ HTML ফাইলে করবেন, তেমনি কাজ করে, তবে এখানে ডাইনামিক ডেটা এবং টেমপ্লেটিংয়ের অতিরিক্ত সুবিধা থাকে। আপনি বাহ্যিক CSS ফাইল, ইনলাইন স্টাইল, বা EJS টেমপ্লেটের ভিতরে স্টাইল যোগ করতে পারেন।

এখানে আপনার EJS-ভিত্তিক ওয়েবসাইটে স্টাইল যোগ করার জন্য একটি গাইড।

---

### **1. বাহ্যিক CSS ব্যবহার করা**

আপনি যেমন সাধারণ HTML ফাইলে CSS ফাইল লিঙ্ক করেন, ঠিক তেমনি EJS টেমপ্লেটেও বাহ্যিক CSS ফাইল যোগ করতে পারেন। এটি ভালো অভ্যাস যে CSS আলাদা ফাইলে রাখা হয়, যাতে কোড ব্যবস্থাপনা এবং রক্ষণাবেক্ষণ সহজ হয়।

#### উদাহরণ:

1. **একটি CSS ফাইল তৈরি করুন** (যেমন, `styles.css`) একটি `public` ডিরেক্টরির ভিতরে।

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

2. **CSS ফাইলটি লিঙ্ক করুন** আপনার EJS লেআউট (`layout.ejs`) ফাইলে।

```html
<!-- views/layout.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title><%= title %></title>
  <link rel="stylesheet" href="/styles.css"> <!-- বাহ্যিক CSS লিঙ্ক -->
</head>
<body>
  <%- body %> <!-- এখানে পৃষ্ঠা-নির্দিষ্ট কনটেন্ট যাবে -->
</body>
</html>
```

3. **CSS ফাইলটি Express সার্ভার থেকে সার্ভ করুন**।

```javascript
// server.js
const express = require('express');
const app = express();

// "public" ফোল্ডার থেকে স্ট্যাটিক ফাইল (CSS, ছবি ইত্যাদি) সার্ভ করুন
app.use(express.static('public'));

// আপনার অন্যান্য রুট এখানে...
```

এখন, যখন আপনি আপনার অ্যাপে যেকোনো রুটে নেভিগেট করবেন, তখন `styles.css` ফাইলটি EJS টেমপ্লেটের উপর প্রয়োগ হবে।

---

### **2. EJS-এ ইনলাইন স্টাইল**

আপনি সরাসরি আপনার EJS টেমপ্লেটের ভিতরে `<style>` ট্যাগ ব্যবহার করে স্টাইল যোগ করতে পারেন। এটি ছোট, পৃষ্ঠা-নির্দিষ্ট স্টাইলিংয়ের জন্য উপকারী।

#### উদাহরণ:

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

এতে, শুধুমাত্র `index.ejs` পৃষ্ঠায় স্টাইলিং প্রয়োগ হবে।

---

### **3. EJS ভেরিয়েবলের মাধ্যমে ডাইনামিক স্টাইলিং**

আপনি EJS ভেরিয়েবল ব্যবহার করে আপনার টেমপ্লেটে ডাইনামিকভাবে স্টাইল যোগ করতে পারেন। উদাহরণস্বরূপ, আপনি সার্ভার থেকে একটি রং বা ফন্ট সাইজ পাস করে পৃষ্ঠা দেখানোর সময় তার আউটলুক পরিবর্তন করতে পারেন।

#### উদাহরণ:

1. **সার্ভার থেকে ডাইনামিক স্টাইল ডেটা পাস করুন**:

```javascript
// server.js
app.get('/', (req, res) => {
  res.render('index', {
    title: 'Dynamic Styles',
    color: '#ff5733', // ডাইনামিক রঙের ডেটা পাস
  });
});
```

2. **EJS টেমপ্লেটে ডেটা ব্যবহার করুন**:

```html
<!-- views/index.ejs -->
<%- include('partials/header') %>
<h2>Dynamic Styles Page</h2>
<p>This page has dynamic styles based on the server data.</p>

<style>
  h2 {
    color: <%= color %>; /* ডাইনামিক রঙ যোগ করা */
  }
</style>

<%- include('partials/footer') %>
```

এই উদাহরণে, `<h2>` এলিমেন্টের রঙ সার্ভার থেকে পাস করা `color` ভেরিয়েবলের উপর ভিত্তি করে ডাইনামিকভাবে সেট করা হচ্ছে।

---

### **4. CSS ফ্রেমওয়ার্ক ব্যবহার**

আপনি সহজেই জনপ্রিয় CSS ফ্রেমওয়ার্ক যেমন **Bootstrap**, **Tailwind CSS**, বা **Bulma** আপনার EJS টেমপ্লেটের মধ্যে ব্যবহার করতে পারেন।

#### উদাহরণ: Bootstrap ব্যবহার করা

1. **Bootstrap CDN অন্তর্ভুক্ত করুন** আপনার লেআউট ফাইলে:

```html
<!-- views/layout.ejs -->
<head>
  <meta charset="UTF-8">
  <title><%= title %></title>
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"> <!-- Bootstrap -->
</head>
```

2. **Bootstrap ক্লাস ব্যবহার করুন** আপনার EJS টেমপ্লেটে:

```html
<!-- views/index.ejs -->
<%- include('partials/header') %>

<div class="container">
  <h2 class="text-center">Home Page</h2>
  <p class="lead">Welcome to the home page, styled with Bootstrap!</p>
</div>

<%- include('partials/footer') %>
```

এখন আপনার অ্যাপে Bootstrap স্টাইলিং প্রয়োগ হবে।

---

### **সারাংশ**

1. **বাহ্যিক CSS**: আপনার স্টাইলগুলি আলাদা ফাইলে রাখুন যাতে সহজে রক্ষণাবেক্ষণ করা যায়। Express এর মাধ্যমে এগুলি সার্ভ করুন।
2. **ইনলাইন স্টাইল**: সরাসরি নির্দিষ্ট EJS টেমপ্লেটে স্টাইল যোগ করুন।
3. **ডাইনামিক স্টাইলিং**: EJS ভেরিয়েবল ব্যবহার করে আপনার টেমপ্লেটে ডাইনামিক স্টাইল ডেটা Inject করুন।
4. **CSS ফ্রেমওয়ার্ক**: Bootstrap বা Tailwind CSS এর মতো CSS ফ্রেমওয়ার্ক সহজে আপনার টেমপ্লেটে ব্যবহার করুন।

এই কৌশলগুলি ব্যবহার করে আপনি আপনার EJS টেমপ্লেটগুলিকে স্টাইলিং করতে পারবেন এবং আপনার ওয়েব অ্যাপ্লিকেশনকে আরও আকর্ষণীয় ও প্রতিক্রিয়াশীল করে তুলতে পারবেন।
