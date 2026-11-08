+   * `class error_category`  
+     Classification of errors into *groups/families*, also an abstract base class for translation into readable text.
+   * `class system_error`  
+     Is an exception class that contains an `error_code` when an error is propagated by exception.
+   * `enum class errc`  
+     Is an enumeration of general-purpose values derived from the POSIX standard of type `error_condition`.
+   * `is_error_code_enum<>`, `is_error_condition_enum<>`, `make_error_code`, `make_error_condition`  
+     Implement mechanisms to convert `enum class` values into `error_code` or `error_condition` values.
+   * `generic_category()`  
+     Returns an `error_category` instance that can interpret `errc`-based codes and *conditions*.
+   * `system_category()`  
+     Returns an instance to interpret errors from the operating system.

# 28.5.2 Principles

Although `system_error` defines its own exception class, throwing an exception is not always the right way to handle an error. Sometimes, the additional return value of a function simply provides information that you want to incorporate into your program's control flow. A broken connection to a network server might be propagated as an exception, but if you are trying multiple servers during connection setup, you should not necessarily implement this in a loop with exceptions. And do not forget that in some areas, exceptions are entirely undesirable: In *real-time systems*, the requirements for deterministic timing behavior are so high that implementers sometimes avoid exceptions altogether. And in *embedded systems*, the additional memory consumption that some exception implementations bring cannot be neglected. Therefore, C++ pragmatically supports both types of error handling—return values with error codes as well as exceptions—and bridges the two worlds.

In case of an error, the `errno` variable often stores more detailed information about the nature of the error. Many functions from `<stdio>` and `<math>` store an error code here in case of failure. On POSIX-compliant platforms, many system functions provide details in `errno` when a function call fails. On Windows, `GetLastError` is often used additionally or instead. And the more libraries you use, the more sources from which error codes can be determined are added. C++ takes into account the possibility that error codes from different sources need to be evaluated and supports the extension of these by libraries. When that happens, the interface of existing functions must not change.