+   18.3 Find the error(s) in each of the following, and explain how to correct it (them):
+   a) string string1( 28 ); // construct string1
+      string string2( 'z' ); // construct string2
+   b) // assume std namespace is known
+      const char *ptr = name.data(); // name is "joe bob"
+      ptr[ 3 ] = '-'; 
+      cout << ptr << endl;

# Answers to Self-Review Exercises

+   18.1 a) <string>. b) std:: c) erase. d) find_first_of.

+   18.2 a) True.
+   b) True.
+   c) True.
+   d) False. A string is an object that provides many different services. A C-style string does not provide any services. C-style strings are null terminated; strings are not necessarily null terminated. C-style strings are pointers and strings are objects.

+   18.3 a) Constructors for class string do not exist for integer and character arguments. Other valid constructors should be used—converting the arguments to strings if need be.
+   b) Function data does not add a null terminator. Also, the code attempts to modify a const char. Replace all of the lines with the code:
+      cout << name.substr( 0, 3 ) + "-" + name.substr( 4 ) << endl;

# Exercises

+   18.4 Fill in the blanks in each of the following:
+   a) Class string member functions ______ and ______ convert strings to C-style strings.
+   b) Class string member function ______ is used for assignment.
+   c) ______ is the return type of function rbegin.
+   d) Class string member function ______ is used to retrieve a substring.

+   18.5 State which of the following statements are true and which are false. If a statement is false, explain why.
+   a) strings are always null terminated.
+   b) Class string member function max_size returns the maximum size for a string.
+   c) Class string member function at can throw an out_of_range exception.
+   d) Class string member function begin returns an iterator.

+   18.6 Find any errors in the following and explain how to correct them:
+   a) std::cout << s.data() << std::endl; // s is "hello"
+   b) erase( s.rfind( "x" ), 1 ); // s is "xenon"
+   c) string& foo()
+      {
+         string s( "Hello" );
+         ...
+         // other statements
+         return;
+      } // end function foo

18.7 (Simple Encryption) Some information on the Internet may be encrypted with a simple algorithm known as "rot13", which rotates each character by 13 positions in the alphabet. Thus, 'a' corresponds to 'n', and 'x' corresponds to 'k'. rot13 is an example of symmetric key encryption. With symmetric key encryption, both the encrypter and decrypter use the same key.