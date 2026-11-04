
Possible without the wonderful collaboration I had with Ritchie Houtmeyers (remember the countless hours spent in our server room office?) and Ricardo Noulez. Big thanks go to Bart Vande Ghinste for giving me a crash course in COM+.

Over the years, I've had the honor to interact with a large number of community members at various conferences. Listing all of them would be a Herculean task, so I won't even attempt to do so. I want to mention a few, though. First of all, thanks to the Belgian developer evangelism team for their relentless support over the years. Gerd De Bruycker and Tom Mertens, you've done a great job. Today's community is in great hands with Katrien De Graeve, Hans Verbeeck, and Arlindo Alves. Hans De Smaele, you continue to be my ongoing source of debugging and bit-twiddling inspiration. Finally, and sadly enough, this list wouldn't be complete without taking a moment to remember the late David Bosshmans and Patrick Tisseghem, who passed away suddenly. We miss you guys!

My Redmond-based Microsoft Corporation career started in October 2007, thanks to Scott Guthrie's mail through my blog, asking me to interview with the company. Ultimately, I ended up working on Windows Presentation Foundation's AppModel team, where I felt welcome from day one. In particular, I want to thank my first office mate, Chango Valtchev, for the countless hours he spent bringing me up to speed in the codebase, sharing tons of debugging insights, and sharing epic hikes. My first couple of managers, Grzegorz Zygmunt and Adam Smith, have been great in helping me shape my early career, while also accommodating my speaking engagements abroad.

As I began writing this book in 2009, many of my colleagues were put to the test. My office mates Mike Cook and Eric Harding had to endure the most boring stories on various language constructs, generated IL code, functional programming adventures, and ways to (ab)use the C# programming language. Benjamin Westbrook, with whom I've worked for several months, underwent a similar ordeal during lunchtimes. I have to thank Ben for sharing the things he enjoys most when reading technical books; I hope you find some of your stylistic ideas here and there throughout the book. Patrick Finnigan deserves a special mention here, too. He's a great colleague who has "had my back" with regard to work our team has been doing. He has also provided invaluable technical and stylistic feedback about this book, making it better in the process. Thanks a lot!

Thanking all the other Windows Presentation Foundation colleagues I've worked with and who gave me various technical insights would take up way too much space. Instead, here's a sampling of folks I'm very grateful to have worked with: Adam, Alik, Andre, Dwayne, Joe, Eric, Matt, Saied, Zia. Thanks so much!

While on this writing adventure, I transitioned to the Cloud Programmability Team. Thanks to Erik Meijer for taking me on board into the oasis he's created for innovative and creative ideas and for allowing me to work on one of my key passions: LINQ. My colleagues Danny Van Velzen, Jeffrey Van Gogh, Mark Shields, and Wes Dyer have been fantastic with bringing me up to speed. Endless technical discussions were a tremendous source of inspiration that contributed directly to this book's contents. This is also the right spot to thank my professor Raymond Boute. It turns out Erik and I caught the passion for functional programming from the same professor (although a few decades apart).

I can’t thank the Sams team enough, in particular Neil Rowe for his incredible patience with me. Even though I always knew writing this book was going to be a huge task, lots of unexpected twists made the schedule more challenging than anticipated. Combine this with an ever-growing page count and changing table of contents, and I’m very grateful I could write the book I think is right for a C# programmer audience, with virtually no constraints. I also want to thank the technical team for leading the way through new authoring and publication software and assisting with my numerous technical requests. A special word of thanks goes to the technical reviewer, Doug Holland, and various other team members who participated in various reviews. Writing a book is not only about teaching your readers, it’s also a lot about learning things yourself (including some of the English language, thanks Keith!).

None of this book would exist if not for the wonderful C# language and its designers. I want to thank Anders Hejlsberg and the entire language design team for giving us the most popular .NET language out there. This big thank you also applies to the CLR team for bringing a managed runtime to a wide variety of platforms. Internal resources, in particular on our C# discussion list, have provided valuable insights.

Last but not least, I want to thank the waiters and waitresses in various downtown Bellevue restaurants for tolerating my regular book-writing presence, as I hid behind a laptop screen and asked for endless soda refills.

## We Want to Hear from You!

As the reader of this book, you are our most important critic and commentator. We value your opinion and want to know what we're doing right, what we could do better, what areas you'd like to see us publish in, and any other words of wisdom you're willing to pass our way.

As an executive editor for Sams Publishing, I welcome your comments. You can email or write me directly to let me know what you did or didn't like about this book—as well as what we can do to make our books better.

- Please note that I cannot help you with technical problems related to the topic of this book. We do have a User Services group, however, where I will forward specific technical questions related to the book.

When you write, please be sure to include this book's title and author as well as your name, email address, and phone number. I will carefully review your comments and share them with the author and editors who worked on the book.

Email: feedback@samspublishing.com

Mail:
Neil Rowe
Executive Editor
Sams Publishing
800 East 96th Street
Indianapolis, IN 46240 USA

## Reader Services

Visit our website and register this book at informit.com/register for convenient access to any updates, downloads, or errata that might be available for this book.

## Introduction

Does the world need yet another book about C#? Very rightfully, you might be asking this question right now (and so did some of my colleagues when I first told them about this book project). In short, what sets this book apart from many others is its in-depth coverage of how things work. Personally, I'm a firm believer in education that stimulates the student's curiosity. That's exactly one of the things this book aims to do.

> The important thing is not to stop questioning. Curiosity has its own reason for existing. One cannot help but be in awe when he contemplates the mysteries of eternity, of life, of the marvelous structure of reality. It is enough if one tries merely to comprehend a little of this mystery every day. Never lose a holy curiosity.
> —Albert Einstein

Understanding how a language brings its features to life is always a good thing, which will help you on many fronts. For one thing, coming up with a proper software design requires a good insight into the "à la carte menu" of language features, so that you pick the ones best suited for the job at hand and those that won't leave you with a bitter after-taste. Also solid knowledge about the language and its caveats is invaluable while debugging your (or someone else's) code. Occasional historical perspectives interwoven throughout this book highlight why the language looks the way it does today.

A tremendous number of .NET libraries have been developed over the years, each addressing specific needs for particular applications. Doing justice to any of those by trying to reduce their coverage to a few tens of pages seems overly optimistic. Moreover, different developers have different needs: Maybe you're in charge of user interface (UI) design or web development, or maybe you specialize in service-oriented architectures or designing a data-access layer. Each of those domains has specific concepts that deserve whole books dedicated to them.

For all those reasons, this book shies away from even attempting such shallow and brief coverage of the .NET Framework. Instead, this book focuses on the common ground where all developers meet, the way they express their thoughts through programming languages. In this book, you get essential insights into the foundations of the platform and one of the most commonly used languages, C#. Armed with this knowledge, you should be able to discover and understand many technologies that build on the platform.

As a concrete example, today's libraries are built using object-oriented programming, so the capabilities of this feature are fully explored. Similarly, recent application programming interfaces (APIs), such as Language Integrated Query, have started to leverage the expressiveness of programming constructs borrowed from the functional world, such as lambda expressions, so we delve into how they work.
