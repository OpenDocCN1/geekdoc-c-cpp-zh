the “JavaScript core skills” section of Opera’s excellent Web Standards Curriculum.³ Should you ever need even more intricate, implementation-level details, you could then head to either the official specs of the language or one of the massive “bible” books such as David Flanagan’s JavaScript: The Definitive Guide [Fla06].

This book aims to provide you with quick yet qualitative solutions to common client-side JavaScript-based tasks, from low-level stuff (such as getting a reference to a DOM element) to intricate features (such as Ajax-based autocompletion). This means we’ll tackle JavaScript, CSS, the DOM, Ajax, JSON, and more. We won’t go deep into the server side; this book is mostly on the client side of things (most often the browser). You’ll encounter a couple of tiny PHP scripts along the way, for illustration purposes, but you could write your server side any way you like—including in JavaScript, for instance, with Node!

It’s not just for copying and pasting, either. The text for each task takes care to highlight the key concepts, the potential gotchas, and the technical tricks you should take away from the task. Ultimately, you should step away from this book as a better JavaScript programmer.

# This Book and JavaScript Libraries

Let’s speak plainly here. If you’re doing any sort of nontrivial JavaScript programming and you’re not relying heavily on good, established frameworks for it, You’re Doing It Wrong. On the browser side, effectively pulling off web page scripting is a challenge. You face obstacles from all sides: DOM inconsistencies, faulty language implementations, CSS quirks, weird Ajax bugs, and more. On the server side, once you have a runtime ready, you still face the enormous task of putting together the basic bricks of an application server such as a datastore, a network stack, a module system, and so on.

Fortunately, great people already solved these challenges for you. There’s a wealth of options, too, especially on the client side; take a look at Appendix C, on page 116, for details on the main JavaScript frameworks.

Because any competent and pragmatic JavaScript developer will rely on one or more good frameworks, this book takes care to illustrate all the major client-side frameworks in what I think of as “basic” tasks. I selected Prototype, jQuery, MooTools, YUI, Dojo, and ExtJS, which should cover most of the “developer mind share” in this business.

> 3. http://www.opera.com/company/education/curriculum/