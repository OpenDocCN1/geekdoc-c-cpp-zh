```
```cpp
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
```

**Listing 17.9** C API with simple RAII.

With this wrapper, an exception can be thrown after `sqlite3_exec` without any issues. When leaving the scope of `db`—either by exception or normally—the destructor is called—thus, `sqlite3_close()`.

In the event of an exception in the constructor, the object is considered not created, and therefore the destructor with `sqlite3_close()` is not called. A good, simple RAII solution.

With the two lines with `= delete`, we prevent accidental assignments and copies that would cause multiple releases of the same resource `db_`.

# 17.2.4  It Doesn't Always Have to Be an Exception

Although I mainly deal with exceptions when discussing RAII in this chapter, RAII is not necessarily tied to the triggering of exceptions. You just need to recall the important principles, and the pitfalls are especially present when dealing with exceptions.

It is entirely possible to implement RAII without `throw` and to instead let users check the success of the initialization after construction—for example, with a conversion to `bool`.

```
```cpp
// https://godbolt.org/z/c8xfM1nEa
#include <string>
#include <sqlite3.h>

class DbWrapper {
    sqlite3 *db_;
```
```