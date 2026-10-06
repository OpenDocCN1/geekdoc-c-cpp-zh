we split them on each character. This allows us to easily shift our array and get out characters. Next, we create our request string. The string consists of our write value and our key, terminated by a null character (\000); and then the name of the file, also terminated by a null character. We use the socket we created as part of our initialization to send our request to our host and port. The 0 value is the flags value of the send method. We don't need to set any special flags on our packet, so we leave the value as 0.

Next, we receive our packet back from the server. The recv method returns two things: the data it received, and information about where the data came from. We ignore that information and parse our binary string. We know our first character should be ASCII 1. So we verify that the bit is set, take the rest of the information up to the null character, and assign it to the ses variable. Now that we have negotiated our session, we will start sending data to the server.

# Note

If there are problems communicating between our client and server, both components may hang while they wait on output that may never get there. We can restart both pieces and try again if it fails. If we were going to use this in the real world, additional error handling would help us overcome these challenges.

We initialize the counter to 1 for our while loop. We will still have data in our contents array, we create a new message. We add our session and packet counter value to the message with null character separators. Finally, we add the next slice of contents and another null terminator. We do some math to ensure that our packet is limited to 1024 characters so that our packet will go through. We send each chunk until we are done. We have a way to send files with our DFTP module. Let's figure out how to receive them.

```
class DFTPServer < DFTPBase
  def initialize(host,port,key)
    super(host,port,key)
    @sock.bind(@host, @port)
```