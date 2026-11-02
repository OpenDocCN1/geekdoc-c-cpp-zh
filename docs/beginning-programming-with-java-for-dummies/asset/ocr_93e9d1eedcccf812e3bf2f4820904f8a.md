processor, or one of your own Java programs) is either a 32-bit program or a 64-bit program. You may run a 32-bit web browser on a 64-bit operating system running on a 64-bit computer. Alternatively, you may run a 32-bit browser on a 32-bit operating system on a 64-bit computer. (See the figure that accompanies this sidebar.)

+   - If you run a 32-bit operating system, you run only 32-bit software.
+   - If you run a 64-bit operating system, you probably run some 32-bit software and some 64-bit software. Most 32-bit software runs fine on a 64-bit operating system.

![](bbox=[0.28, 0.33, 0.75, 0.7])

When a website makes you choose between 32-bit and 64-bit software versions, the main consideration is the word length of your operating system, not the word length of your computer's circuitry. You can run a 32-bit word processor on a 64-bit operating system, but you can't run a 64-bit word processor on a 32-bit operating system (no matter what word length your computer's circuitry has). Choosing 64-bit software has one big advantage — namely, that 64-bit software can access more than three gigabytes of a computer's fast random access memory. And in my experience, more memory means faster processing.

How does all this stuff about word lengths affect your Java and Eclipse downloads? Here's the story:

+   - On a 64-bit operating system, you might have two versions of the same program. For example, on my Windows computer, I have two versions of Internet Explorer — a 32-bit version and a 64-bit version.
+   - Normally, Windows puts 32-bit programs in its Program Files (x86) directory and puts 64-bit programs in its Program Files directory.
+   - A chain of word lengths is as strong as its weakest link. For example, when I visit http://java.com and click the site's Do I Have Java? link, the answer I get depends on the match between my computer's Java version and the web browser that I'm running. With only 64-bit Java installed