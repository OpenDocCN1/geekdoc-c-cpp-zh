distributes work packets to the worker (client) machines. Each client machine connects to a specific point on the network, provided by the server, and then waits for work to be given to it. Note that a client here is a CPU/GPU set, not a physical node. Thus, a quad-core CPU with four GPUs attached with a 1:1 mapping of CPU cores to GPU devices would represent four clients. Equally, a quad-core CPU with a 1:4 mapping of CPU cores to GPU devices would appear as a single client.

In ZeroMQ terminology, the server will bind with a port, that is, it will create an access point. All clients will then connect to that known access point. At this point no application data has been transmitted. However, in the background, ZeroMQ will have set up an internal queue for each client that connects to the port.

The next step is to decide on a messaging pattern, the simplest being the request/reply pattern. This is similar to MPI in that we have a send and recv function, and that for every send, there must be a response. This is done as follows:

```
Client:
zmq::context_t context(1);
zmq::socket_t socket(context, ZMQ_REQ);
socket.connect("tcp://localhost:5555");
Server:
zmq::context_t context(1);
zmq::socket_t socket(context, ZMQ_REP);
socket.bind("tcp://*:5555");
```

The CPU client then maintains a work queue, usually at least two items to allow for GPU double buffering, plus at least one inbound and one outbound network message.

The protocol used in the application is that the CPU client connects to the server and asks the server for a batch of work. The server then responds with a range that it would like the client to work on. The client then does any work necessary on the CPU to generate data for that work packet. This might be, for example, generating all possible combinations for a given model value to test against some prediction.

```
// Host program to be called from main
__host__ void gpu_kernel_client(const u32 pid)
{
    printf("\nRunning as Client");
}
```

```
// Init Network
zmq::context_t context(1);
zmq::socket_t socket(context, ZMQ_REQ);
socket.connect("tcp://localhost:5555");
```

```
// GPU params
size_t chunk_size;
u32 active_streams;
u32 num_devices;
```