
Public inheritance should be reserved for classes for which the LSP holds true. In those cases the derived classes can always be used instead of the base class from which they derive by code merely using base class references, pointers or members (i.e., conceptually derived classes *is-a* base class). This most often applies to classes derived from base classes offering virtual members. To separate the user interface from the redefinable interface the base class’s public interface should not contain virtual members (except for the virtual destructor) and the virtual members should all be in the base class’s private section. Such virtual members can still be overridden by derived classes (this should not come as a surprise, considering how polymorphism is implemented) and this design offers the base class full control over the context in which the redefined members are used. Often the public interface merely calls a virtual member, but those members can always be redefined to perform additional duties.

The prototypical form of a base class therefore looks like this:

```cpp
class Base
{
    public:
        virtual ~Base();
        void process();              // calls virtual members (e.g.,
                                     // v_process)

    private:
        virtual void v_process();    // overridden by derived classes
};
```

Alternatively a base class may offer a non-virtual destructor, which should then be protected. It shouldn’t be public to prevent deleting objects through their base class pointers (in which case virtual destructors should be used). It should be protected to allow derived classes (instructing them to call their base class destructors). Such base classes should, for the same reasons, have non-public constructors and overloaded assignment operators.

## 14.8 The ‘streambuf’ class

The class `std::streambuf` receives the character sequences processed by streams and defines the interface between stream objects and devices (like a file on disk). A `streambuf` object is usually not directly constructed, but usually it is used as base class of some derived class implementing the communication with some device.

The primary reason for existence of the class `streambuf` is to decouple the stream classes from the devices they operate upon. The rationale here is to add an extra layer between the classes allowing us to communicate with devices and the devices themselves. This implements a *chain of command* which is seen regularly in software design.

The *chain of command* is considered a generic pattern when designing reusable software, encountered also in, e.g., the TCP/IP stack.

A `streambuf` can be considered yet another example of the chain of command pattern. Here the program talks to stream objects, which in turn forward their requests to `streambuf` objects, which in turn communicate with the devices. Thus, as we will see shortly, we are able to do in user-software what had to be done via (expensive) system calls before.

The class `streambuf` has no public constructor, but does make available several public member functions. In addition to these public member functions, several member functions are only available to classes derived from `streambuf`. In section 14.8.2 a predefined specialization of the class `streambuf` is introduced. All public members of `streambuf` discussed here are also available in `filebuf`.

The next section shows the `streambuf` members that may be overridden when deriving classes from `streambuf`. Chapter 23 offers concrete examples of classes derived from `streambuf`.

The class `streambuf` is used by streams performing input operations and by streams performing output operations, and their member functions can be ordered likewise. The type `std::streamsize` used below may, for all practical purposes, be considered equal to the type `size_t`.

When inserting information into `ostream` objects the information is eventually passed on to the `ostream`’s `streambuf`. The `streambuf` may decide to throw an exception. However, this exception does not leave the `ostream` using the `streambuf`. Rather, the exception is caught by the `ostream`, which sets its `ios::badbit`. Exceptions raised by manipulators inserted into `ostream` objects are not caught by the `ostream` objects.

### Public members for input operations

- `std::streamsize in_avail();`
  
  This member function returns a lower bound on the number of characters that can be read immediately.

- `int sbumpc();`
  
  The next available character or EOF is returned. The returned character is removed from the `streambuf` object. If no input is available, `sbumpc` calls the (protected) member `uflow` (see section 14.8.1 below) to make new characters available. EOF is returned if no more characters are available.

- `int sgetc();`
  
  The next available character or EOF is returned. The character is *not* removed from the `streambuf` object. To remove a character from the `streambuf` object, `sbumpc` (or `sgetn`) can be used.

- `std::streamsize sgetn(char *buffer, std::streamsize n);`
  
  At most `n` characters are retrieved from the input buffer, and stored in `buffer`. The actual number of characters read is returned. The (protected) member `xsgetn` (see section 14.8.1 below) is called to obtain the requested number of characters.

- `int snextc();`
  
  The current character is obtained from the input buffer and returned as the next available character or EOF is returned. The character is *not* removed from the `streambuf` object.

- `int sputbackc(char c);`
  
  Inserts `c` into the `streambuf`’s buffer to be returned as the next character to read from the `streambuf` object. Caution should be exercised when using this function: often there is a maximum of just one character that can be put back.

- `int sungetc();`
  
  Returns the last character read to the input buffer, to be read again at the next input operation. Caution should be exercised when using this function: often there is a maximum of just one character that can be put back.

### Public members for output operations

- `int pubsync();`
  
  Synchronizes (i.e., flushes) the buffer by writing any information currently available in the `streambuf`’s buffer to the device. Normally only used by classes derived from `streambuf`.

- `int sputc(char c);`
  
  Character `c` is inserted into the `streambuf` object. If, after writing the character, the buffer is full, the function calls the (protected) member function `overflow` to flush the buffer to the device (see section 14.8.1 below).

- `std::streamsize sputn(char const *buffer, std::streamsize n);`
  
  At most `n` characters from `buffer` are inserted into the `streambuf` object. The actual number of characters inserted is returned. This member function calls the (protected) member `xsputn` (see section 14.8.1 below) to insert the requested number of characters.

### Public members for miscellaneous operations

The next three members are normally only used by classes derived from `streambuf`.

- `ios::pos_type pubseekoff(ios::off_type offset, ios::seekdir way, ios::openmode mode = ios::in | ios::out);`
  
  Sets the offset of the next character to be read or written to `offset`, relative to the standard `ios::seekdir` values indicating the direction of the seeking operation.

- `ios::pos_type pubseekpos(ios::pos_type pos, ios::openmode mode = ios::in | ios::out);`
  
  Sets the absolute position of the next character to be read or written to `pos`.

- `streambuf *pubsetbuf(char* buffer, std::streamsize n);`
  
  The `streambuf` object is going to use the buffer accommodating at least `n` characters.

### 14.8.1 Protected ‘streambuf’ members

The protected members of the class `streambuf` are important for understanding and using `streambuf` objects. Although there are both protected data members and protected member functions defined in the class `streambuf` the protected data members are not mentioned here as using them would violate the principle of data hiding. As `streambuf`'s set of member functions is quite extensive, it is hardly ever necessary to use its data members directly. The following subsections do not even list all protected member functions but only those that are useful for constructing specializations.

`Streambuf` objects control a buffer, used for input and/or output, for which begin-, actual- and end-pointers have been defined, as depicted in figure 14.4.

`Streambuf` offers one protected constructor:

- `streambuf::streambuf();`
  
  Default (protected) constructor of the class `streambuf`.

### 14.8.1.1 Protected members for input operations

Several protected member functions are available for input operations. The member functions marked virtual may of course be redefined in derived classes:

- `char *eback();`
  
  `Streambuf` maintains three pointers controlling its input buffer: `eback` points to the 'end of the putback' area; characters can safely be put back to this position. See also figure 14.4. `eback` points to the beginning of the input buffer.

- `char *egptr();`
  
  `egptr` points just beyond the last character that can be retrieved from the input buffer. See also figure 14.4. If `gptr` equals `egptr`, the buffer must be refilled. This should be implemented by calling `underflow`, see below.
