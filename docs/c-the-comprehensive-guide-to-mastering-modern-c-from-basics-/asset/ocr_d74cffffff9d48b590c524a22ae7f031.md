+   * Memory for data has been allocated, and the pointer is valid. The buffer object is considered correctly created, and if it needs to be cleaned up, the destructor does this.

+   * Memory was not allocated; the exception leaves the constructor. Thus, the buffer is considered not created, and no allocated resources are left behind. Because the object was not created, the destructor will not be called under any circumstances—even if data is uninitialized and thus a delete[] would be extremely dangerous. It never occurs.

The methods removed with = delete ensure that the buffer is not accidentally copied and then the entire data structure is freed multiple times: another reason to use unique_ptr.

# 17.2.2 Owning Raw Pointers

In complex object hierarchies, you must also need to be prepared for the initialization of object variables (member variables) to fail with an exception. Even if you do not handle and swallow them with catch, but actually want to let the exception pass through, you may need to undo any previous initializations before the exception leaves the current constructor.

Unlike the preceding Buffer class, things are not so simple with StereoImage.