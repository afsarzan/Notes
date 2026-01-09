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
 Navigating the Server
| Action | Command |
| :--- | :--- |
| **List Databases** | `show dbs` |
| **Switch/Create DB** | `use <database_name>` |
| **List Collections** | `show collections` |
| **Current DB Stats** | `db.stats()` |
| **Delete Database** | `db.dropDatabase()` |

---

## 2. CRUD Operations (The Core 4)

### Create
* **Single:** `db.<collection>.insertOne({ <key>: <value> })`
* **Multiple:** `db.<collection>.insertMany([{...}, {...}])`

### Read (Search)
* **All Documents:** `db.<collection>.find()`
* **With Formatting:** `db.<collection>.find().pretty()`
* **Match Specific:** `db.<collection>.find({ <field>: <value> })`
* **Sort Results:** `db.<collection>.find().sort({ <field>: 1 })` *(1: Asc, -1: Desc)*
* **Limit Results:** `db.<collection>.find().limit(<number>)`

### Update
* **Update One:** `db.<collection>.updateOne({ <filter_field>: <val> }, { $set: { <new_field>: <new_val> } })`
* **Increment Value:** `db.<collection>.updateMany({}, { $inc: { <field>: <number> } })`
* **Add to Array:** `db.<collection>.updateOne({ <filter> }, { $push: { <array_field>: <item> } })`

### Delete
* **Delete One:** `db.<collection>.deleteOne({ <field>: <value> })`
* **Delete Many:** `db.<collection>.deleteMany({ <field>: <value> })`
* **Wipe Collection:** `db.<collection>.drop()`

---

## 3. Query Operators (Filters)
Use these inside your `.find()` or `.update()` brackets.

| Category | Operator | Usage Example |
| :--- | :--- | :--- |
| **Comparison** | `$gt` / `$lt` | `{ price: { $gt: 100 } }` (Greater than) |
| **Comparison** | `$gte` / `$lte`| `{ price: { $gte: 100 } }` (Greater or equal) |
| **Comparison** | `$ne` | `{ status: { $ne: "closed" } }` (Not equal) |
| **Logical** | `$or` | `{ $or: [ {cond1}, {cond2} ] }` |
| **Logical** | `$and` | `{ $and: [ {cond1}, {cond2} ] }` |
| **In Array** | `$in` | `{ category: { $in: ["A", "B"] } }` |

---

## 4. Aggregation Pipeline (Processing Data)
Think of this as a "Filter -> Process -> Output" machine.



```javascript
db.<collection>.aggregate([
  { $match: { <field>: <value> } },           // Step 1: Filter
  { $group: { _id: "$<field>", total: { $sum: 1 } } }, // Step 2: Group & Count
  { $sort: { total: -1 } }                    // Step 3: Sort
])
