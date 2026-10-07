# The Andrew File System (AFS)

# ASIDE: The Importance Of Workload

One challenge of evaluating any system is the choice of workload. Because computer systems are used in so many different ways, there are a large variety of workloads to choose from. How should the system designer which workloads are important, in order to make reasonable decisions?

The designers of AFS, given their experience in measuring file systems used, made certain workload assumptions; in particular, they assumed that most files were not frequently shared, and accessed sequentially in their. Given these assumptions, the AFS design makes perfect sense.

However, these assumptions are not always correct. For example, imagine an application that adds information, periodically, to a log. This little write log, which adds small amounts of data to an existing file, are quite problematic for AFS. Many other difficult workloads exist well, e.g., random updates in a transaction database.

One place to get some information about what types of workloads are common through various research studies that have been performed. See any of these studies for good examples of workload analysis [B+91, H+11, R+00], including the AFS retrospective [H+88].

NFS, as a block-based protocol, performs I/O that is proportional to the size of the read or write.

Overall, we find that NFS and AFS make different assumptions and surprisingly realize different performance outcomes as a result Whether Whether differences matters is, as always, a question of workload.

# 50.8 AFS: Other Improvements

We saw with the introduction of Berkeley FFS (which added symbolic links and a number of other features), the designers of AFS took the opportunity when building their system to add a number of features that made the system easier to use and manage. For AFS provides a true namespace to clients, ensuring that all files are named the same way on all clients. NFS, in contrast, allows each client to mount NFS servers in any that they please, and thus only by convention (and great administrative effort) would be named similarly across clients.

AFS also takes security seriously, and incorporates mechanisms to authenticate users and ensure that a set of files could be private if a user so desired. NFS, in contrast, had quite primitive support for security for many years.

AFS also includes facilities for flexible user-managed access control. Thus, when using AFS, a user has a great deal of control over exactly

© 2008–19, ARPAC-DUSSEAU

THREE
EASY
PIECES