# 📚 MongoDB: Introduction and CRUD Operations

---

## 📘 What is MongoDB?
MongoDB is a **NoSQL, document-oriented database** designed for handling large volumes of semi-structured or unstructured data. Unlike traditional SQL databases, MongoDB stores data in **JSON-like documents**, making it flexible and ideal for modern application development.

It was first released in **2009** by a company called **10gen**, now known as **MongoDB Inc.**

---

## 🧩 What is NoSQL?

NoSQL stands for "**Not Only SQL**" and refers to a class of databases that:

- Do **not require fixed schemas**
- Handle **unstructured/semi-structured data**
- Support **horizontal scalability**
- Are optimized for **speed and flexibility**

MongoDB is one of the most widely used NoSQL databases today, thanks to its simplicity, rich document model, and ease of scaling.

---

## 🔄 MongoDB vs SQL Databases

| Feature             | SQL Databases                 | MongoDB (NoSQL)                   |
|---------------------|-------------------------------|------------------------------------|
| Data Format         | Tables (rows/columns)         | JSON-like Documents (BSON)         |
| Schema              | Rigid, Predefined              | Flexible, Schema-less              |
| Query Language      | SQL                           | JavaScript-like Queries            |
| Relationships       | JOINs                         | Embedded Documents or References   |
| Scalability         | Vertical (scale-up)           | Horizontal (scale-out via sharding)|
| Transactions        | Full ACID support             | Multi-document transactions (v4.0+)|

---

# 🛠️ MongoDB CRUD Operations

## 🟢 Create: Inserting Data
MongoDB provides two main commands for inserting data:
```javascript
db.collection.insertOne(document, options)
db.collection.insertMany([doc1, doc2, ...], options)
```
### ✅ Examples:
```javascript
// Insert a single document
db.studentData.insertOne({ name: "Alice", age: 20 })

// Insert multiple documents
db.studentData.insertMany([
  { name: "Bob", age: 22 },
  { name: "Charlie", age: 21 }
])
```
---
## 🔍 Read: Querying Data
To read documents from a collection, use:
```javascript
db.collection.find(filter, options)
db.collection.findOne(filter, options)
```
### ✅ Examples:
```javascript
// Get all documents
db.studentData.find()

// Pretty print output
db.studentData.find().pretty()

// Get first matching document
db.studentData.findOne({ name: "Alice" })
```

---
## 📝 Update: Modifying Data
MongoDB allows updates through:
```javascript
db.collection.updateOne(filter, update, options)
db.collection.updateMany(filter, update, options)
db.collection.replaceOne(filter, replacement, options)
```

### ✅ Examples:
```javascript
// Update the first document where fees is 5000
db.studentData.updateOne(
  { fees: 5000 },
  {
    $set: {
      fees: 6000,
      feesIncrementDate: new Date()
    }
  }
)

// Update all documents to add 'updatedBy'
db.studentData.updateMany(
  {},
  { $set: { updatedBy: "admin" } }
)

// Replace a document completely
db.studentData.replaceOne(
  { name: "Charlie" },
  { name: "Charlie", age: 23, enrolled: true }
)
```

#### 🆚 updateOne() vs replaceOne()
- `updateOne()` updates part of a document using update operators like `$set`, `$inc`, `$unset`, etc. Only the specified fields are changed.
- `replaceOne()` completely replaces the matched document with the new one — all existing fields are removed unless explicitly included in the replacement.

---
## ❌ Delete: Removing Data
MongoDB supports deleting documents via:
```javascript
db.collection.deleteOne(filter, options)
db.collection.deleteMany(filter, options)
```
### ✅ Examples:
```javascript
// Delete the first matching document
db.studentData.deleteOne({ email: "harry@gmail.com" })

// Delete all documents
db.studentData.deleteMany({})
```
⚠️ Be cautious: deleteMany({}) deletes all documents from the collection.

---
# 🧪 BSON vs JSON in MongoDB
Although you write documents in **JSON** format, MongoDB stores them internally in **BSON** (Binary JSON). BSON supports more data types and is more efficient to store and query.

## ✅ Benefits of BSON:
- Faster binary encoding/decoding
- Supports additional types like `Date`, `Binary`, `ObjectId`
- More efficient for internal operations
### Example:
```javascript
db.studentData.insertOne({ name: "Rajeev" })
// Output: { insertedId: ObjectId("66a1f0d3c8c1d45a5c8a8e12") }
```
Here, `ObjectId()` is a **BSON type**, not valid in plain JSON.

---

# 🆔 Behavior of `_id` Field in MongoDB
When inserting a document without an `_id`, MongoDB will automatically add one of type `ObjectId`. If you insert a document manually with an `_id` field:
- It must be **unique**
- Duplicate `_id` values will cause an error
```javascript
// Auto-generated _id
db.studentData.insertOne({ name: "Priya" })

// Custom _id
db.studentData.insertOne({ _id: 101, name: "Deepak" })

// Duplicate _id — will cause error
db.studentData.insertOne({ _id: 101, name: "Ravi" })
```

---
## 🧾 Key Quoting Rules in MongoDB Shell
In MongoDB shell (JavaScript-based), quotes are optional unless the key:
- Has spaces
- Has special characters
- Starts with a number

### ✅ Valid:
```javascript
{ name: "Rajeev" }
{ "first name": "Rajeev" }
```
### ❌ Invalid:
```javascript
{ first name: "Rajeev" } // Missing quotes
```
---
## 📦 Basic Shell Commands
```javascript
show dbs
```
List all existing databases. Note: A database only appears if it contains at least one document.

---
```javascript
use studentData
```
Switch to the studentData database. Will be created lazily when data is inserted.

---
```javascript
db.studentData.find()
db.studentData.find().pretty()
```
Retrieve all documents from the collection.
