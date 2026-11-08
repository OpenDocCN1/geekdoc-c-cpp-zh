```
```cpp
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
        const int errCode = sqlite3_exec(*db,sql.c_str(),nullptr,nullptr);
        if(errCode)
            return false;           // still correct RAII
    }
    return (bool)db;
}
```
```

**Listing 17.10** C API with simple RAII, without throw.

It is crucial that you can undo all activities of the constructor in the destructor—regardless of whether the initialization was successful or not. This is ensured here by db_ = nullptr and the check in the destructor. And with the help of operator bool(), it can also be checked from the outside whether the initialization was successful. In the example, this is also marked with explicit. In the standard library, for example, the streams work this way—but more on that later.

# 17.2.5 Multiple Constructors

It is also important to ensure that all ways of creating the object must leave a valid instance. In the standard library, ostream is an example of this:

+   - `ostream` os creates a data stream to a file that has not yet been specified.
+   - `ostream` os {"file.txt"} opens the file, if possible.