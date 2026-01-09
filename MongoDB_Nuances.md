# MongoDB Handbook & Essential Cheat Sheet

A comprehensive guide to using MongoDB, ranging from basic setup to advanced aggregation pipelines,
- MongoDB is a NoSQL document-oriented database. It stores data in JSON-like documents (actually BSON, a binary form of JSON)
- Key Components
  - mongod – the main MongoDB server daemon. It handles connections, database storage, and queries. You must run this before using MongoDB locally.
  - mongosh – the MongoDB Shell. It’s the command-line interface for interacting with MongoDB. You use it to run commands, queries, and scripts.
  - MongoDB Compass – a GUI tool for visualizing data, running queries, and analyzing performance. Perfect for beginners who prefer a graphical view.
- ** Basic Mongo Shell Commands**
    - show dbs // List all databases
    - use ecommerce // Create or switch to a database
    - show collections // List all collections in the current DB
    - db.dropDatabase() // Drop current database
- 

## 1. Introduction & Basics
MongoDB is a NoSQL, document-oriented database. It stores data in **BSON** (Binary JSON) format.

### Key Components
* **mongod**: The primary database server process.
* **mongosh**: The MongoDB Shell (command-line interface).
* **MongoDB Compass**: The official Graphical User Interface (GUI).
* **BSON Documents**: Data is stored in records called documents, which are grouped into collections.

---

## 2. Basic Shell Commands
| Task | Command |
| :--- | :--- |
| **List Databases** | `show dbs` |
| **Switch/Create DB** | `use ecommerce` |
| **List Collections** | `show collections` |
| **Check Stats** | `db.stats()` |
| **Check Server Info** | `db.serverStatus()` |
| **Drop Database** | `db.dropDatabase()` |

---

## 3. CRUD Operations (Create, Read, Update, Delete)

### Create (Insert)
```javascript
// Insert multiple products
db.products.insertMany([
  { name: "Wireless Mouse", price: 799, category: "Electronics", stock: 120, tags: ["wireless"], createdAt: new Date() },
  { name: "Gaming Laptop", price: 85999, category: "Computers", stock: 30, tags: ["gaming"], createdAt: new Date() }
]);
```
- Stage,Description,Example Use
$match,Filters documents,"{ $match: { category: ""Fruit"" } }"
$project,Shapes/Renames fields,"{ $project: { _id: 0, name: 1 } }"
$group,Calculates totals/avg,"{ $group: { _id: ""$cat"", total: { $sum: 1 } } }"
$sort,Reorders results,{ $sort: { totalSales: -1 } }
$lookup,Joins collections,Joining orders with products.
