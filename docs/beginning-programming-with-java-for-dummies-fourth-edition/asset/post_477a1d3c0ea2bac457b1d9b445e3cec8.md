
## Setting Up Java

You can get the latest, greatest versions of Java by visiting www.oracle.com/technetwork/java/javase/downloads. Look for the newest available version of the JDK. Select a version that runs on your computer's operating system. Figure 2-1 shows me clicking a Download JDK button (circa March 2014) at the Oracle website.

![](img/6d9dcff12e52b997f3ad31445b712549_42_0.png)

Figure 2-1: Getting the Java JDK.

If you can't identify the most appropriate Java version or if you want to know what the acronyms JRE and JDK stand for, see the sidebar entitled 'Eenie, meenie, miney mo.'

After you accept a license agreement and click a link to a Java installation file, your computer does one of two things:

- Downloads and installs Java on your system.
- Downloads the Java installation file and saves the file on your computer's hard drive.

If the installation begins on its own, follow the instructions, answer "Yes" to any prompts, and (unless you have good reason to do otherwise) accept the defaults. If the installation doesn't begin on its own, start the installation by double-clicking the downloaded installation file.

### Eenie, meenie, miney mo

The Java Standard Edition download page (www.oracle.com/technetwork/java/javase/downloads) has many options. If you're not familiar with these options, the page can be intimidating. Here are some of the choices on the page:

- **Word length: 32-bit or 64-bit**  
  You may have to choose between links labeled for 32-bit systems and links labeled for 64-bit systems. If you don't know which to choose, start by trying the 32-bit version. (For more information about 32-bit systems and 64-bit systems, see the "How many bits does your computer have?" sidebar.)

- **Java version number**  
  The Java download page may have older and newer Java versions for you to choose from. You may see links to Java SE 7, Java SE 8, Java SE 8u4, and many others. (Numbering such as *8u4* stands for the fourth update to Java 8.) If you're not sure which version number you want, choosing the highest version number is probably safe. Most of this book's examples run on a computer with Java 5 installed. A few examples run only on Java 7, Java 8, or higher.

(J2SE 1.2). Yes, the "Java 2" numbering overlaps partially with the "1.x" numbering. Next come versions 1.3 and 1.4. After version 1.4 comes version 1.4.2 (with intermediate stops at versions like 1.4.1_02). After 1.4.2_06, the next version is version 1.5, which is also known as version 5.0. (That's no misprint. Version 5.0 comes immediately after the 1.4 versions.)

The formal name for version 1.5 is "Java 2 Platform, Standard Edition 5.0." And to make matters even worse, the next big release is "Java Platform, Standard Edition 6" with the "2" removed from "Java 2" and the "0" missing from "6.0." That's what happens when a company lets marketing people call the shots.

More recently, from Java 6 onward, the version numbers settle into a predictable pattern. After Java 6 comes "Java Platform, Standard Edition 7" and "Java Platform, Standard Edition 8" with updates such as "8u02" (meaning "Java 8, update 2").

- **JDK versus JRE**  
  The download page offers you a choice between the JDK (Java Development Kit) and the JRE (Java Runtime Environment). The JDK download contains more stuff than the JRE download. The JRE includes a Java Virtual Machine and the Application Programming Interface (refer to Chapter 1). The JDK includes everything in the JRE, and in addition, the JDK includes a Java compiler (again, refer to Chapter 1).

The Eclipse IDE contains its own Java compiler. So, you can survive by downloading the smaller JRE (avoiding the big JDK download). But I recommend downloading the entire JDK. Why? Because you never know when another compiler (separate from Eclipse) will come in handy. Besides, the installation and configuration of Eclipse on a Mac is convoluted if you haven't installed the full JDK. So, if you want to have a smooth ride, download the JDK instead of the JRE.

By the way, another name for the JDK is the Java SDK — the Java Software Development Kit. Some people still use the SDK acronym, even though the folks at Oracle don't use it anymore. (Actually, the original name was the JDK. Later, Sun Microsystems changed it to the SDK. A few years after that, the captains of Java changed back to the name JDK. This constant naming and renaming drives me crazy as an author.)

- **Java SE versus Java EE versus Java ME**  
  While you wander around, you may notice links labeled Java EE or Java ME. If you know what these are, and you know you need them, by all means, download these goodies. But if you're not sure, bypass both the Java EE and the Java ME links. Instead, follow links to the Java SE (Java Standard Edition).

  The abbreviation Java EE stands for Java Enterprise Edition and Java ME stands for Java Micro Edition. The Enterprise Edition has software for large businesses, and the Micro Edition has software for handheld devices. (Google's Android software bears a passing resemblance to Java's Micro Edition, but in many ways, Android and Java ME are very different animals.) You don't need the Java EE or the Java ME to run any of the examples in this book.

- **Additional Java-related software**  
  You can download Java alone, or you can download Java with Oracle's NetBeans IDE. You can download a collection of demos and samples. You can probably even download Java with fries and a soft drink. You can download plenty of extra stuff, but in truth, all you need is the Java JDK.

- **Installation type**  
  You may be prompted to choose between online installation and offline installation.

  With the offline installation, you begin by downloading a large setup file. The file takes up lots of space on your hard drive (between 30MB and 150MB, depending on what you choose to download). If you ever need to install the JDK again, you have the file on your computer. Until you want a newer version of the JDK, you don't need to download the JDK again.

  Why would anyone want to install the same version of the JDK a second time? Typically, I have two reasons. Either I want to install the software on a second computer, or I mess something up and have to uninstall (and then reinstall) the software.

  With the online installation, you don't download a big setup file. Instead, you download a teeny little setup file. Then you download (and discard) pieces of the big 30MB to 150MB file as you need them. Using online installation saves you many megabytes of hard drive space. But, if you want to install the same version of the JDK a second time, you have to redo the whole surf/click/download process.

processor, or one of your own Java programs) is either a 32-bit program or a 64-bit program. You may run a 32-bit web browser on a 64-bit operating system running on a 64-bit computer. Alternatively, you may run a 32-bit browser on a 32-bit operating system on a 64-bit computer. (See the figure that accompanies this sidebar.)

- If you run a 32-bit operating system, you run only 32-bit software.
- If you run a 64-bit operating system, you probably run some 32-bit software and some 64-bit software. Most 32-bit software runs fine on a 64-bit operating system.

![](img/6d9dcff12e52b997f3ad31445b712549_46_0.png)

When a website makes you choose between 32-bit and 64-bit software versions, the main consideration is the word length of your operating system, not the word length of your computer's circuitry. You can run a 32-bit word processor on a 64-bit operating system, but you can't run a 64-bit word processor on a 32-bit operating system (no matter what word length your computer's circuitry has). Choosing 64-bit software has one big advantage — namely, that 64-bit software can access more than three gigabytes of a computer's fast random access memory. And in my experience, more memory means faster processing.

How does all this stuff about word lengths affect your Java and Eclipse downloads? Here's the story:

- On a 64-bit operating system, you might have two versions of the same program. For example, on my Windows computer, I have two versions of Internet Explorer — a 32-bit version and a 64-bit version.

  Normally, Windows puts 32-bit programs in its Program Files (x86) directory and puts 64-bit programs in its Program Files directory.

- A chain of word lengths is as strong as its weakest link. For example, when I visit http://java.com and click the site's Do I Have Java? link, the answer I get depends on the match between my computer's Java version and the web browser that I'm running. With only 64-bit Java installed
