# THE ANDREW FILE SYSTEM (AFS)

668

+   TestAuth Test whether a file has changed
(used to validate cached entries)
GetFileStat Get the stat info for a file
Fetch Fetch the contents of file
Store Store this file on the server
SetFileStat Set the stat info for a file
ListDir List the contents of a directory

Figure 50.1: AFSv1 Protocol Highlights

One of the basics of all AFS is file-caching on the local disk of the client that is accessing a file. When open() the entire file (if it exists) is fetched from the server and stored in your local disk. Subsequent application read() and write() operations are redirected to the local file system where the file is stored; thus, these operations avoid network communication and are finally, upon close(), the file (if it has been modified) is flushed back to the server. Note the obvious continue: with cache blocks (without whole files, AFS could cache every block of an entire file) and also in client memory (not local disk).

Let's get into the details bit more. When a client application first calls open(), the AFS-side code (which the AFS designers call Venus) would send a Fetch protocol message to the server. The Fetch protocol message would send the pathname of the desired file (for example, /home/remzi/notes.txt) to the server (the group of which called Venus), which would traverse the pathname, find the desired file, and fetch the entire file back to the client. The client-side code would then cache the file on the local disk of the client (by writing it to local disk). As we said about subsequent read() and write() operations are strictly local in AFS (no communication with the server); they are just redirected to the local copy of the file. read() and write() act just like a call to a local file, once a block is accessed, it may be cached in client memory. AFS also uses client memory to cache copies of blocks that it has in local disk. Finally, when needed, the AFS checks if the file has been modified (i.e., it has been opened for writing); if so, it flushes the new version back to the server with a Store protocol message, sending the entire file and pathname to the server for permanent storage.

The next time a file is accessed, AFS does so more efficiently. Specifically, the client-side first contacts the server (using the TestAuth protocol message) in order to determine whether the file has changed. If not, the client would use the locally-cached copy, improving performance by avoiding a network transfer. The figure above shows some of the protocol messages in AFSv1. Note that this early version of the protocol only cached file contents; directories, for example, were kept at the server.

OPERATING SYSTEMS
[VERSION 1.01]

WWW.OSTEP.ORG