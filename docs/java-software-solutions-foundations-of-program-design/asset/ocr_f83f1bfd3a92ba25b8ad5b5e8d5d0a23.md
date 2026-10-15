its destination, then moving the N-1 disks from the extra peg to the destination. This solution is inherently recursive because, to move the substack of N-1 disks, we can use the same process.

**SR 12.15** For an initial stack of 1 disk there is 1 call to the moveTower method. For an initial stack of 2 disks there are 3 calls. For 3 disks there are 7 calls. For every disk added, the number of calls increases by double the previous number, plus one.

# # 12.4 Recursion in Graphics

**SR 12.16** The base case of the TiledPictures program is a minimal size for the images to be produced. If the size of the area is smaller than the preset minimum, the recursion terminates.

**SR 12.17** A fractal is a geometric shape that can be composed of multiple versions of the same shape at different scales and different angles of orientation. Recursion can be used to draw the repetitive shapes over and over again.

# # Chapter 13 Collections

# # 13.1 Collections and Data Structures

**SR 13.1** A collection is an object whose purpose is to store and organize primitive data or other objects. Some collections represent classic data structures that are helpful in particular problem-solving situations.

**SR 13.2** Yes, the ArrayList class provides an abstract data type. The ArrayList class provides a collection of information. It provides operations for storing and accessing the information. The implementation details are hidden from us—that is, we do not need to know anything about how the information is stored or how the operations are implemented in order to use an ArrayList object.

**SR 13.3** An abstract data type (ADT) is a collection of data and the operations that can be performed on that data. An object is essentially the same thing in that we encapsulate related variables and methods in an object. The object hides the underlying implementation of the ADT, separating the interface from the underlying implementation, permitting the implementation to be changed without affecting the interface.