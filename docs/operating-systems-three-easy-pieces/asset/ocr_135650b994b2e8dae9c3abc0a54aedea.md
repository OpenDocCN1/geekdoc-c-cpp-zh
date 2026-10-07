# SUN’s Network File System (NFS)

ASIDE: KEY NFS TERMS

+   - The key to realizing the main goal of fast and simple crash recovery in NFS is in the design of a stateless protocol. After a crash, the server can quickly restart and begin serving requests again, clients just retry requests until they succeed.
- Making requests idempotent is a central aspect of the NFS protocol. An operation is idempotent when the effect of performing it times is equal to performing it once. In NFS, idempotency enables client retry without worry, and unifies client-message retransmission and how the client handles server crashes.
- Performance concerns dictate the need for client-side caching and buffering, but introduces a cache consistency problem.
- NFS implementations provide an engine solution to cache consistency through multiple means: a flush-on-open ensures that when a file is closed, its contents are forced to the server, enabling other clients to observe the updates to it. An attribute cache reduces the frequency of checking with the server whether a file has changed (via GETATTR requests).
- NFS servers must commit writes to persistent media before returning success; otherwise, data loss can occur.
- To support NFS integration into the operating system, Sun introduced the VFS/Vnode interface, enabling multiple file system implementations to coexist in the same operating system.

potency of operations is essential; because a client can safely replay a failed operation, it is OK to do whether or not the server has executed the request.
We have also seen how the introduction of caching in multiple-client, single-server system can complicate things. In particular, the system must resolve the cache consistency problem in order to behave reasonably; however, NFS does in a slightly hot fashion which can occasionally result in observed weird behavior. Finally, we saw how server caching can be: writes to the server must be forced to storage before returning success (otherwise data can be lost).
We haven't talked about other issues which are certainly relevant, security. Security in early NFS implementations was remarkably lax; it was rather easy for any user to masquerade as others and gain access to virtually any file. Subsequent integration with more serious authentication services (e.g., Kerberos [NT94]) have addressed these obvious deficiencies.