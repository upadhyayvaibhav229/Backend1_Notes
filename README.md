
---

# 🧠 MongoDB (With Why It’s Used)

---

## 🟢 **What is MongoDB?**

MongoDB is a NoSQL document database that stores data in flexible, JSON-like documents called BSON(Binary JSON).
Instead of tables (like in SQL), it uses collections and documents.

### ✅ **Why use MongoDB?**

* Schema-less (flexible structure)
* Scalable and high performance
* Stores data in JSON format (easy to read/write)
* Works great with JavaScript and Node.js

---


## 🟢 MongoDB Cheatsheet

### 📌 Connect to MongoDB

```bash
mongo              # Start shell
mongosh            # Newer shell
```

---

## 📁 Database Operations

```js
show dbs                     // List all databases
use myDatabase               // Switch to or create database
db                          // Check current database
db.dropDatabase()           // Delete current database
```

---

## 📦 Collection Operations

```js
show collections             // List collections
db.createCollection('users') // Create new collection
db.users.drop()              // Drop collection
```

---

## 🧾 Documents (CRUD)

### ➕ Create

```js
db.users.insertOne({ name: "Vaibhav", age: 25 })
db.users.insertMany([{ name: "A" }, { name: "B" }])
```

---

### 🔍 Read (Query)

```js
db.users.find()                             // All documents
db.users.findOne({ name: "Vaibhav" })       // One match
db.users.find({ age: { $gt: 20 } })         // Filter: age > 20
db.users.find().limit(5).sort({ age: -1 })  // Top 5, descending
```

---

### 🔄 Update

```js
db.users.updateOne(
  { name: "Vaibhav" },
  { $set: { age: 26 } }
)

db.users.updateMany(
  { age: { $lt: 18 } },
  { $inc: { age: 1 } }
)
```

---

### ❌ Delete

```js
db.users.deleteOne({ name: "Vaibhav" })
db.users.deleteMany({ age: { $lt: 18 } })
```

---

## 🔍 Query Operators

| Operator | Description  | Example                         |
| -------- | ------------ | ------------------------------- |
| `$eq`    | Equal        | `{ age: { $eq: 25 } }`          |
| `$ne`    | Not equal    | `{ age: { $ne: 25 } }`          |
| `$gt`    | Greater than | `{ age: { $gt: 18 } }`          |
| `$lt`    | Less than    | `{ age: { $lt: 30 } }`          |
| `$in`    | In array     | `{ name: { $in: ["A", "B"] } }` |
| `$nin`   | Not in array | `{ age: { $nin: [20, 30] } }`   |

---

## 🔁 Projection

```js
db.users.find({}, { name: 1, age: 1 })    // Include name & age only
db.users.find({}, { password: 0 })       // Exclude password
```

---

## 🔄 Aggregation (Basics)

```js
db.users.aggregate([
  { $match: { age: { $gt: 20 } } },
  { $group: { _id: "$age", count: { $sum: 1 } } }
])
```

---

## 🔗 Indexes

```js
db.users.createIndex({ email: 1 })       // Create index
db.users.getIndexes()                    // List indexes
```

---

## 📘 Extra Commands

```js
db.users.countDocuments({})              // Total documents
db.users.distinct("city")                // Unique values of field
```

---
## 📚 Documentation

- [Mongoose Guide](Mongoose.md)
