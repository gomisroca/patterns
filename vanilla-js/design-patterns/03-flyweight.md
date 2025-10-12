## Flyweight Pattern

Useful way to conserve memory when creating a large number of similar objs.

### Example

If we have a library, it won't have just one copy of a book, it will have multiple copies of the same book. It wouldn't make sense to create a new book instance each time if there's multiple copies. Instead, we want to create multiple instances of the `Book` contructor, which will represent a single book.

```js
class Book {
  constructor(title, author, isbn) {
    this.title = title;
    this.author = author;
    this.isbn = isbn;
  }
}
```

Now, we can add books to the library:

```js
const books = new Map();

const createBook = (title, author, isbn) => {
  const existingBook = books.has(isbn);

  if (existingBook) {
    return books.get(isbn);
  }

  const book = new Book(title, author, isbn);
  books.set(isbn, book);

  return book;
};
```

However, we can't add multiple copies of the same book to the library just yet.

```js
// Keep track of total amount of books
const bookList = [];

const addBook = (title, author, isbn, availability, sales) => {
  const book = {
    ...createBook(title, author, isbn),
    sales,
    availability,
    isbn,
  };

  bookList.push(book);
  return book;
};
```

Now, instead of creating a new Book instance each time we add a copy, we will use the same instance of said book.

```js
addBook("Harry Potter", "JK Rowling", "AB123", false, 100);
addBook("Harry Potter", "JK Rowling", "AB123", true, 50);
addBook("To Kill a Mockingbird", "Harper Lee", "CD345", true, 10);
addBook("To Kill a Mockingbird", "Harper Lee", "CD345", false, 20);
addBook("The Great Gatsby", "F. Scott Fitzgerald", "EF567", false, 20);

console.log("Total amount of copies: ", bookList.length); // 5 copies of books
console.log("Total amount of books: ", isbnNumbers.size); // 3 unique instances of books
```

### Pros

- Useful when creating a huge number of objs
- Minimizes memory consumption

### Cons

- Nowadays, hardware is powerful enough to make flyweight pattern less important
