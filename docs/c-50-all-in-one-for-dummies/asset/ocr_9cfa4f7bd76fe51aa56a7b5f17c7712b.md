# StreamWriting for Old Walter

See the later section "More Readers and writers" for additional reader/
writer pairs.

The following sections provide the FileWrite and FileRead programs,
which demonstrate ways to use these classes for text I/O the C# way.

# StreamWriting for Old Walter

In the movie Golden Pond, Henry Fonda spent his retirement years trying
to catch a monster trout that he named Old Walter. You aren't out to drag in
the big fish, but you should at least cast a line into the stream. This section
covers writers to files.

Programs generate two kinds of outputs:

+   * Some programs write blocks of data as bytes in binary format.
This of output is useful for storing objects in an efficient way —
example, a file of Student objects that you need to persist (keep on disk
a permanent file).

See the later section "More Readers and Writers" for the BinaryReader
and StreamWriter classes.

A sophisticated example of binary I/O is the persistence of groups
ofobjects that refer to each other (using the HAS_A relationship).
An object involves identifying information (so its type can
be reconstructed when you read the object back in), and each of its
data members may be one of which references to connected objects,
with its own identifying information and data members. Persisting
objects is called serialization. You can look it up in Help when
you're ready; I don't cover it here. Sophistication is out of my league.

+   * Most programs read and write human-readable text: you know

Human-readable data was formerly known as ASCII, or slightly later,
ANSI. These two refer to the standards that defined them. However, ANSI encoding provides the alphabets
of East and West of Hawaii; it can handle only Roman letters, likenth used in English. It has no characters for Russian, Hebrew, Arabic,
Hindi, or any other language using a non-Roman alphabet, including
Asian languages such as Chinese, Japanese, and Korean. The modern,
more flexible Unicode file format is "backward-compatible" — including
the ANSI characters at the beginning of its character set, but still
providing a large number of other alphabets, including everything you

![](bbox=[0.135, 0.525, 0.225, 0.605])

![](bbox=[0.135, 0.745, 0.225, 0.825])