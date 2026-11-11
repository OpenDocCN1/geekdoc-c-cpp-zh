
You already saw the abbreviation JDK for Java Development Kit. Somewhat confusingly, versions 1.2 through 1.4 of the kit were known as the Java SDK (Software Development Kit). You will still find occasional references to the old term. Up to Java 10, there is also a Java Runtime Environment (JRE) that contains only the virtual machine. That is not what you want as a developer. It is intended for end users who have no need for the compiler.

Next, you’ll see the term Java SE everywhere. That is the Java Standard Edition, in contrast to Java EE (Enterprise Edition) and Java ME (Micro Edition).

You might run into the term Java 2 that was coined in 1998 when the marketing folks at Sun felt that a fractional version number increment did not properly communicate the momentous advances of JDK 1.2. However, since they had that insight only after the release, they decided to keep the version number 1.2 for the *development kit*. Subsequent releases were numbered 1.3, 1.4, and 5.0. The *platform*, however, was renamed from Java to Java 2. Thus, we had Java 2 Standard Edition Software Development Kit Version 5.0, or J2SE SDK 5.0.

Fortunately, in 2006, the numbering was simplified. The next version of the Java Standard Edition was called Java SE 6, followed by Java SE 7 and Java SE 8.

However, the “internal” version numbers are 1.6.0, 1.7.0, and 1.8.0. This minor madness finally ran its course with Java SE 9, when the version number became 9, and then 9.0.1. (Why not 9.0.0 for the initial version? To keep a modicum of excitement, the version number specification requires that trailing zeroes are dropped for the fleeting interval between a major release and its first security update.)

> **NOTE:** For the remainder of the book, we will drop the “SE” acronym. When you see “Java 9”, that means “Java SE 9”.

Prior to Java 9, there were 32-bit and 64-bit versions of the Java Development Kit. The 32-bit versions are no longer developed by Oracle. You need to have a 64-bit operating system to use the Oracle JDK.

With Linux, you have a choice between an RPM file and a .tar.gz file. We recommend the latter—you can simply uncompress it anywhere you like.

Now you know how to pick the right JDK. To summarize:

- You want the JDK (Java SE Development Kit), not the JRE.
- Linux: Pick the `.tar.gz` version.

Accept the license agreement and download the file.

> **NOTE:** Depending on the constellation of the planets, Oracle may offer you a bundle that contains both the Java Development Kit and the NetBeans integrated development environment. I suggest that you stay away from all bundles and install only the Java Development Kit at this time. If you later decide to use NetBeans, simply download it from http://netbeans.org.

### 2.1.2 Setting up the JDK

After downloading the JDK, you need to install it and figure out where it was installed—you’ll need that information later.

- Under Windows, launch the setup program. You will be asked where to install the JDK. It is best not to accept a default location with spaces in the path name, such as `c:\Program Files\Java\jdk-11.0.x`. Just take out the Program Files part of the path name.
- On the Mac, run the installer. It installs the software into `/Library/Java/JavaVirtualMachines/jdk-11.0.x.jdk/Contents/Home`. Locate it with the Finder.
- On Linux, simply uncompress the `.tar.gz` file to a location of your choice, such as your home directory or `/opt`. Or, if you installed from the RPM file, double-check that it is installed in `/usr/java/jdk-11.0.x`.

In this book, the installation directory is denoted as `jdk`. For example, when referring to the `jdk/bin` directory, I mean the directory with a name such as `/opt/jdk-11.0.4/bin` or `c:\Java\jdk-11.0.4\bin`.

When you install the JDK on Windows or Linux, you need to carry out one additional step: Add the `jdk/bin` directory to the executable path—the list of directories that the operating system traverses to locate executable files.

- On Linux, add a line such as the following to the end of your `~/.bashrc` or `~/.bash_profile` file:

  ```bash
  export PATH=jdk/bin:$PATH
  ```

  Be sure to use the correct path to the JDK, such as `/opt/jdk-11.0.4`.
