```
```java
/**
 * A Java class that holds the bytecodes in a byte array.
 * @version 1.00 2007-11-02
 * @author Guy Horstmann
 */
public class ByteArrayJavaClass extends SimpleJavaFileObject
{
    private ByteArrayOutputStream stream;

    /**
     * Constructs a new ByteArrayJavaClass.
     * @param name the name of the class file represented by this file object
     */
    public ByteArrayJavaClass(String name)
    {
        super(URI.create("bytes:///" + name), Kind.CLASS);
        stream = new ByteArrayOutputStream();
    }

    public OutputStream openOutputStream() throws IOException
    {
        return stream;
    }

    public byte[] getBytes()
    {
        return stream.toByteArray();
    }
}
```
```

| `javax.tools.Tool` | 6 |
|---|---|
| • `int run(InputStream in, OutputStream out, OutputStream err, String... arguments)` | runs the tool with the given input, output, and error streams and the given arguments. Returns 0 for success, a nonzero value for failure. |

| `javax.tools.JavaCompiler` | 6 |
|---|---|
| • `StandardJavaFileManager getStandardFileManager(DiagnosticListener<?> diagnosticListener, Locale locale, Charset charset)` | gets the standard file manager for this compiler. You can supply null for default error reporting, locale, and character set. |