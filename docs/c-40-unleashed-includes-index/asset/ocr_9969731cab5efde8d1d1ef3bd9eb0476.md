```
IEnumerable<Customer> ReadCustomersFrom(string file) {
    try {
        using (FileStream fs = File.OpenRead(file)) {
            using (StreamReader sr = new StreamReader(fs)) {
                // Read from the file, creating Customer instances to return...
            }
        }
    }
    catch (IOException ex) {
        // If we handle this exception somehow, we can do it here.
    }
}
```

Various methods used in the preceding code can throw an exception. Instead of getting an error code back that needs to be checked on the spot, we declare an event handler using the try-catch statement. Each exception we're interested in handling can have its own catch block. If an exception is left unhandled, it simply propagates to the caller of the current method.

A structured approach to exceptions has various advantages, most of which are shown in the preceding section. First, we didn't have to sacrifice the return value of a method call in favor of error codes. Code simply reads as it was intended to behave in regular circumstances: If the file is found, we get a FileStream object back. Next, we can create a StreamReader and so on.

# TWO RETURN VALUES AND CHECKED EXCEPTIONS

It might help to think about structured exception handling as a way to add a second return "channel" to each function. The primary return channel is used to communicate the answer of a function in response to a call and is used in regular circumstances. A second return channel is monitored by the runtime for reported errors that signal less-common exceptional circumstances.

In platforms with checked exceptions, like Java, this is made more visible by the use of a throws clause on a method signature:

    public String readLine() throws IOException;

.NET doesn't have checked exceptions because they tend to lead to sloppy code where people introduce irresponsible catch-all statements. In addition, some caveats apply to versioning of code when new error conditions are introduced.

Second, propagation of exceptions that are left unhandled is a service provided by the runtime. In fact, this changes defaults: In Win32 and COM, if you don't do anything with the error code you get back, your program will continue to run. In most cases, this probably is not the right thing to do because the behavior of a program that has failed silently at some point in time is ill defined. At best, it will crash at some point in the future.