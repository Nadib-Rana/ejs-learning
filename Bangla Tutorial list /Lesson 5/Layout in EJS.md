### Layout in EJS (বাংলায়)

EJS-এ **layout** ব্যবহার করা ওয়েব অ্যাপ্লিকেশনের ডিজাইনকে আরও কার্যকর এবং পুনরায় ব্যবহারযোগ্য করতে সাহায্য করে। সাধারণত, একটি ওয়েবপেজে অনেক পৃষ্ঠা (page) থাকবে, এবং প্রতিটি পেজে কিছু সাধারণ অংশ (যেমন: হেডার, ফুটার) থাকবে। EJS-এ **layout** ব্যবহারের মাধ্যমে, আপনি এই সাধারণ অংশগুলো এক জায়গায় সংরক্ষণ করতে পারেন এবং প্রতিটি পেজে এটি অন্তর্ভুক্ত করতে পারেন।

---

### **Layout ব্যবহারের উপায়**

EJS-এর layout ব্যবহারের জন্য সাধারণত **partials** (যেমন হেডার, ফুটার) ব্যবহার করা হয়। আপনি এই পার্সিয়ালগুলোকে একটি মূল টেমপ্লেটের মধ্যে ইনক্লুড করতে পারেন।

---

### **১. Layout Template তৈরি করা**

প্রথমে একটি **layout.ejs** ফাইল তৈরি করুন, যেখানে আপনার পেজের সাধারণ অংশ (যেমন হেডার, ফুটার) থাকবে।

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
    <h1>আমার ওয়েবসাইট</h1>
    <nav>
      <a href="/">হোম</a>
      <a href="/about">আমাদের সম্পর্কে</a>
    </nav>
  </header>

  <!-- এখানে পেজ-specific কন্টেন্ট ইনক্লুড হবে -->
  <div>
    <%- body %>
  </div>

  <footer>
    <p>&copy; 2024 আমার ওয়েবসাইট</p>
  </footer>
</body>
</html>
```

- এখানে, `<%- body %>` এমন একটি জায়গা যেখানে প্রতিটি পেজের কন্টেন্ট **এড করা হবে**।

---

### **২. পার্সিয়াল (Partial) ব্যবহার করা**

আপনি যদি শিরোনাম, ফুটার ইত্যাদি বিভিন্ন কমন অংশ একাধিক পেজে ব্যবহার করতে চান, তবে **partial** ব্যবহার করতে পারেন।

#### Header.partial.ejs
```html
<!-- views/partials/header.ejs -->
<header>
  <h1>আমার ওয়েবসাইট</h1>
  <nav>
    <a href="/">হোম</a>
    <a href="/about">আমাদের সম্পর্কে</a>
  </nav>
</header>
```

#### Footer.partial.ejs
```html
<!-- views/partials/footer.ejs -->
<footer>
  <p>&copy; 2024 আমার ওয়েবসাইট</p>
</footer>
```

এগুলি বিভিন্ন পেজে একত্রে ব্যবহার করা যেতে পারে।

---

### **৩. Pug (or layout engine) Integration**

EJS সরাসরি layout engine-কে ইন্টিগ্রেট করে না, তবে আপনি **express-ejs-layouts** প্যাকেজ ব্যবহার করে **layout** সহজে ব্যবহার করতে পারেন।

#### `express-ejs-layouts` ব্যবহার করার জন্য:

1. প্রথমে `express-ejs-layouts` ইনস্টল করুন:
   ```bash
   npm install express-ejs-layouts
   ```

2. তারপর এটি **Express.js** সার্ভারে ব্যবহার করুন:
   
```javascript
// server.js
const express = require('express');
const ejsLayouts = require('express-ejs-layouts');
const app = express();

// Layouts Middleware ব্যবহার করুন
app.use(ejsLayouts);

// EJS এর view engine হিসেবে সেট করুন
app.set('view engine', 'ejs');

// Default Layout সেট করা
app.set('layout', 'layout');  // layout.ejs ফাইলটি ব্যবহৃত হবে

// Route তৈরি করুন
app.get('/', (req, res) => {
  res.render('index', { title: 'হোম পেজ', body: 'এটি হোম পেজের কন্টেন্ট।' });
});

app.get('/about', (req, res) => {
  res.render('about', { title: 'আমাদের সম্পর্কে', body: 'এটি আমাদের সম্পর্কে পেজের কন্টেন্ট।' });
});

app.listen(3000, () => {
  console.log('Server running at http://localhost:3000');
});
```

---

### **৪. Layout এবং Partial ব্যবহার করে রেন্ডারিং**

যখন আপনি কোন পেজ রেন্ডার করবেন, তখন **layout** এবং **partial** ব্যবহার করে মূল কন্টেন্ট দেখানো হবে।

```html
<!-- views/index.ejs -->
<%- include('partials/header') %>
<h2>হোম পেজ</h2>
<p><%= body %></p>
<%- include('partials/footer') %>
```

এতে, `header` এবং `footer` পার্সিয়াল ফাইলগুলো স্বয়ংক্রিয়ভাবে আপনার পেজে অন্তর্ভুক্ত হয়ে যাবে।

---

### **সারাংশ**

1. **Layout** ব্যবহার করে সাধারণ কন্টেন্ট এক জায়গায় সংরক্ষণ করুন, যেমন হেডার, ফুটার, বা নেভিগেশন।
2. **Partial** ফাইলগুলো আলাদাভাবে তৈরি করুন এবং প্রয়োজনে ইনক্লুড করুন।
3. **express-ejs-layouts** ব্যবহার করে লেআউট ব্যবস্থাপনা সহজ করুন।

এভাবে আপনি EJS-এ লেআউট ব্যবহারের মাধ্যমে আপনার ওয়েবসাইটের ডিজাইন এবং কন্টেন্ট পুনরায় ব্যবহারযোগ্য এবং সুশৃঙ্খল রাখতে পারেন।
