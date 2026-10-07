# Program Notes

The main point of Listing 8.8 is that the os parameter, which is type ostream &, can refer to anostream object as cout and to an ofstream object such as fout. The program also illustrates howostream formatting methods can be used for both types. Let's review, or in some cases, examine for the first time, some of these methods (Chapter 17, "Input, Output, and Files," provides a fuller discussion.)

The set() method allows to set various formatting states. For example, the method call set(ios_base::fixed) places an object in the mode of using decimalpoint notation. The method call set(ios_base::showpoint) places an object in the mode of showing a decimal point, even if the following digits are zero. The precision(decimal) method indicates the number of figures to show to the right of the decimal (provided that the object is in fixed mode). All these settings stay until they are reset by another method call. The width() sets the field width to be used for the next output action. (The default is a field width of zero, which is then expanded to fit the actual quantity being.)

The file_it() uses an interfacing of method calls:
ios_base::fmtflags initial;
initial = os.set(ios_base::fixed); // save initial formatting state
...
os.set(initial); // restore initial formatting state

The set() returns a copy of all the formatting settings in effect before the call was made. ios_base::fmtflags is a fancy name for the type needed to store this information. So the assignment to initial the settings that were in place before the file_it() function was called. The initial variable can then be used as an argument to set() to reset all the formatting settings to this original value. Thus, the function restores the object to the state it had before passing to file_it().

Knowing more about classes will help you understand how these methods work and, for example, ios_base keeps popping up. But you don't have to wait until Chapter 17 to use these methods.

One final fact: Each object stores its own formatting settings. When the program passes through file_it(), cout's settings are altered and then restored. The program passes through file_it(), fout's settings are altered and then restored.

# When to Use Reference Arguments

There are two main reasons for using reference arguments:

+   - To allow to alter a data object in the calling function
- To speed up a program by passing a reference instead of an entire data object

The second reason is most important for larger data objects, as structures and class objects. These two reasons are reasons you might have for using a pointer argument. This makes sense because reference arguments are really just a different interface for