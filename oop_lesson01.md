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
