# # Chapter 1: Filing Information with the Streams Library

# ### In This Chapter

+   - Seeing the need for a streams library
+   - Using the right header files
+   - Opening a file
+   - Dealing with errors
+   - Working with flags to customize your file opening

First things first. We've all heard of rivers and lakes and streams, and it's interesting just how many common words are used in computer programming. That's handy, because it lets us use words we already know with similar meaning, but it's also a bummer because it's harder to impress strangers. While we don't have gluggerbumbles and picklershops in computer programming — words most people have never even heard of, mainly because we made them up — we do have *streams*!

Most programmers think of a stream as the same thing as a file. You know — a file that's stored on your hard drive or maybe on a Universal Serial Bus (USB) flash drive or Secure Digital (SD) card. But streams go beyond just files. A *stream* is any type of data structure that you *stream* (that is, flow) your data into and out of in a sequence of bytes.

For example, if we open an Internet connection to a top-secret computer that stores all our top-secret data (oooh), and we start putting our data on the remote computer, we might use a stream-based data structure. By that we mean we write the data in sequence, one byte after another, as the data goes over the Internet like a stream of water, reaching the remote computer. The data we wrote first gets there first and so on.

You can use the same approach for storing data into a file. Rather than just filling a huge 500MB data structure and then dropping it onto the hard drive, you write your data piece after piece; the information goes into the file.

In this chapter, we talk about different kinds of streams available to you, the C++ programmer.