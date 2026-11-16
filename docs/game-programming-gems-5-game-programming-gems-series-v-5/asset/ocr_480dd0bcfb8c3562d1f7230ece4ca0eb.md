Since the Freezable's constructor will be called during the thaw, the user must take care not to reinitialize its members. For example, if a Freezable initializes its members to NULL at construction, the members will be reinitialized to NULL during the thaw.

We could work around the problem of reinitialization by providing an alternative constructor that only gets called by placement new during the thaw. The problem is that there is no way to extend this to the Freezable's members unless the user implements an alternative constructor for each member and sets up explicit calls to it down the constructor chain. That is a lot of hassle for what will probably amount to a bunch of empty constructors. A more pragmatic approach is to expose the problem from the start (so the user will be aware of it) and ask the user to check for reinitialization by calling FreezeMgr::IsThawing().

To review the limitations placed on the end user:

+   - The user must derive all classes containing virtual functions from Freezable.
+   - The user must overload GetClassName().
+   - The user must declare all Freezable types before using the FreezeMgr.
+   - The user must not change the order in which Freezable types are declared.
+   - The user should either do nothing in the Freezable's constructor or its member class constructors, or should check to see if a thaw is in progress and only perform initialization if there is not.

To manage and freeze the user's classes:

+   - Track the Freezables as they are created.
+   - After all the MemBlocks and FreezePtrs have remapped, remap the Freezables.
+   - Write out the FreezePtr remap table.
+   - Write out a table of Freezables. This table just contains the relative offset of each Freezable.

To thaw from a file:

+   - Read in the contiguous data block.
+   - Patch all the pointers.
+   - Find each Freezable in memory and determine its 32-bit type number.
+   - Use the type number to index the table of AbstractCreators.
+   - Pass the Freezable to the AbstractCreator::Construct().

# A Few More Features

The FreezeMgr is still not quite ready for prime time. More features are necessary for it to be useful.