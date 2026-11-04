```
{
    using (var server = new NamedPipeServerStream(PIPE, PipeDirection.Out))
    {
        Console.Write("Waiting for connection...");
        server.WaitForConnection();
        Console.WriteLine("Connected");

        using (var writer = new StreamWriter(server))
        {
            Console.Write("Enter message: ");
            var message = Console.ReadLine();
            writer.WriteLine(message);
        }
    }
}
```

The Client method takes in a computer name where the named pipe server lives and uses the NamedPipeClient stream to set up communication. Although pipes can be set up for bidirectional communication, we make the client read-only using PipeDirection.In. To connect to the server, we call the Connect method, which could also take in a timeout value. Note also that more advanced constructor overloads exist, which allow control over pipe options, security aspects, and so on.

Once the client is connected, we establish a StreamReader over the stream to receive a single line of text. It's worth thinking for a moment about how the general-purpose stream reader can read a line of text from any kind of stream, keeping in mind that streams only have byte-level read and write operations.

The server is a mirror image to the client and differs in that no computer name has to be specified (after all, the machine itself is the server) on the NamedPipeServerStream constructor. As data is sent to the client, we configure the pipe direction for outbound traffic only. Another difference is the way we establish a connection, which now waits for a client to arrive. Overloads to the constructor of NamedPipeServerStream allow you to specify how many connections can be established, but we assume just one here. I leave it to you to discover asynchronous methods that can be used to spawn a worker thread as a client connects to the server (tip: it starts with Begin...).

How we write data from the server to the client should be obvious given the mirrored nature of both parts. This time we use a StreamWriter and its WriteLine method to send data across the pipe. Figure 28.13 shows two command prompt instances running the server and client component of this application.

Again, I leave it to you to envision a true chat application using named pipes, although easier techniques through WCF exist. One typically uses pipes to interact with existing software components that leverage them already. Notice that communication stacks such as .NET Remoting and WCF can leverage (named) pipes themselves in one of their "channel" implementations. Pipes provide an efficient way to send data across two or