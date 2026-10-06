
Publication License, v1.0 or later (the latest version is available at http://www.openccontent.org/openpub/).

Trolltech®, Qt®, Qtopia®, and the Trolltech and Qtopia logos are registered trademarks of Trolltech ASA.

ISBN-13: 978-0-13-235416-5

Text printed in the United States on recycled paper at Courier in Westport, Massachusetts.

First printing, February 2008

# Series Editor's Note

Dear Reader,

As a working programmer, I use Qt every day, and I am really impressed by the organization, design, and power that Qt brings to the C++ programmer.

While Qt began as a cross-platform GUI toolkit, it has expanded to include portable facilities for just about every aspect of day-to-day programming: files, processes, networking, and database access, to name just a few. Because of Qt's broad applicability, you can really write your code once and just recompile it on a different platform to have it work out of the box. This is extraordinarily valuable when your customer base requires your product to run on different platforms.

Of course, because Qt is also available with an open source license, if you're an open source developer, you can too benefit from everything Qt has to offer.

While Qt comes with extensive online help, that help is primarily reference oriented. The example programs are useful, but it can be hard to reverse engineer correct use of Qt for your programs just by reading the examples. And that is where this book comes into the picture.

This is a really neat book. First, it's the official book on Qt from Trolltech, which says a lot. But it's also a great book: well organized, well written, and easy to follow and learn from. The combination of a great book about a great technology makes for a real winner, and that is why I am very proud and excited to have this book in the Prentice Hall Open Source Software Development Series.

I hope you will enjoy reading this book and that you will learn a lot from it; I certainly did.

Arnold Robbins
of Ayalon, Israel
November 2007

# Foreword

Why Qt? Why do programmers like us choose Qt? Sure, there are the obvious answers: Qt's single-source compatibility, its feature richness, its C++ performance, the availability of the source code, its documentation, the high-quality technical support, and all the other items mentioned in Trolltech's glossy marketing materials. This is all very well, but it misses the most important point: Qt is successful because programmers like it.

How come programmers we like technology, but dislike another? Personally, I believe software engineers enjoy technology that feels right, but dislike everything that doesn't. How else can we explain that some of the brightest programmers need to help program a video recorder, or that most engineers seem to have trouble operating the company's phone system? For one I am perfectly capable of memorizing sequences of random numbers and commands, but if these are required to control my answering machine, I'd prefer not to have one. At Trolltech, our phone system forces us to press the "*" for two seconds before we are allowed to enter the other person's extension number. If you forget to do this and start to enter the extension immediately, you have to dial the entire number again. Why not '#', or '1' or '5', or any of the other 20 keys on the phone? Why two seconds and not one, or two and a half? Why anything at all? I find the phone so irritating that I avoid it whenever I can. Nobody likes having to do random things, especially when these things randomly depend on some context you wish you didn't have to know about in the first place.

Programming can be a lot like using our phone system, only worse. And this is where Qt comes to the rescue. Qt is different. For one thing, Qt makes sense. And for another, Qt is fun. Qt lets you concentrate on your tasks. When Qt's architects faced a problem, they didn't just look for a good solution, or a quick solution, or the simplest solution, and then they documented it. Granted, they made mistakes, and granted, some of their design decisions didn't pass the test of time, but they still got a lot of things right, and what wasn't right could and be corrected. You can see this by the fact that a system originally designed to bridge Windows 95 now unifies modern desktop systems as diverse as Windows Vista, Mac OS X, and GNU/Linux, as well as small devices as mobile phones.

# Preface

Qt is a comprehensive C++ development framework for creating cross-platform applications. The purpose of this book is to teach you how to write GUI programs using Qt 4. The book starts with "Hello Qt" and quickly progresses to more advanced topics, such as creating custom widgets and providing drag and drop.

The book is divided into three parts. Part I covers all the fundamental concepts and practices necessary for programming GUI applications using Qt. Knowledge of part alone is sufficient to create useful GUI applications. Part II covers Qt topics in greater depth, and Part III provides more specialized and advanced material. You can read the chapters of Part II and III in any order, but they assume familiarity with Part I. The book also includes several appendices, Appendix A explaining how to download and install the software, Appendix B showing how to build Qt applications and Appendix C introducing Qtambi.

The first Qt 4 edition of the book was built on the Qt 3 edition, although it was completely revised to reflect good idiomatic Qt 4 programming techniques and included new chapters on Qt 4's model/view architecture, the new plugin framework, embedded programming with Qt/Embedded Linux, and a new appendix. This extended and revised second edition has been thoroughly updated to take advantage of features introduced in Qt versions 4.2 and 4.3, and includes new chapters on look and feel customization and application scripting as well two new appendices. The original graphics chapter has been split into separate 2D and 3D chapters, between which they now cover the new graphics classes and Painter's OpenGL back-end. In addition, new material has been added to the database, XML, and embedded programming chapters.

This edition, like its predecessors, emphasizes explaining Qt programming and providing realistic examples, rather than simply rehashing or summarizing Qt's extensive online documentation. Because the book teaches Qt 4 programming principles and practices, readers will be easily able to learn the Qt modules that come out in Qt 4.4, Qt 4.5, and later Qt 4.x versions. If you are using one of these later versions, be sure to read the "What's New in Qt 4.x" documents in the reference documentation to get an overview of the new features that are available.

Matthias Ettrich
Berlin, Germany
November 2007
