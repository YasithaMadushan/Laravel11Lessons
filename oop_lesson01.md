-------------------------------------------------------------------------------
**Real-world example of Object-Oriented Programming (OOP) in PHP**
-------------------------------------------------------------------------------
This example will cover basic OOP concepts such as classes, objects, properties, methods, inheritance, and encapsulation

Step 1: Define the Book Class
  ```php
<?php

class Book{
    //properties
    private $title;
    private $author;
    private $isbn;
    private $available;

    //constructor
public function __construct($title, $author, $isbn){
    $this->title = $title;
    $this->author = $author;
    $this->isbn = $isbn;
    $this->available = true;
}

    //getters and setters
    public function getTitle(){
        return $this->title;
    }

    public function getAuthor(){
        return $this->author;
    }

    public function getISBN(){
        return $this->isbn;
    }

    public function getAvailable(){
        return $this->available;
    }

    //method to borrow the book
    public function borrowBook(){
        if($this->available){
            $this->available = false;
            return true;
        }
        return false;
    }

    //method to return the book
    public function returnBook(){
        $this->available = true;
}
}

```
Step 2: Define the Library Class
  ```php
<?php
class Library{
    //properties
    private $books;

    //constructor
    public function __construct(){
        $this->books = [];
    }

    //methods
    public function addBook(Book $book){
        $this->books[] = $book;

    }
    public function findBookByIsbn($isbn){
        foreach($this->books as $book){
            if($book->getIsbn() == $isbn){
                return $book;
            }
        }
        return null;
    }
    public function listAvailableooks(){
        $availableBooks = [];
        foreach($this->books as $book){
            if($book->isAvailable()){
                $availableBooks[] = $book;
            }
        }
        return $availableBooks;
    }
}
?>
```
Step 3: Demonstrate page
  ```php
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Library Management System </title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </head>
    <body>
    <?php
    include 'Book.php';
    include 'Library.php';
    
    // Create a new library
    $library = new Library();
    
    // Create some books
    $book1 = new Book("1984", "George Orwell", "1234567890");
    $book2 = new Book("To Kill a Mockingbird", "Harper Lee", "2345678901");
    $book3 = new Book("The Great Gatsby", "F. Scott Fitzgerald", "3456789012");
    
    // Add books to the library
    $library->addBook($book1);
    $library->addBook($book2);
    $library->addBook($book3);
    
    // List all available books
    echo "<h3>Available Books:</h3>";
    echo "<table class='table table-striped'>";
    echo "<thead>";
    echo "<tr>";
    echo "<th>Book Title</th>";
    echo "<th>Author</th>";
    echo "</tr>";
    foreach ($library->listAvailableBooks() as $book) {
        echo "<tr>";
        echo "<td>".$book->getTitle() . "</td><td>" . $book->getAuthor() . "</td>";
        echo "</tr>";
    }
    echo "</table>";
    // Borrow a book
    $isbnToBorrow = "1234567890";
    $bookToBorrow = $library->findBookByIsbn($isbnToBorrow);
    if ($bookToBorrow && $bookToBorrow->borrowBook()) {
        echo "<div class='alert alert-success'>You borrowed: " . $bookToBorrow->getTitle() . "</div>";
    } else {
        echo "<div class='alert alert-warning'>Book not available for borrowing.</div>";
    }
    
    // List all available books after borrowing
    
    echo "<h3>Available Books after borrowing:</h3>";
    echo "<table class='table table-striped'>";
    echo "<thead>";
    echo "<tr>";
    echo "<th>Book Title</th>";
    echo "<th>Author</th>";
    echo "</tr>";
    foreach ($library->listAvailableBooks() as $book) {
        echo "<tr>";
        echo "<td>".$book->getTitle() . "</td><td>" . $book->getAuthor() . "</td>";
        echo "</tr>";
    }
    echo "</table>";
    // Return the borrowed book
    $bookToBorrow->returnBook();
    echo "\nYou returned: " . $bookToBorrow->getTitle() . "\n";
    
    // List all available books after returning
    echo "<div class='alert alert-success'>Available Books after returning:</div>";
    echo "<table class='table table-striped'>";
    echo "<thead>";
    echo "<tr>";
    echo "<th>Book Title</th>";
    echo "<th>Author</th>";
    echo "</tr>";
    foreach ($library->listAvailableBooks() as $book) {
        echo "<tr>";
        echo "<td>".$book->getTitle() . "</td><td>" . $book->getAuthor() . "</td>";
        echo "</tr>";
    }
    echo "</table>";
    ?>
    </body>
    </html>
    ```
    
