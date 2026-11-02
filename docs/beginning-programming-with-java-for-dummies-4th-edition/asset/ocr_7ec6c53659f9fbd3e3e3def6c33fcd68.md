(continued)

on my computer, the Do I Have? link in my 32-bit Firefox browser answers NO working Java was detected on your system. But the same link in my 64-bit Internet Explorer answers You have the recommended Java installed.

On a Mac, Safari and Firefox are 64-bit browsers, but Chrome is a 32-bit browser. So on a Mac, you’re likely to see slightly different behavior when using Firefox versus Chrome.

Here’s the most important thing to remember about word lengths: When you follow this chapter’s instructions, you get Java software and Eclipse software on your computer. Your Java software’s word length

must match your Eclipse software’s word length. In other words, 32-bit Eclipse runs with 32-bit Java, and 64-bit Eclipse runs with 64-bit Java. I haven’t tried all possible combinations, but when I try to run 32-bit Eclipse with 64-bit Java, I see a misleading No Java virtual machine was found error message.

Finally, some websites use unintuitive names for their software downloads. If you see *i365* or *i586* in the name of a download, that usually means 32-bit. If you see *x86* without the number 64 anywhere in a download’s name, that also means 32-bits. If you see *64* in the name (with or without the *x86* designation), that indicates a 64-bit program.

# Finding Java on your computer

Chapter 1 describes the Java ecosystem with its compiler, its virtual machine, and its other parts. Your computer may already have some of these Java gizmos. If so, you can either live with what you already have or add the newest version of Java to whatever is already on your system.

![](bbox=[0.118, 0.661, 0.207, 0.735])

Java’s versions aren’t like indoor cats. They can coexist on the same computer without fighting or hissing at one another. If you have more than one version of Java on your computer, you’re okay. You can even mix 32-bit versions and 64-bit versions on the same computer (as long as you have at least one Java version whose word length matches your Eclipse version). I have three versions of Java on my Windows 8 computer, and I never run into trouble. (Occasionally, I cause my own trouble by confusing one version of Java for another. But this chapter’s “Configuring Java in Eclipse” section helps me sort things out. What would I do without this book by my side?)

To find out what you already have and possibly avoid reinstalling Java, keep reading.

# On Windows 8

In the Start screen, hold down the Windows key while pressing Q. In the resulting search box, type **Programs and Features** and then press Enter. Then proceed to the In All Versions of Windows (XP and Newer) paragraphs.