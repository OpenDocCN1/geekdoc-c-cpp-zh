This concludes our discussion of printing. You now know how to print 2D graphics and other document types, how to enumerate printers and stream print services, and how to set and retrieve attributes. Next, we turn to two important user interface issues: the clipboard and the drag-and-drop mechanism.

# ## 11.13  The Clipboard

One of the most useful and convenient user interface mechanisms of GUI environments (such as Windows and the X Window System) is *cut and paste*. You select some data in one program and cut or copy them to the clipboard. Then, you switch to another program and paste the clipboard contents into that application. Using the clipboard, you can transfer text, images, or other data from one document to another or, of course, from one place in a document to another in the same document. Cut and paste is so natural that most computer users never think about it.

Even though the clipboard is conceptually simple, implementing clipboard services is actually harder than you might think. Suppose you copy text from a word processor to the clipboard. If you paste that text into another word processor, you expect the fonts and formatting to stay intact. That is, the text in the clipboard needs to retain the formatting information. However, if you paste the text into a plain text field, you expect that just the characters are pasted in, without additional formatting codes. To support this flexibility, the data provider must be able offer the clipboard data in multiple formats, so the data consumer can pick one of them.

The system clipboard implementations of Microsoft Windows and the Macintosh are similar, but, of course, there are slight differences. However, the X Window System clipboard mechanism is much more limited—cutting and pasting of anything but plain text is only sporadically supported. You should consider these limitations when trying out the programs in this section.

> > **NOTE:** Check out the file `jre/lib/flavormap.properties` on your platform to get an idea of what kinds of objects can be transferred between Java programs and the system clipboard.

Often, programs need to support cut and paste of data types that the system clipboard cannot handle. The data transfer API supports the transfer of arbitrary local object references in the same virtual machine. Between different virtual machines, you can transfer serialized objects and references to remote objects.

Table 11.5 summarizes the data transfer capabilities of the clipboard mechanism.