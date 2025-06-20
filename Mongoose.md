# 🟣 **Mongoose Cheatsheet**

---

## 📘 What is Mongoose?

**Mongoose** is an **ODM (Object Data Modeling)** library for MongoDB and Node.js. It provides a structured and schema-based way to interact with MongoDB collections using JavaScript objects.

---

## ✅ Why Use Mongoose?

| Feature           | Benefit                                                |
| ----------------- | ------------------------------------------------------ |
| ✅ Schema-based    | Adds structure and rules to MongoDB’s flexible data    |
| ✅ Data validation | Automatically validates input before saving            |
| ✅ Query helpers   | Clean, readable code for interacting with the database |
| ✅ Middleware      | Add logic before/after actions (like saving)           |
| ✅ Relationships   | Easy referencing and population of related documents   |

> 📌 Without Mongoose, you must manually handle schemas, validation, and complex queries.

---

## 🔗 Setup

### 🔸 Installation

```bash
npm install mongoose
```

### 🔸 Connection

```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/myDB')
  .then(() => console.log('MongoDB Connected'))
  .catch(err => console.error(err));
```

---

## 🧱 Defining a Schema

```js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  age: Number,
  email: { type: String, required: true, unique: true },
  isAdmin: { type: Boolean, default: false }
}, { timestamps: true });
```

> 🟢 `timestamps: true` automatically adds `createdAt` and `updatedAt` fields.

---

## 🧩 Creating a Model

```js
const User = mongoose.model('User', userSchema);
```

---

## 🔄 CRUD with Mongoose

### ➕ Create

```js
const user = new User({ name: 'Vaibhav', age: 25, email: 'v@example.com' });
await user.save();

// OR directly
await User.create({ name: 'Vaibhav', age: 25, email: 'v@example.com' });
```

---

### 🔍 Read

```js
await User.find();                          // All documents
await User.findOne({ name: 'Vaibhav' });    // First match
await User.findById('objectId');            // Find by ID
```

---

### ✏️ Update

```js
await User.findByIdAndUpdate(id, { age: 30 }, { new: true });
await User.updateOne({ name: "Vaibhav" }, { $set: { age: 30 } });
```

---

### ❌ Delete

```js
await User.findByIdAndDelete(id);
await User.deleteOne({ name: 'Vaibhav' });
```

---

## 🔍 Query Helpers

```js
await User.find().sort({ age: -1 });              // Sort by age descending
await User.find().limit(5);                       // Limit results
await User.find().select('name email');           // Select specific fields
await User.countDocuments({ isAdmin: true });     // Count documents
```

---

## 🔗 Relationships & Populate

### Define Reference

```js
const postSchema = new mongoose.Schema({
  title: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
});
const Post = mongoose.model('Post', postSchema);
```

### Use Populate

```js
await Post.find().populate('author');
```

---

## 🔄 Middleware (Hooks)

```js
userSchema.pre('save', function(next) {
  console.log('Before saving user...');
  next();
});
```

* `pre('save')`: Before saving
* `post('save')`: After saving

---

## 🌐 Virtual Fields

```js
userSchema.virtual('info').get(function() {
  return `${this.name} (${this.age})`;
});
```

> Virtuals are not stored in DB but accessible in JS.

---

## ✅ Validations Example

```js
const schema = new mongoose.Schema({
  email: {
    type: String,
    required: true,
    match: /.+\@.+\..+/,
    unique: true
  },
  age: {
    type: Number,
    min: 18,
    max: 60
  }
});
```

---

## 🔐 Schema Options

| Option        | Purpose                        |
| ------------- | ------------------------------ |
| `required`    | Field must be provided         |
| `default`     | Default value if not specified |
| `unique`      | Unique across collection       |
| `min` / `max` | Number limits                  |
| `match`       | Regex pattern (for strings)    |

---

## 🧠 Summary

| Task          | Command                            |
| ------------- | ---------------------------------- |
| Connect       | `mongoose.connect()`               |
| Define schema | `new mongoose.Schema({})`          |
| Create model  | `mongoose.model()`                 |
| Create doc    | `Model.create()` or `new Model()`  |
| Read          | `Model.find()`, `Model.findById()` |
| Update        | `Model.findByIdAndUpdate()`        |
| Delete        | `Model.findByIdAndDelete()`        |
| Populate      | `.populate('refField')`            |
| Middleware    | `schema.pre/post()`                |
| Virtuals      | `schema.virtual().get()`           |

---
