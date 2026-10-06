
operating system behind its stylish interface and is compatible with many areas with similar UNIX- and Linux-derived operating systems, including the text-based shells it uses.

## C-shell-compatible shells

The C shell, commonly known as csh, is written in the C programming language and uses a scripting style generally similar to the C programming language. Csh was created with an emphasis on use at the command line. It provides features to aid in such efforts, such as command history and filename completion, functions much rarer in the world of shells when it was developed. Due to differences in the way the shell functions and the way scripts are written, csh is almost entirely incompatible with shells outside of those immediately related to it.

A descendant of csh, the TENEX C shell, otherwise known as tcsh, was released by Ken Green in 1983. Ultimately, tcsh is csh with the added or enhanced features for command history, editing, and filename completion merged in. For the systems that ship with a csh-like shell installed by default, we are likely to find that this shell is actually tcsh, as this is the most actively developed and maintained shell in the C-shell family at this point.

## Bourne-compatible shells

The Bourne shell, often called simply sh, was developed by Stephen Bourne in the late 1970s, and is a common ancestor of other shells, including the Bourne-again shell, K shell, and Z shell, just to name a few. Among these shells, we can find a variety of common features.

The Korn shell, named for its developer, David Korn, was developed at Bell Labs in the early 1980s. The Korn shell, commonly called ksh, supports some handy programming features, such as the ability to perform floating-point math, and the use of more complex data structures than some of the other shells allow. While ksh does indeed support features that might allow for easier or more efficient development, it is not as commonly found on UNIX-like systems, and we are less likely to find it in place as a default shell than we might be to find one of the other Bourne variants, such as bash.

The Z shell, referred to as zsh, is frequently considered to be the most feature-rich among the Bourne-like family of shells. Zsh was developed in the early 1990s by Paul Falstad at Princeton University. Falstad incorporated a great many interesting features when creating zsh, including enhanced command completion, ability to add modules for additional features such as those needed for networking or more advanced mathematics, and the ability to make use of enhanced and more complex data structures for programming.

The Bourne-again shell, commonly referred to as bash, was developed by Brian Fox in the late 1980s for use in the GNU Project.¹ Bourne-again is a reference to the Bourne shell, as we discussed earlier in this section. Ultimately, the bash shell is the text-based shell we will most commonly encounter on a UNIX-like system. Many UNIX and Linux systems (and OS X as well) supply a bash shell as an installation default. We can also find the bash shell ported to Microsoft operating systems, although we are not likely to find it as we are the native text-based shells.

Due to it being such a common shell, the rest of our discussion in this chapter related to UNIX-like shell scripting, and the examples we will develop for such systems, will focus on the use of the bash shell. We can typically find bash on newer OS versions, and Bourne on older ones. While there is no guarantee we will have access to bash on a system in any given penetration testing engagement, the likelihood is much higher than that of finding the other shell already present.

## Other UNIX-like shells

There are a large number of other shells for UNIX-like operating systems we might find on any particular system, ranging from only slightly different, such as the compact BusyBox shell, to truly different altogether, like the goosh shell. For almost any purpose imaginable, we can find a specialized shell or a clone of an existing shell with an altered set of features.

Thankfully, we will also usually find the more common shells present, typically at least two or three varieties on a given system. While some of these other shells might indeed be well suited for some specific purpose, we are often better off sticking with the most commonly deployed and installed shells.

## Working With Shells

Identifying the shell we are in by sight can be tricky. Since they all behave differently, knowing which shell we are dealing with is important. A number of features may be different among the shells: the way they generate random numbers, the built-in commands that are or are not present, the environment variables set, and many more.

Thankfully, there is a simple and sure command we can use to identify the shell we are operating in, this being `ps -p $$`. By executing this command, we are asking for a list of processes by process ID (`-p`) where the process ID matches our current process (`$$`), namely the shell we are presently using. We can see an example of this as we move between several different shells in Fig. 1.2.

```
root@mostdefinitelynotkali: ~/Desktop
File Edit View Search Terminal Help
root@mostdefinitelynotkali:~/Desktop# ps -p $$
PID TTY       TIME CMD
7951 pts/0    00:00:00 bash
root@mostdefinitelynotkali:~/Desktop# 
```

## FIGURE 1.2 Identifying the shell in use.

We can also easily enter a new shell, simply by issuing the shortened name of the shell as a command. For example, to enter the C shell, we issue the csh command.

## Warning

When working with shells, entering a new shell is actually adding another layer of shell.

## Bash Basics

We need a few basic items to get started with. First, we need an environment with bash shell. As we discussed throughout the chapter so far, we will likely find present most UNIX and Linux distributions, as well as OS X. We may also find on Windows in some cases, a topic we will return to later.

Second, we need a text editor. A number of text editors are perfectly suited for creating scripts, from text-based editors such as vi and Emacs, to graphical editors such as gedit. Which editor to use is really a matter of personal preference, but for sake of consistency we will stick to gedit, as shown in Fig. 1.3.

![](img/42f332b2adf7dab7e681e5d6cdd2074c_33_0.png)

## FIGURE 1.3 The gedit Editor.

## Hello World

We will jump right into the, then go back through and examine the. Open a new file in gedit, and enter the following:

```
#!/bin/bash
echo "Hello World"
```

Now we want to save the file somewhere convenient, such as the root of our home directory, or on our desktop. We can do this in gedit by clicking Save, navigating to where we want to save the file, inputting a name in the field (helloworld.sh), and then clicking Save again.

In order to run the script we just created, we need to make it executable. We can do this by issuing the command chmod u+x helloworld.sh from the command line while we are in the directory containing the file. This command will add execute permissions for the user that owns the file.

Now that we have created the file and made it executable, we simply need to run it. We can do this with the command ./helloworld.sh. The / in front of the command tells the shell we should be executing this script named helloworld.sh that might exist elsewhere in the file system.

If everything went well, we should see output similar to Fig. 1.4.
