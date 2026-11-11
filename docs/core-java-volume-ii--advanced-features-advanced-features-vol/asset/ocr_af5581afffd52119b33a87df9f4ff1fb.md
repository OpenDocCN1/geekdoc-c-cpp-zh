```
```java
messages.append("Blocking:\n");
try (var sock = new Socket("localhost", 8189))
{
    in = new Scanner(sock.getInputStream(), StandardCharsets.UTF_8);
    while (!Thread.currentThread().isInterrupted())
    {
        messages.append("Reading ");
        if (in.hasNextLine())
        {
            String line = in.nextLine();
            messages.append(line);
            messages.append("\n");
        }
    }
}
finally
{
    EventQueue.invokeLater(() ->
    {
        messages.append("Socket closed\n");
        interruptButton.setEnabled(true);
        blockingButton.setEnabled(true);
    });
}
}

/**
 * A multithreaded server that listens to port 8189 and sends numbers to the client,
 * simulating a hanging server after 10 numbers.
 */
class TestServer implements Runnable
{
    public void run()
    {
        try (var s = new ServerSocket(8189))
        {
            while (true)
            {
                Socket incoming = s.accept();
                Runnable r = new TestServerHandler(incoming);
                new Thread(r).start();
            }
        }
        catch (IOException e)
        {
            messages.append("\nTestServer.run: " + e);
        }
    }
}
```
```