- Under Windows 10, type “environment” into the search bar of the Windows Settings, and select “Edit environment variables for your account” (see Figure 2.1). An Environment Variables dialog should appear. (It may hide behind the Windows Settings dialog. If you can’t find it anywhere, try running `sysdm.cpl` from the Run dialog that you get by holding down the Windows and R key at the same time, and then select the Advanced tab and click the Environment Variables button.) Locate and select a variable named Path in the User Variables list. Click the Edit button, then the New button, and add an entry with the `jdk\bin` directory (see Figure 2.2).

![](img/127bccebb2cfadea3f02579edaad63c3_47_0.png)

Figure 2.1  Setting system properties in Windows 10

Save your settings. Any new “Command Prompt” windows that you start will have the correct path.

Here is how you test whether you did it right: Start a terminal window. Type the line

```text
javac --version
```

and press the Enter key. You should get a display such as this one:

```text
javac 11.0.1
```

## BIO 1113

## Chapter 18: Gene Expression

Gene expression is the process by which information from a gene is used to synthesize a functional gene product, typically proteins. This process involves two main steps: transcription and translation.

**Transcription** is the synthesis of RNA from a DNA template. RNA polymerase reads the template strand and creates a complementary RNA strand. The product of transcription is messenger RNA (mRNA).

- **Initiation**: RNA polymerase binds to the promoter region and unwinds the DNA.
- **Elongation**: RNA polymerase moves along the template strand, adding RNA nucleotides.
- **Termination**: RNA polymerase reaches a terminator sequence, releasing the mRNA.

**Translation** is the synthesis of a polypeptide chain using mRNA as a template. Ribosomes facilitate this process by reading codons on mRNA and matching them with appropriate tRNA molecules carrying amino acids.

| Codon | Amino Acid |
|-------|------------|
| AUG   | Methionine (start) |
| UAA   | Stop codon |
| UAG   | Stop codon |
| UGA   | Stop codon |

The genetic code is degenerate, meaning multiple codons can code for the same amino acid. The reading frame is determined by the start codon AUG, ensuring proper translation of the protein.

Post-translational modifications, such as phosphorylation, glycosylation, and ubiquitination, can alter protein function and localization. These modifications are critical for regulating protein activity.

- 2. Make a directory `javasrc` in your home directory. If you like, you can do this from a terminal window.

  ```bash
  mkdir javasrc
  ```

- 3. Inside the `jdk/lib` directory, locate the file `src.zip`.
- 4. Unzip the `src.zip` file into the `javasrc` directory. In a terminal window, you can execute the commands

  ```bash
  cd javasrc
  jar xvf jdk/lib/src.zip
  cd ..
  ```

> **TIP:** The `src.zip` file contains the source code for all public libraries. To obtain even more source (for the compiler, the virtual machine, the native methods, and the private helper classes), go to http://openjdk.java.net.

The documentation is contained in a compressed file that is separate from the JDK. You can download the documentation from `www.oracle.com/technetwork/java/javase/downloads`. Follow these steps:

- 1. Download the documentation zip file. It is called `jdk-11.0.x_doc-all.zip`.
- 2. Unzip the file and rename the doc directory into something more descriptive, like javadoc. If you like, you can do this from the command line:

  ```bash
  jar xvf Downloads/jdk-11.0.x_doc-all.zip
  mv docs jdk-11-docs
  ```

- 3. In your browser, navigate to `jdk-11-docs/index.html` and add this page to your bookmarks.

You should also install the Core Java program examples. You can download them from `http://horstmann.com/corejava`. The programs are packaged into a zip file `corejava.zip`. Just unzip them into your home directory. They will be located in a directory `corejava`. If you like, you can do this from the command line:

```bash
jar xvf Downloads/corejava.zip
```

### 2.2 Using the Command-Line Tools

If your programming experience comes from a development environment such as Microsoft Visual Studio, you are accustomed to a system with a built-in text editor, menus to compile and launch a program, and a debugger. The JDK contains nothing even remotely similar. You do everything by typing in commands in a terminal window. This sounds cumbersome, but it is
