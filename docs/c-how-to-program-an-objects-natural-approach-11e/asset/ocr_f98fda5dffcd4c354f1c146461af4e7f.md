full class definition must be available, as you’ll see in the .cpp files for classes Author (Fig. 20.4) and Book (Fig. 20.5).

```
```cpp
// Fig. 20.2: Author.h
// Author class definition.
#pragma once
#include <memory>
#include <string>
#include <string_view>

class Book; // forward declaration of class Book

// Author class definition
class Author {
public:
    explicit Author(std::string_view authorName);
    ~Author();

    // print the title of the Book this Author wrote
    void printBookTitle();

    std::string name; // name of the Author
    std::weak_ptr<Book> weakBookPtr; // Book the Author wrote
    std::shared_ptr<Book> sharedBookPtr; // Book the Author wrote
};
```
```

**Fig. 20.2** | Author class definition.

```
```cpp
// Fig. 20.3: Book.h
// Book class definition.
#pragma once
#include <memory>
#include <string>
#include <string_view>

class Author; // forward declaration of class Author

// Book class definition
class Book {
public:
    explicit Book(std::string_view bookTitle);
    ~Book();

    // print the name of this Book's Author
    void printAuthorName();

    std::string title; // title of the Book
    std::weak_ptr<Author> weakAuthorPtr; // Author of the Book
    std::shared_ptr<Author> sharedAuthorPtr; // Author of the Book
};
```
```

**Fig. 20.3** | Book class definition.