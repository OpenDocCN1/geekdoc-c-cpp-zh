For this reason, the key operations of the FreezeMgr are Freeze() and Thaw(). Since the FreezeMgr has to keep track of user-created data, its interface will also include methods for allocation and deletion.

As for the singleton design pattern used, we'll implement the singleton interface for this sample in the most basic way; see [Bilas00] for a more sophisticated approach.

From the end user's perspective, the process will be:

+   - Use the FreezeMgr to create game data.
+   - Initialize the data in whatever manner is appropriate.
+   - Command the FreezeMgr to pack all relevant data into a file and save it for optimal reloading.

# Tracking User Allocated Memory

Whenever the user asks the FreezeMgr to create something, the FreezeMgr will allocate a memory block and store an internal record of it. This record includes the block's size and address. We'll provide the following method for allocating memory:

```
template < typename TYPE >
TYPE* FreezeMgr::AllocTyped() { u32 elements; }
```

AllocTyped() is a template method that will use both malloc() and the placement new operator to create a user-specified type (or array of types) and call the appropriate constructor(s). We use malloc() instead of new because we want to control exactly when the class is constructed, independent of when its memory is allocated.

The record used to track memory allocations is called a MemBlock. MemBlocks are stored by the FreezeMgr in a map of addresses onto MemBlocks. The MemBlock contains a method that will check to see if a given address falls in its range. The method is:

```
bool MemBlock::ContainsAddress ( void* addr ) const;
```

In turn, the FreezeMgr contains a method that, given an arbitrary address, will return the MemBlock that contains the address, should such a MemBlock exist:

```
MemBlock* FreezeMgr::FindContainingMemBlock ( void* addr ) const;
```

# Tracking User Declared Pointers

User declared pointers are tracked with the help of a template class called FreezePtr. Its template parameter is the pointer type. The only data member is the pointer itself.

Upon construction, FreezePtr will attempt to register itself with the FreezeMgr. If the FreezePtr falls within a MemBlock, a record of it will be stored in that MemBlock. Otherwise, the FreezePtr is ignored.

Determining whether a FreezePtr falls within a MemBlock is just a matter of calling FreezeMgr::FindContainingMemBlock().