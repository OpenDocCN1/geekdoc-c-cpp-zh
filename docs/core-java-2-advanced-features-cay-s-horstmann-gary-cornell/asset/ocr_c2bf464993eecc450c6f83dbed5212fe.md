```
```java
blockingButton.addActionListener(event ->
{
    interruptibleButton.setEnabled(false);
    blockingButton.setEnabled(false);
    cancelButton.setEnabled(true);
    connectThread = new Thread(() ->
    {
        try
        {
            connectBlocking();
        }
        catch (IOException e)
        {
            messages.append("\nInterruptibleSocketTest.connectBlocking: " + e);
        }
    });
    connectThread.start();
});

cancelButton = new JButton("Cancel");
cancelButton.setEnabled(false);
northPanel.add(cancelButton);
cancelButton.addActionListener(event ->
{
    connectThread.interrupt();
    cancelButton.setEnabled(false);
});
server = new TestServer();
new Thread(server).start();
pack();
}

/**
 * Connects to the test server, using interruptible I/O.
 */
public void connectInterruptibly() throws IOException
{
    messages.append("Interruptible:\n");
    try (SocketChannel channel = SocketChannel.open(new InetSocketAddress("localhost", 8189)))
    {
        in = new Scanner(channel, "UTF-8");
        while (!Thread.currentThread().isInterrupted())
        {
            messages.append("Reading ");
            if (in.hasNextLine())
            {
                String line = in.nextLine();
                messages.append(line);
                messages.append("\n");
```
```

(Continues)