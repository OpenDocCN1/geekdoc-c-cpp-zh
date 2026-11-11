```
```java
add(new JScrollPane(messages));

interruptibleButton = new JButton("Interruptible");
blockingButton = new JButton("Blocking");

northPanel.add(interruptibleButton);
northPanel.add(blockingButton);

interruptibleButton.addActionListener(event ->
{
    interruptibleButton.setEnabled(false);
    blockingButton.setEnabled(false);
    cancelButton.setEnabled(true);
    connectThread = new Thread(() ->
    {
        try
        {
            connectInterruptibly();
        }
        catch (IOException e)
        {
            messages.append("\nInterruptibleSocketTest.connectInterruptibly: " + e);
        }
    });
    connectThread.start();
});

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
```
```