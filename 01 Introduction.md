# 📚 MongoDB Notes

## 📘 What is MongoDB?

MongoDB is a **NoSQL, document-oriented database** designed for handling large volumes of semi-structured or unstructured data. Unlike traditional SQL databases, MongoDB stores data in **JSON-like documents**, making it flexible and ideal for modern application development.

It was first released in **2009** by a company called **10gen**, now known as **MongoDB Inc.**

### 🧩 What is NoSQL?

NoSQL stands for "**Not Only SQL**" and refers to a class of databases that:
- Do **not require fixed schemas**
- Handle **unstructured/semi-structured data**
- Support **horizontal scalability**
- Are optimized for **speed and flexibility**

MongoDB is one of the most widely used NoSQL databases today.

### 🔄 MongoDB vs SQL Databases

| Feature             | SQL Databases                 | MongoDB (NoSQL)                   |
|---------------------|-------------------------------|------------------------------------|
| Data Format         | Tables (rows/columns)         | JSON-like Documents (BSON)         |
| Schema              | Rigid, Predefined              | Flexible, Schema-less              |
| Query Language      | SQL                           | JavaScript-like Queries            |
| Relationships       | JOINs                         | Embedded Documents or References   |
| Scalability         | Vertical (scale-up)           | Horizontal (scale-out via sharding)|
| Transactions        | Full ACID support             | Multi-document transactions (v4.0+)|

---

## 🛠️ MongoDB CRUD Commands

### 🟢 Create
```js
db.collection.insertOne(document, options)
db.collection.insertMany([doc1, doc2, ...], options)
