# INPUT-OUTPUT AND MANIPULATORS IN C++

# 11.1 INTRODUCTION

In all the earlier chapters, we have worked with cin and cout for taking all different types of data as input and displaying them. But, we have not worked with the formatted output i.e., the way we want to print the data onto screen. For managing the input and output operations C++ provides the concept of stream classes. We know that cin is treated as standard input stream and cout as standard output stream classes. We known that cin is treated as standard input streams and cout as standard output streams. A stream is termed as input stream and when data is sent by the program to the output device say screen, the stream termed as output stream. It is quite obvious as we have seen in almost all the C++ programs so far that to take data from keyboard we have cin, which receives data and display s onto the screen. Thus, cin is standard input stream and cout is standard output stream.

We have also said that >> is an extraction operator << is insertion operator. This is so as cin >> extraction data from input stream from input stream and cout << displays inserts data into output stream. C++ provides numbers of stream classes for the efficient handling input and output and which is our next topic of discussion.

# 11.2 C++ STREAM CLASSES

In C++ there are number of streams classes for defining various streams related with files and for doing input output operations. All these classes are defined in the file iostream.h. Figure given below shows the hierarchy of these classes :