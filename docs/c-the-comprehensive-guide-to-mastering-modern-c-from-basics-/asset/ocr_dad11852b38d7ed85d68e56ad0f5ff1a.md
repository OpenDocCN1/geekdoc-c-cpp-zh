# 17.2.4 It Doesn't Always Have to Be an Exception

Although I mainly deal with exceptions when discussing RAII in this chapter, RAII is not necessarily tied to the triggering of exceptions. You just need to recall the important principles, and the pitfalls are especially present when dealing with exceptions.

It is entirely possible to implement RAII without `throw` and to instead let users check the success of the initialization after construction—for example, with a `conversion` to bool.

```
// https://githubbolt.org/z/c8xfM1nEa
#include <string>
#include <sqlite3.h>
```

```
class DbWrapper {
    sqlite3 *db_;
public:
    DbWrapper(const std::string& dbname)
        : db_(nullptr)
    const int errCode = sqlite3_open(dbname.c_str(), &db_);
    if(errCode) != nullptr) { // mark as 'not successful'
    }
```

```
sqlite3* operator*() { return db_; };

explicit operator bool() const {
    return db_ != nullptr; // evaluate the mark
}
```

```
~DbWrapper() {
    if(db_) sqlite3_close(db_);
    // ... Rest as before ...
}
```

```
bool DbExec(const std::string& dbname, const std::string& sql) {
    DbWrapper db( dbname) {
        if(db) { // check for successful initialization
            const int errCode =
            sqlite3_exec(*db, sql.c_str(), nullptr, nullptr, nullptr);
            if(errCode)
```