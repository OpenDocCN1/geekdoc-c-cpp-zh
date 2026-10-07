# THE ANDREW File SYSTEM (AFS)

> > ASIDE: CACHE CONSISTENCY IS NOT A PANACEA
When discussing distributed file systems, much is made of the cache consistency the file systems provide. However, this baseline consistency does not solve all problems with regards to file access from multiple clients. For example, if you are building a repository, with multiple clients performing check-ins and check-outs of code, you can't simply rely on the file system to do all the work for you; rather, you must use explicit file-locking in order to ensure that the "right thing" happens when concurrent access takes place. Indeed, an application that cares about concurrent updates will add extra machinery to handle clients. The baseline consistency described in this chapter and the previous one are useful primarily for casual usage, i.e., when a user logs into a system and expects some reasonable version of their files to show up there. Expecting from more these protocols is setting yourself for failure, disappointment, and tear-frustrated frustration.

thus ensuring that the server would notify the client of its cached state. The benefit is obvious: although the first access to /home/remzi.txt generates many client-server messages (as above), it also establishes callbacks for all the directories as well as no server interaction at all. Thus, in the case where a file is cached at the client, AFS behaves nearly identically to a local disk-based system. If one accesses a file more than once, the second access would be just fast as accessing a file locally.

# 50.5 Cache Consistency

When we discussed NFS, there were two aspects of cache consistency we considered: update visibility and cache staleness. With update visibility, the question is: will the server be updated with a new version of a file? With cache staleness, the question is: once the server has a new version, how long before clients see the new version instead of an older copy?

Because of callbacks and whole-file caching, the cache consistency provided by AFS is easy to describe and understand. There are two important cases to consider: consistency between processes on different machines, and consistency between processes on the same machine.

Between different machines, AFS makes updates visible at the server and invalidates cached copies at the exact time, which is when the updated file is closed. A client opens a file, and then writes to it (perhaps repeatedly). When it is finally closed, the server then "breaks" callbacks for all clients with cached copies (and thus visible). At this point, the break is accomplished by contacting each client and informing them that the callback has on the file is no longer

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG