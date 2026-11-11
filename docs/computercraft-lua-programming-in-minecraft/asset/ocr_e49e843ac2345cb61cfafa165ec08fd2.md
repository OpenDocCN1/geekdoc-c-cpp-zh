program. Alternatively neither the sender or receiver are long, so they can easily be typed in.

Here is the full program for the sender.

```
```
while true do
  term.clear()
  term.setCursorPos(1, 1)
  print("Please enter message to send:")
  message = read()
  rednet.open("right")
  rednet.broadcast(message)
  rednet.close("right")
  sleep(0.1)
end
```
```

The program loops forever, waiting for a message to be entered. When a message is entered, then it opens a connection to the wireless network using rednet.open. The side passed as a parameter (in this case "right") needs to match the face of the computer to which the wireless access point is attached.

The command rednet.broadcast sends the message to all computers to which this computer is attached. Finally the connection is closed using rednet.close.

# ## Setting up the Receiver

The receiver setup is the same as the sender, with the addition of a monitor on which the messages will be displayed.

The program for the receiver is still pretty simple. See Appendix A for details of how to download and install it, or you can enter it using the editor.

```
```
rednet.open("left")
while true do
  id, message = rednet.receive(1)
  if message then
    print(message)
  end
end
```
```

The first thing that happens is that a connection is established to the wireless access point to the left. There is then a loop that will only quit if you CTRL-T the program. Inside this loop rednet.receive is called to see if there is a message.