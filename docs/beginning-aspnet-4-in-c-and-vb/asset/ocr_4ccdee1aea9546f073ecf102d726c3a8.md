You could use P2P technology to prevent this web server collapse. Instead of sending the file directly from the server to all the clients, you send the file to just a few clients. A few of the remaining clients then download the file from the clients that already have it, a few more clients download it from those second-level clients, and so on. In fact, this process is made even faster by splitting the file into chunks and dividing these chunks among clients, some of whom download it directly from the server, and some whom download chunks from other clients. This is how file-sharing technologies such as BitTorrent work, and is illustrated in Figure 45-3.

![](bbox=[0.2, 0.28, 0.8, 0.7])

FIGURE 45-3

# P2P Architectural Challenges

There are still problems to solve in the file-sharing architecture discussed here. For a start, how do clients detect that other clients exist, and how do they locate chunks of the file that other clients might have? Also, how can you ensure optimal communication between clients that may be separated by entire continents?

Every client participating in a P2P network application must be able to perform the following operations to overcome these problems:

+   - It must be able to *discover* other clients.
+   - It must be able to *connect* to other clients.
+   - It must be able to *communicate* with other clients.

The discovery problem has two obvious solutions. You can either keep a list of the clients on the server so clients can obtain this list and contact other clients (known as *peers*), or you can use an infrastructure (for example PNRP, covered in the next section) that enables clients to find each other directly. Most file-sharing