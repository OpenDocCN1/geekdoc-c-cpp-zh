
# The Andrew File System (AFS)

## ASIDE: The Importance Of Workload

One challenge of evaluating any system is the choice of workload. Because computer systems are used in so many different ways, there are a large variety of workloads to choose from. How should the system designer decide which workloads are important, in order to make reasonable decisions?

The designers of AFS, given their experience in measuring file systems used, made certain workload assumptions; in particular, they assumed that most files were not frequently shared, and accessed sequentially in their life-cycle. Given these assumptions, the AFS design makes perfect sense.

However, these assumptions are not always correct. For example, imagine an application that adds information, periodically, to a log. This little write log, which adds small amounts of data to an existing file, is quite problematic for AFS. Many other difficult workloads exist well, e.g., random updates in a transaction database.

One place to get some information about what types of workloads are common is through various research studies that have been performed. See any of these studies for good examples of workload analysis [B+91, H+11, R+00], including the AFS retrospective [H+88].

NFS, as a block-based protocol, performs I/O that is proportional to the size of the read or write.

Overall, we find that NFS and AFS make different assumptions and surprisingly realize different performance outcomes as a result. Whether differences matters is, as always, a question of workload.

## 50.8 AFS: Other Improvements

We saw with the introduction of Berkeley FFS (which added symbolic links and a number of other features), the designers of AFS took the opportunity when building their system to add a number of features that made the system easier to use and manage. For AFS provides a true namespace to clients, ensuring that all files are named the same way on all clients. NFS, in contrast, allows each client to mount NFS servers in any name that they please, and thus only by convention (and great administrative effort) would be named similarly across clients.

AFS also takes security seriously, and incorporates mechanisms to authenticate users and ensure that a set of files could be private if a user so desired. NFS, in contrast, had quite primitive support for security for many years.

AFS also includes facilities for flexible user-managed access control. Thus, when using AFS, a user has a great deal of control over exactly which files they can access. NFS, like most UNIX file systems, has much less support for this type of sharing.

Finally, as mentioned before, AFS tools to enable simpler management of servers for the administrators of the system. In thinking about system management, AFS was light years ahead of the field.

## 50.9 Summary

AFS shows how distributed file systems can be built quite differently than what we saw with NFS. The protocol design of AFS is particularly important; by minimizing server interactions (through whole-file-caching and callbacks), each server can support many clients and thus reduce the number of servers needed to manage a particular site. Many other features, including the single namespace, security, and access-control lists, make AFS quite nice to use. The consistency model provided by AFS is simple to understand and reason about, and does not lead to the weird behavior one sometimes observes in NFS.

Perhaps unfortunately, AFS is likely on the decline. Because NFS became an open standard, many different versions supported it, and, along with CIFS (the Windows file system protocol), NFS dominates the marketplace. Although one still sees AFS installations from time to time (such as in various educational institutions, including Wisconsin), the only lasting influence will likely be the ideas of AFS rather than the actual system itself. Indeed, NFSv4 now adds server state (e.g., an “open” protocol message), and thus bears an increasing similarity to the basic AFS protocol.

[V99] "File system usage in Windows NT 4.0" by Werner Vogels. SOSP '99, Kiawah Island Resort, South Carolina, December 1999. A cool study of Windows workloads, which are inherently different than many of the Unix-based systems that had previously been.

## Homework (Simulation)

This section introduces afs.py, a simple AFS simulator you can use to shore up your knowledge of how the Andrew File System works. Read the README file for more details.

## Questions

- 1. Run a few simple cases to make sure you can predict what values will be read by clients. Vary the random seed flag (-s) and see if you can trace through and predict intermediate values as well as the final values stored in the files. Also vary the number of files (-f), the number of clients (-C), and the read ratio (-r, from 0 to 1) to make it a bit more challenging. You might also generate longer traces to make for interesting interactions, e.g., (-n 2 or higher).
- 2. Now do the same and see if you can predict each callback that the AFS initiates. Try different random seeds, and make sure to use a high level of feedback (e.g., -d 3) to see when callbacks occur when you have the program compute the answers for you (-c). Can you guess exactly when each callback occurs? What is the precise condition for one to take?
- 3. Similar to above, run with some different random seeds and see if you can predict the exact cache state at each step. Cache state can be observed by running.
- 4. Now let's construct some specific workloads. Run the simulation with -A oal:wl,oal:cl flag. What are different possible values observed by client 1 when it reads the file a, when running with the random scheduler? (try different random seeds to see different outcomes?) Of all the possible schedule interleavings of the two clients' operations, how many of them lead client 1 reading the value 1, and how many reading the value 0?
- 5. Now let's construct specific schedules. When running with the -A oal:wl,oal:cl flag, also run with the following schedules: -S 01, -S 10011, -S 01100, and others of which you can think. What value will client 1 read?
- 6. Now run with this workload: -A oal:wl,oal:cl and vary the schedules as above. What happens when you run with -S 011007? What about when you run with -S 010011? What is important in determining the final value of the file?

## Summary Dialogue on Distribution

**Student:** Well, that was quick. Too quick, in my opinion!

**Professor:** Yes, distributed systems are complicated and cool and well worth your study; just not in this book (or course).

**Student:** That's too bad; I wanted to learn more! But I did learn a few things.

**Professor:** Like what?

**Student:** Well, everything can fail.

**Professor:** Good start.

**Student:** But by having lots of these things (whether disks, machines, or whatever), you can hide much of the failure that arises.

**Professor:** Keep going!

**Student:** Some basic techniques like retrying are really useful.

**Professor:** That's true.

**Student:** And you have to think carefully about protocols: the exact bits that are exchanged between machines. Protocols can affect everything, including how systems respond to failure and how scalable they are.

**Professor:** You really are getting better at this learning stuff.

**Student:** Thanks! And you're not a bad teacher yourself!

**Professor:** Well thank you very much too.

**Student:** So is this the end of the book?

**Professor:** I'm not sure. They don't tell me anything.

**Student:** Me neither. Let's get out of here.

**Professor:** OK.

**Student:** Go ahead.

**Professor:** No, after you.

**Student:** Please, professors first.

**Professor:** No, please, after you.

**Student:** (exasperated) Fine!

**Professor:** (waiting) ... so why haven't you left?

**Student:** I don't know how. Turns out, the only thing I can do is participate in these dialogues.

**Professor:** Me too. And now you've learned our final lesson...
