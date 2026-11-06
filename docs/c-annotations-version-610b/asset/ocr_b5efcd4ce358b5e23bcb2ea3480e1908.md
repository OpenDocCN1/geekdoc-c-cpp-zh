+   * int sputn(char const *buffer, std::streamsize n):
+   
+     At most n characters from buffer are inserted into the streambuf object. The actual number of characters inserted is returned. This member function calls the (protected) member xsputn (see section 14.8.1 below) to insert the requested number of characters.

# **Public members for miscellaneous operations**

The next three members are normally only used by classes derived from streambuf.

+   * ios::pos_type pubseekoff(ios::off_type offset, ios::seekdir way, ios::openmode mode = ios::in | ios::out):
+   
+     Sets the offset of the next character to be read or written to offset, relative to the standard ios::seekdir values indicating the direction of the seeking operation.

+   * ios::pos_type pubseekpos(ios::pos_type offset, ios::openmode mode = ios::in | ios::out):
+   
+     Sets the absolute position of the next character to be read or written to pos.

+   * streambuf *pubsetbuf(char* buffer, std::streamsize n):
+   
+     The streambuf object is going to use the buffer accomodating at least n characters.

# **14.8.1 Protected 'streambuf' members**

The protected members of the class streambuf are important for understanding and using streambuf objects. Although there are both protected data members and protected member functions defined in the class streambuf the protected data members are not mentioned here as using them would violates the principle of data hiding. As streambuf's set of member functions is quite extensive, it is hardly ever necessary to use its data members directly. The following subsections do not even list all protected member functions but only those are covered that are useful for constructing specializations.

Streambuf objects control a buffer, used for input and/or output, for which begin-, actual- and end-pointers have been defined, as depicted in figure 14.4.

Streambuf offers one protected constructor:

+   * streambuf::streambuf():
+   
+     Default (protected) constructor of the class streambuf.

# **14.8.1.1 Protected members for input operations**

Several protected member functions are available for input operations. The member functions marked virtual may or course be redefined in derived classes:

+   * char *eback():
+   
+     Streambuf maintains three pointers controlling its input buffer: eback points to the 'end of the putback' area: characters can safely be put back to this position. See also figure 14.4. Eback points to the beginning of the input buffer.

+   * char *egptr():
+   
+     Egptr points just beyond the last character that can be retrieved from the input buffer. See also figure 14.4. If gptr equals egptr the buffer must be refilled. This should be implemented by calling underflow, see below.