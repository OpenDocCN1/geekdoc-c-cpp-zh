
- **Exception** `bad_alloc`

  Memory was not allocated; the exception leaves the constructor. Thus, the buffer is considered not created, and no allocated resources are left behind. Because the object was not created, the destructor will not be called under any circumstances—even if data is uninitialized and thus a `delete[]` would be extremely dangerous. It never occurs.

The methods removed with `= delete` ensure that the buffer is not accidentally copied and then the entire internal data structure is freed multiple times: another reason to use `unique_ptr`.

### 17.2.2 Owning Raw Pointers

In complex object hierarchies, you must not forget that you also need to be prepared for the initialization of object variables (*member variables*) to fail with an exception. Even if you do not handle and swallow them with catch, but actually want to let the exception pass through, you may need to undo any previous initializations before the exception leaves the current constructor.

Unlike the preceding `Buffer` class, things are not so simple with `StereoImage`.

```cpp
// https://godbolt.org/z/TK3vTv1EM
struct StereoImage {
    Image *left, *right;
    StereoImage()
      : left(new Image)
      , right(new Image) // Danger!
    { }
    ~StereoImage() {
        delete left;
        delete right;
    }
};
```

**Listing 17.6** If “right” throws an exception, a leak occurs with “left”.

If the creation of `right` fails with an exception here, the memory already allocated for `left` would not be released. Because the constructor was exited with an exception, the `StereoImage` is considered not created, and its destructor will not be called. The compiler could undo the successful initialization of `left` by calling its destructor, but this is a raw pointer without a destructor! Another mechanism is needed—a catch with a rethrow or something other than a raw pointer for the fields of `StereoImage`.

The following listing provides one example (among many) of how you can avoid this vulnerability.

```cpp
// https://godbolt.org/z/cs4eEEGrf
#include <memory> // unique_ptr
struct Image {
    /* ... */
};
struct StereoImage {
    std::unique_ptr<Image> left, right;
    StereoImage()
        : left(new Image)
        , right(new Image)
    { }
};
```

**Listing 17.7** Correct RAII for “StereoImage”.

If the initialization of `right` fails with an exception, then `StereoImage`—as before—is considered not created. The destructor of `StereoImage` is not called. However, `left` now has a fully functional destructor, and the compiler can call it during unwinding. And that, in turn, releases the memory of `left`.

The raw pointer here occupies the resource memory. The same applies to all types of resources: *file handles*, *sockets*, *mutexes*, *semaphores*, and so on.

### 17.2.3 From C to C++

As noted at the beginning of the chapter, C++ developers will also frequently use C APIs. Typically, this involves *requesting* and *releasing* a resource via that API. For example, if you are using the SQLite serverless database interface, then a simplified code fragment might look like the following listing.

```cpp
// https://godbolt.org/z/hG3jPGYv (uses sqlite library)
#include <string>
#include <stdexcept>
#include <sqlite3.h> // library
using std::string; using std::runtime_error;

void dbExec(const string &dbname, const string &sql) {
    sqlite3 *db;
    int errCode = sqlite3_open(dbname.c_str(), &db); // acquire
    if(errCode) {
        throw runtime_error("Error opening the DB.");
    }
    errCode = sqlite3_exec(db, sql.c_str(), nullptr, nullptr, nullptr);
    if(errCode) {
        throw runtime_error("SQL Exec Error.");        // ✘ not good!
    }
    errCode = sqlite3_close(db);                 // release
}
```

**Listing 17.8** C API in C++ code.

Here, the `database` resource is acquired with `sqlite3_open()`, released with `sqlite3_close()`, and operated on with `sqlite3_exec()` in between. It is, of course, not a good idea to exit the function with an exception:

- The first exception is correct because if `sqlite3_open()` was not successful, `sqlite3_close()` does not need to be called.
- However, the second exception prevents `sqlite3_close()` from being called, and the resource would be blocked—or at least not released—which can have different impacts depending on the type of resource.

