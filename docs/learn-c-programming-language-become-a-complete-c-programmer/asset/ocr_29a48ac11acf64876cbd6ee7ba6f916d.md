```
for (auto p : v) {
assert(p!=nullptr);
// ...
}
}
```

The **assert()** is a macro found in <cassert>. The error message produced by **assert()** is implementation-defined but should contain the source file name (__FILE__), and the source line number (__LINE__) containing the **assert()**.

Asserts are (as they should be) used more frequently in production code than in small illustrative textbook examples.

The name of the function (__func__) may also be included in the message. It can be a serious mistake to assume that the **assert()** is evaluated when it is not. For example, given a usual compiler setup, **assert(p!=nullptr)** will catch an error during debugging, but not in the final shipped product.

For a way to manage assertions, see §13.4.

# 30.4.3 system_error

In <system_error>, the standard library provides a framework for reporting errors from the operating system and lower-level system components. For example, we may write a function to check a file name and then open a file like this:

```
ostream& open_file(const string& path)
{
auto dn = split_into_directory_and_name(path); // split into {path,name}
error_code err {does_directory_exist(dn.first)}; // ask “the system” about the path if
(err) { // err!=0 means error
// ... see if anything can be done ...
if (cannot_handle_err)
throw system_error(err); }
// ...
return ofstream{path};
}
```

Assuming that “the system” doesn’t know about C++ exceptions, we have no choice about whether to deal with error codes or not; the only questions are “where?” and “how?” In <system_error>, the standard library provides facilities for classifying error codes, for mapping systemspecific error codes into more portable ones, and for mapping error codes into exceptions:

+   error_code
+   error_category
+   system_error error_condition
+   errc
+   future_errc io_errc