This code constructs the string by combining "Book = " with book. Since book is an object, its toString() method is called. That method is inherited from Object.prototype and returns the default value of "[object Object]" in most JavaScript engines. If you are happy with that value, there's no need to change your object's toString() method. Sometimes, however, it's useful to define your own toString() method so that string conversions return a value that gives more information. Suppose, for example, that you want the previous script to log the book's title:

```
var book = {
    title: "The Principles of Object-Oriented JavaScript",
    toString: function() {
        return "[Book " + this.title + "]"
    }
};

var message = "Book = " + book;

// "Book = [Book The Principles of Object-Oriented JavaScript]"
console.log(message);
```

This code defines a custom toString() method for book that returns a more useful value ① than the inherited version. You don't usually need to worry about defining a custom toString() method, but it's good to know that it's possible to do so if necessary.

# Modifying Object.prototype

All objects inherit from Object.prototype by default, so changes to Object.prototype affect all objects. That's a very dangerous situation. You were advised in Chapter 4 not to modify built-in object prototypes, and that advice goes double for Object.prototype. Take a look at what can happen:

```
Object.prototype.add = function(value) {
    return this + value;
};

var book = {
    title: "The Principles of Object-Oriented JavaScript"
};

console.log(book.add(5));        // "[object Object]5"
console.log("title".add("end"));  // "titleend"

// in a web browser
console.log(document.add(true));  // "[object HTMLDocument]true"
console.log(window.add(5));       // "[object Window]true"
```