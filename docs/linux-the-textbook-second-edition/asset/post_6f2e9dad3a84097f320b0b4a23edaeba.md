
as such has the same structured programming capabilities of high-level languages. When you type a command and press <Enter>, the shell interprets and tries to execute the command, assuming that the first word in the command line is the name of the command. A shell command can be built-in or external. The shell has the code for executing a built-in command, but the code for an external command is in a file. To execute an external command, the shell searches several directories, one by one, to locate the file that contains the code for the command. If the file is found, it is executed if it contains the code (binary or shell script). The names of the directories that the shell searches to locate the file for an external command form are known as the search path. The search path is stored in a shell variable called PATH (for the Bourne, Korn, and Bash shells) or path (for the C shell). You can change the search path for your shell by adding new directory names in PATH or by deleting some existing directory names from it.

Several shells are available for you to use. These shells differ in terms of convenience of use at the command line level and features available in their programming languages. The most commonly used shells in a Linux-based system are the Bash and C shells. The Bourne shell is the oldest and has a good programming language. The C shell has a more convenient and rich command-level interface. The Korn shell has some good features of both and is a superset of the Bourne shell.

Certain characters, called shell metacharacters, have special meaning to the shell. Because the shell treats them in special ways, they should not be used in file names. If you must use them in commands, you need to quote them for the shell to treat them literally.

## Questions and Problems

- 1. Create a directory called Linux in your home directory. What command line did you use to do this?
- 2. Give a command line for displaying the files lab1, lab2, lab3, and lab4. Can you give two more command lines that do the same thing? What is the command line for displaying the files lab1.c, lab2.c, lab3.c, and lab4.c? (Hint: use shell metacharacters.)
- 3. Give a command line for printing all the files in your home directory that start with the string memo and end with .ps on a printer called upmpr. What command line did you use to do this?
- 4. Give the command line for nicknaming the command who -H as w. Give both Bash and C shell versions. Where would you put it if you want it to execute every time you start a new shell?
- 5. Type the command man ls > ~/Linux/ls.man on your system. This command will put the man page for the ls command in the ls.man file in your ~/Linux directory (the one you created in Problem 1). Give the command for printing two copies of this file on a printer in your lab. What command line would you use to achieve this printing?
- 6. What is the mesg value set to for your environment? If it is on, how would you turn it off for your current session? How would you set it off for every login?
- 7. What does the command lpr -Pqpr [0-9]*.jpg do? Explain your answer.
- 8. Use the passwd command to change your password. If you are on a network, be aware that you might have to use the yppasswd command to modify your network login password. Also, make sure you abide by the rules set up by your system administrator for coming up with good passwords!
- 9. Using the correct terminology (e.g., command, option, option argument, and command argument), identify the constituent parts of the following Linux single commands.
  
  `ls -la *.exe`
  
  `lpr -Pwpr file27`
  
  `chmod g+rwx *.*`

- 10. View the man pages for each of the useful commands listed in Table 2.3. Which part of the man pages is most descriptive for you? Which of the options shown on each of the man pages is the most useful for beginners? Explain.
- 11. How many users are logged on to your system at this time? What command did you use to discover this?
- 12. Determine the name of the operating system that your computer runs. What command did you use to discover this?
- 13. Give the command line for displaying manual pages for the socket, read, and connect system calls on your system.
- 14. What is a shell? What is its purpose?
- 15. What are the two types of shell commands? What are the differences between them?
- 16. Give the names of five Linux shells. Which are the most popular? What is a login shell? What do you type in to terminate the execution of a shell? How do you terminate the execution of your login shell?
- 17. What shells do you think are supersets of other shells? In other words, which shells have other shells’ complete command sets plus their own? Can you find any commands in a subset shell that are not in a superset shell? Refer to Figure 2.4.
- 18. What is the search path for a shell? What is the name of a shell variable that is used to maintain it for the Bash, C, and Korn shells? Where (i.e., in which file) is this variable typically located?
- 19. What is the search path set to in your environment? How did you find out? Set your search path so that your shell searches your current and your ~/bin directories while looking for a command that you type. In what order does your shell search the directories in your search path? Why?
- 20. What are hidden files? What are the names of the hidden files that are executed when you log on to your Linux systems, and how did you find out this?
- 21. What is a shell start-up file? What is the name of this file for the Bash shell? Where (i.e., in which directory) is this file stored?
- 22. What important features of each shell, as discussed on the manual pages for that shell, seem to be most important for you as either a new, intermediate, or advanced user of Linux? Explain the importance of these features to you in comparison with the other shells available and their features.
- 23. Suppose that your login shell is a C shell. You receive a shell script that runs with the Bourne shell. How would you execute it? Clearly write down all the steps that you would use.

## Advanced Questions and Problems

24. Following is a typical /etc/profile configuration file, this particular one is from a default installation on our Linux Mint 18.2 system:

```
# /etc/profile: system-wide .profile file for the Bourne shell (sh(1)
# and Bourne compatible shells (bash(1), ksh(1), ash(1), ...).

if [ "$PS1" ]; then
    if [ "$BASH" ] && [ "$BASH" != "/bin/sh" ]; then
        # The file bash.bashrc already sets the default PS1.
        # PS1='\h:\w\$ '
        if [ -f /etc/bash.bashrc ]; then
            . /etc/bash.bashrc
        fi
```
```
else
    if [ "`id -u`" -eq 0 ]; then
        PS1='# '
    else
        PS1='$ '
    fi
fi

if [ -d /etc/profile.d ]; then
    for i in /etc/profile.d/*.sh; do
        if [ -r $i ]; then
            . $i
        fi
    done
    unset i
fi
```

Write an explanatory sentence in your own words describing exactly what you consider important lines in the file accomplish, including the comments (the lines that begin with the pound sign #). Examine this file on your Linux system. How does it compare, line-for-line, with the one above? We assume here that, by default, Bash is both the interactive and login shells on your system.

- 25. What is the default umask setting in an ordinary, nonprivileged account on your Linux system, from both a login and a nonlogin shell? Describe in your own words what the umask setting is, and how it is applied to newly created directories and files. Is the umask set in `/etc/profile` on your Linux system? If not, where can the umask be set most effectively on a persistent basis, for a particular single user, in both a login and a nonlogin shell?

- 26. Assume that all users, when they log into your Linux system, have Bash as their default shell. What file sets the shell prompt for them on your Linux system? Is it the file illustrated in Problem 24? Describe the lines in the file that actually specify the shell prompt, and give a short description of the components of those lines. Experiment to find out which file accomplishes the actual shell prompt setting for ordinary users (for both nonlogin and login shells), and write an explicit description of what you have discovered.
  
  Additionally, set the shell prompt for yourself in the current nonlogin shell, so that it contains the following:
  
  A display of just the date/time.
  
  A display of the date and time, hostname and current directory.
  
  A display where the entire prompt is in red text, along with hostname and current directory.
  Then make those changes persistent for yourself in both login and nonlogin shells. Finally, undo the persistent changes.
  
  As a follow-up, design your own shell prompt so that it contains the information you want in a useful display, given your use case(s), and make that designed prompt persistent for yourself on your Linux system.

- 27. Give a sequential list of the exact commands you would use to make the TC shell the default login shell for your user account on your Linux system. Is the TC shell installed by default on your Linux system? If not, how would you install it on a Debian-family or CentOS system? Give the exact commands for installation of not only the TC shell, but any of the other four major Linux shells available.

- 28. Execute all of the compound command examples provided at the Web link https://explain[shell.com/ and then use the output shown to explain all of them in your own words. Try executing the examples with meaningful arguments on your Linux system, if possible.