One could, of course, convert the entire SQLite3 API into a C++ API, but that is certainly a large undertaking. Besides, someone has surely already done this work for a popular API like SQLite3. Hopefully, they will also maintain it when something changes in the C API.

Rightly, one does not want to incur another dependency. A smaller solution might also suffice. A simple standard method to transform such code into RAII code is to wrap the resource in a wrapper class.

```cpp
// https://godbolt.org/z/n7Grhh1GM
#include <sqlite3.h>
class DbWrapper {
    sqlite3 *db_;
public:
    // acquire resource
    DbWrapper(const string& dbname)
        : db_{nullptr}
    {
        const int errCode = sqlite3_open(dbname.c_str(), &db_);
        if(errCode)
            throw runtime_error("Error opening"); // prevents sqlite3_close
    }

    // release resource
    ~DbWrapper() {
        sqlite3_close(db_);                     // release
    }

    // access Resource
    sqlite3* operator*() { return db_; }
    // No copy or assignment
    DbWrapper(const DbWrapper&) = delete;
    DbWrapper& operator=(const DbWrapper&) = delete;
};

void dbExec(const string &dbname, const string &sql) {
    DbWrapper db{ dbname };
    const int errCode = sqlite3_exec(*db, sql.c_str(), nullptr,
        nullptr, nullptr);
    if(errCode)
        throw runtime_error("Error SQL-Exec."); // now it works!
}
```

**Listing 17.9** C API with simple RAII.

With this wrapper, an exception can be thrown after `sqlite3_exec` without any issues. When leaving the scope of `db`—either by exception or normally—the destructor is called—thus, `sqlite3_close()`.

In the event of an exception in the constructor, the object is considered not created, and therefore the destructor with `sqlite3_close()` is not called. A good, simple RAII solution.

With the two lines with `= delete`, we prevent accidental assignments and copies that would cause multiple releases of the same resource `db_`.

5 To be precise, the documentation states that one should, but not must. We take this example as representative of the common case in resource management, where cleanup should only occur if the request was successful.

### 17.2.4 It Doesn't Always Have to Be an Exception

Although I mainly deal with exceptions when discussing RAII in this chapter, RAII is not necessarily tied to the triggering of exceptions. You just need to recall the important principles, and the pitfalls are especially present when dealing with exceptions.

It is entirely possible to implement RAII without `throw` and to instead let users check the success of the initialization after construction—for example, with a conversion to `bool`.

```cpp
// https://godbolt.org/z/c8xfM1nEa
#include <string>
#include <sqlite3.h>

class DbWrapper {
    sqlite3 *db_;
public:
    DbWrapper(const std::string& dbname)
        : db_(nullptr)
    {
        const int errCode = sqlite3_open(dbname.c_str(), &db_);
        if(errCode) db_ = nullptr;  // mark as not successful
    }

    sqlite3* operator()() { return db_; }

    explicit operator bool() const {
        return db_ != nullptr;      // evaluate the mark
    }
    ~DbWrapper() {
        if(db_) sqlite3_close(db_);
    }
    // ... Rest as before ...
};

bool dbExec(const std::string &dbname, const std::string &sql) {
    DbWrapper db { dbname };
    if(db) {                         // check for successful initialization
        const int errCode = sqlite3_exec(*db, sql.c_str(), nullptr, nullptr, nullptr);
        if(errCode)
            return false;           // still correct RAII
    }
    return (bool)db;
}
```

**Listing 17.10** C API with simple RAII, without throw.

It is crucial that you can undo all activities of the constructor in the destructor—regardless of whether the initialization was successful or not. This is ensured here by `db_ = nullptr` and the check in the destructor. And with the help of `operator bool()`, it can also be checked from the outside whether the initialization was successful. In the example, this is also marked with `explicit`. In the standard library, for example, the streams work this way—but more on that later.

### 17.2.5 Multiple Constructors

It is also important to ensure that all ways of creating the object must leave a valid instance. In the standard library, `ostream` is an example of this:

- `ostream` os creates a data stream to a file that has not yet been specified.
- `ostream` os {"file.txt"} opens the file, if possible.
