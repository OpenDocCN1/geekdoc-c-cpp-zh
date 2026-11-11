**java.nio.Buffer** 1.4

- `Buffer clear()`  
  prepares this buffer for writing by setting the position to 0 and the limit to the capacity; returns this.
- `Buffer flip()`  
  prepares this buffer for reading after writing, by setting the limit to the position and the position to 0; returns this.
- `Buffer rewind()`  
  prepares this buffer for rereading the same values by setting the position to 0 and leaving the limit unchanged; returns this.
- `Buffer mark()`  
  sets the mark of this buffer to the position; returns this.
- `Buffer reset()`  
  sets the position of this buffer to the mark, thus allowing the marked position to be read or written again; returns this.
- `int remaining()`  
  returns the remaining number of readable or writable values—that is, the difference between the limit and position.
- `int position()`
- `void position(int newValue)`  
  gets and sets the position of this buffer.
- `int capacity()`  
  returns the capacity of this buffer.

# 2.6.3 File Locking

When multiple simultaneously executing programs need to modify the same file, they need to communicate in some way, or the file can easily become damaged. File locks can solve this problem. A file lock controls access to a file or a range of bytes within a file.

Suppose your application saves a configuration file with user preferences. If a user invokes two instances of the application, it could happen that both of them want to write the configuration file at the same time. In that situation, the first instance should lock the file. When the second instance finds the file locked, it can decide to wait until the file is unlocked or simply skip the writing process.

To lock a file, call either the lock or tryLock methods of the FileChannel class.