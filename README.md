# MongoDB Documentation

## 1: Install MongoDB

**Local Installation:**

- Download MongoDB Community Server from the official MongoDB website.
- Follow the installation instructions for your operating system.
- Start the MongoDB server.

- Verify the installation:

```bash
    mongo --version
```

**MongoDB Atlas**

- Sign up for a free account at MongoDB Atlas.
- Create a free cluster and configure security settings (IP whitelist and database user).
- Connect to the cluster using the connection string provided.

## 2: Database and Collection Creation

Open the MongoDB shell.

Create a database named library:

```javascript
use library
```

Create a collection named books:

```javascript
db.createCollection("books");
```

## 3: Insert Data

Insert at least five book records into the books collection:

```javascript
db.books.insertMany([
  {
    title: "The Great Gatsby",
    author: "F. Scott Fitzgerald",
    publishedYear: 1925,
    genre: "Classic",
    ISBN: "9780743273565",
  },
  {
    title: "1984",
    author: "George Orwell",
    publishedYear: 1949,
    genre: "Dystopian",
    ISBN: "9780451524935",
  },
  {
    title: "To Kill a Mockingbird",
    author: "Harper Lee",
    publishedYear: 1960,
    genre: "Fiction",
    ISBN: "9780061120084",
  },
  {
    title: "Rich Dad",
    author: "Robert Kiyoski",
    publishedYear: 2004,
    genre: "Finance",
    ISBN: "9780590353428",
  },
  {
    title: "Harry Potter and the Sorcerer's Stone",
    author: "J.K. Rowling",
    publishedYear: 1997,
    genre: "Fantasy",
    ISBN: "9780590353427",
  },
]);
```

# 4: Retrieve Data

Retrieve all books:

```javascript
db.books.find();
```

Query books by a specific author:

```javascript
db.books.find({ author: "J.K. Rowling" });
```

Find books published after the year 2000:

```javascript
db.books.find({ publishedYear: { $gt: 2000 } });
```

## 5: Update Data

Update the publishedYear of a specific book:

```javascript
db.books.updateOne(
  { title: "The Great Gatsby" },
  { $set: { publishedYear: 1926 } }
);
```

Add a new field called rating to all books with a default value:

```javascript
db.books.updateMany({}, { $set: { rating: 4.5 } });
```

## 6: Delete Data

Delete a book by its ISBN:

```javascript
db.books.deleteOne({ ISBN: "9780743273565" });
```

Remove all books of a particular genre:

```javascript
db.books.deleteMany({ genre: "Fantasy" });
```

## 7: Data Modeling Exercise

Create a data model for an e-commerce platform:
**Collections:**

    users: Stores user information.

    products: Stores product details.

    orders: Stores order information with references to users and products.

Sample Structure:

```javascript
// Users Collection
db.users.insertOne({
  userId: 1,
  name: "John Doe",
  email: "john@example.com",
  address: "123 Main Street",
});

// Products Collection
db.products.insertOne({
  productId: 101,
  name: "Laptop",
  price: 10999,
  category: "Electronics",
});

// Orders Collection
db.orders.insertOne({
  orderId: 1001,
  userId: 1,
  products: [101],
  totalAmount: 10999,
  orderDate: new Date(),
});
```

## 8: Aggregation Pipeline

Total number of books per genre:

```javascript
db.books.aggregate([{ $group: { _id: "$genre", totalBooks: { $sum: 1 } } }]);
```

Average published year of all books:

```javascript
db.books.aggregate([
  { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } },
]);
```

Top-rated book:

```javascript
db.books.aggregate([{ $sort: { rating: -1 } }, { $limit: 1 }]);
```

## 9: Indexing

Create an index on the author field:

```javascript
db.books.createIndex({ author: 1 });
```

Benefits of indexing:

- Improves query performance.
- Reduces the time required to search for documents.

## 10: Testing

- Use the MongoDB shell or Compass to verify the inserted and updated records.
- Ensure all queries return the expected results.
