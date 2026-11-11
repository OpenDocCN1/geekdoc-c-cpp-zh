enables or disables assertions for all classes loaded by this class loader that don’t have an explicit class or package assertion status.

+   - `void setClassAssertionStatus(String className, boolean b)` 1.4  
+   enables or disables assertions for the given class and its inner classes.
+   - `void setPackageAssertionStatus(String packageName, boolean b)` 1.4  
+   enables or disables assertions for all classes in the given package and its subpackages.
+   - `void clearAssertionStatus()` 1.4  
+   removes all explicit class and package assertion status settings and disables assertions for all classes loaded by this class loader.

# 7.5 Logging

Every Java programmer is familiar with the process of inserting calls to `System.out.println` into troublesome code to gain insight into program behavior. Of course, once you have figured out the cause of the trouble, you remove the print statements, only to put them back in when the next problem surfaces. The logging API is designed to overcome this problem. Here are the principal advantages of the API:

+   - It is easy to suppress all log records or just those below a certain level, and just as easy to turn them back on.
+   - Suppressed logs are very cheap, so there is only a minimal penalty for leaving the logging code in your application.
+   - Log records can be directed to different handlers—for displaying in the console, writing to a file, and so on.
+   - Both loggers and handlers can filter records. Filters can discard boring log entries, using any criteria supplied by the filter implementor.
+   - Log records can be formatted in different ways—for example, in plain text or XML.