+   - `Throwable(String message, Throwable cause)` 1.4 constructs a Throwable with a given cause.
+   - `Throwable initCause(Throwable cause)` 1.4 sets the cause for this object or throws an exception if this object already has a cause. Returns `this`.
+   - `Throwable getCause()` 1.4 gets the exception object that was set as the cause for this object, or null if no cause was set.
+   - `StackTraceElement[] getStackTrace()` 1.4 gets the trace of the call stack at the time this object was constructed.
+   - `void addSuppressed(Throwable t)` 7 adds a "suppressed" exception to this exception. This happens in a try-with-resources statement where `t` is an exception thrown by a close method.
+   - `Throwable[] getSuppressed()` 7 gets all "suppressed" exceptions of this exception. Typically, these are exceptions thrown by a close method in a try-with-resources statement.

# **java.lang.Exception** 1.0

+   - `Exception(Throwable cause)` 1.4
+   - `Exception(String message, Throwable cause)` constructs an Exception with a given cause.

# **java.lang.RuntimeException** 1.0

+   - `RuntimeException(Throwable cause)` 1.4
+   - `RuntimeException(String message, Throwable cause)` 1.4