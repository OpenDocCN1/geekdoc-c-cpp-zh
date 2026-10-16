waits until the writing party connects by calling the WaitForConnection method. Next, within a loop (until the message “bye” is received), the pipe server reads messages to a buffer array and writes the message to the console (code file PipesReader/Program.cs):

```
private static void PipesReader(string pipeName)
{
    try
    {
        using (var pipeReader =
        new NamedPipeServerStream(pipeName, PipeDirection.In))
        {
            pipeReader.WaitForConnection();
            WriteLine("reader connected");

            const int BUFFERSIZE = 256;

            bool completed = false;
            while (!completed)
            {
                byte[] buffer = new byte[BUFFERSIZE];
                int nRead = pipeReader.Read(buffer, 0, BUFFERSIZE);
                string line = Encoding.UTF8.GetString(buffer, 0, nRead);
                WriteLine(line);
                if (line =="bye") completed = true;
            }
            WriteLine("completed reading");
            ReadLine();
        }
        catch (Exception ex)
        {
            WriteLine(ex.Message);
        }
    }
```

The following are some other options that you can configure with named pipes:

+   - You can set the enumeration PipeTransmissionMode to Byte or Message. With bytes, a continuous stream is sent; with messages every message can be retrieved.
+   - With the pipe options, you can specify WriteThrough to immediately write to the pipe and not to the cache.
+   - You can configure buffer sizes for input and output.
+   - You configure pipe security to designate who is allowed to read and write to the pipe. Security is discussed in Chapter 24.
+   - You can configure inheritatibility of the pipe handle, which is important for communicating with child processes.

Because the NamedPipeServerStream is a Stream, you can use StreamReader instead of reading from the byte array; this method simplifies the code:

```
var pipeReader = new NamedPipeServerStream(pipeName,
PipeDirection.In);
using (var reader = new StreamReader(pipeReader))
```