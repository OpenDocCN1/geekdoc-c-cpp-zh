See the later section "More Readers and writers" for additional reader/ writer pairs.

The following sections provide the FileWrite and FileRead programs, which demonstrate ways to use these classes for text I/O the C# way.

# StreamWriting for Old Walter

In the movie On Golden Pond, Henry Fonda spent his retirement years trying to catch a monster trout that he named Old Walter. You aren't out to drag in the big fish, but you should at least cast a line into the stream. This section covers writing to files.

Programs generate two kinds of output:

+   - Some programs write blocks of data as bytes in pure binary format. This type of output is useful for storing objects in an efficient way — for example, a file of Student objects that you need to persist (keep on disk in a permanent file).
+   - Most programs read and write human-readable text: you know, letters, numbers, and punctuation, like Notepad. The human-friendly StreamWriter and StreamReader classes are the most flexible ways to work with the stream classes. For some details, see the earlier section "Readers and writers."

See the later section "More Readers and Writers" for the BinaryReader and BinaryWriter classes.

A sophisticated example of binary I/O is the persistence of groups of objects that refer to each other (using the HAS_A relationship). Writing an object to disk involves writing identifying information (so its type can be reconstructed when you read the object back in), and then each of its data members, some of which may be references to connected objects, each with its own identifying information and data members. Persisting objects this way is called serialization. You can look it up in Help when you're ready; I don't cover it here. Sophistication is out of my league.

![](bbox=[0.15, 0.58, 0.25, 0.73])

![](bbox=[0.15, 0.82, 0.25, 0.97])

Human-readable data was formerly known as ASCII or, slightly later, ANSI, text. These two monikers refer to the standards organization that defined them. However, ANSI encoding doesn't provide the alphabets east of Austria and west of Hawaii: it can handle only Roman letters, like those used in English. It has no characters for Russian, Hebrew, Arabic, Hindi, or any other language using a non-Roman alphabet, including Asian languages such as Chinese, Japanese, and Korean. The modern, more flexible Unicode file format is "backward-compatible" — including the familiar ANSI characters at the beginning of its character set, but still providing a large number of other alphabets, including everything you