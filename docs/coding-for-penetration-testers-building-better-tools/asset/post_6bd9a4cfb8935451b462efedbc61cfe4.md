
argument from the command line.

-   We may want to search for multiple file types at once, such as PDF, DOC, and XLS. We should be able to handle these through additional arguments and a bit more looping to work through each file type.
-   We have very limited usage for exiftool presently. However, we could expand the regex in our if statement to include more of the file types that exiftool can handle (quite a lot, actually).
-   We are presently dumping our downloaded files in the directory from which the script is running. It would be nice to put these in their own directory, or perhaps in /tmp.
-   The series of splits that pulls out the useful portion of the URL from the Google listing is very fragile and skips some entries entirely to an empty $url variable indicating that the parsing failed. A little work on this portion could easily make it more robust.

Our example here works reasonably well and serves to illustrate some of the things we can do with the metadata in various files and how we might go about finding it.

# Summary

Information gathering can potentially be of great use to us in the case of a penetration test. It can enable us to collect information on the people, system, and environments which are our targets, and based on this information, to attack them. There are many potential uses for the information we have harvested, but two of the primary purposes to which we might put such information in social engineering efforts and in footprinting the target or targets of our

One of the great potential sources of information we have access to is Google. Searches conducted in Google's massive indexes can return specific information on people, equipment, documents, and files from which to harvest metadata, and all manner of other interesting information, provided we know how to conduct these searches properly. Additionally, we can apply automation to our efforts to ease this task.

As we discussed in Chapter 3, Introduction to Perl, Perl is a wonderful tool to use for parsing text. We can also use Perl to automate the navigation and search of Web pages or applications, saving ourselves a great deal of work in the process. We can do quite a bit with the various Web-oriented Perl modules to automate moving through, parsing, and interacting with the Web.

The metadata, or data about, that is attached to nearly all documents, files, visual media, and other structures intended for digital storage of information, can be invaluable to us in the course of a penetration test. Metadata can provide us with usernames, system paths, network server names and paths, deleted sensitive data, and all manner of such interesting items. Such information can often be easily recovered from documents through the use of utilities as strings, or through the use of similar searching tools.

# References

- 1. WorldWideWebSize.com, the size of the World Wide Web (The Internet) [Internet]. Available from: http://www.worldwidebsize.com/ (cited 11.12.15).
- 2. Google Hacking Database, GHDB, Google Dorks [Internet]. Available from: https://www.exploit-db.com/google-hacking-database/ (cited 11.12.15).
- 3. Andy Lester, search.cpan.org [Internet]. Available from: http://search.cpan.org/~petdance/ (cited 11.12.15).

> ¹https://www.exploit-db.com/google-hacking-database.
²http://www.googleguide.com/

# CHAPTER 9

# Exploitation scripting

# Abstract

The ability to use and build exploits is what penetration tests apart from vulnerability scans. This chapter works through building a simple exploit from scratch using Python. Once Python has squeezed the application to submission and returned us a shell, we move to Ruby to make it repeatable and more powerful by converting it to a Metasploit module. After exploring the world of binary exploitation, this chapter moves into Web application testing and investigates how to deal with Remote File Inclusion (RFI) vulnerabilities and Cross-Site Scripting (XSS) vulnerabilities. This chapter walks through using the RFI vulnerabilities and leveraging the shells that were created in Chapter 5. Introduction to Web Scripting with PHP, to go from Web vulnerability to command line, and ends with building additional scripts to steal data using XSS.

# Keywords

Exploitation; exploits; Python; Web; Ruby; RFI; XSS

# INFORMATION IN THIS CHAPTER

- Building Exploits With Python
- Creating Metasploit Exploits
- Exploiting PHP Scripts
- Cross-Site Scripting

# Introduction

Penetration testers must understand how to build exploits with scripting languages in order to apply them effectively in a practical context. Thanks to its network libraries and ability to quickly prototype code, Python is a popular language for building Proof of Concept (POC) exploits. This chapter starts by outlining the steps for building a POC exploit for a sample Linux binary. Long strings submitted as data will cause this application to crash in an exploitable manner; therefore, the chapter examines the exploit creation process from first crash to a working exploit, explaining how to set up the first crash, using various helper scripts, control EIP, add shellcode, and get the shell. Next, it discusses how to convert the Python script to a more flexible Metasploit module in Ruby. The chapter concludes with a detailed discussion of different styles of Web attacks using PHP.

Now that we have been introduced to Python and PHP in Chapters 2 and 5, Introduction to Python and Introduction to Web Scripting with PHP, let's take a look at how to take our base penetration testing skills to the next level. While many of the exploits we will use already built for us, sometimes we will want to go above and beyond the basics. Whether it is to include a new payload in an or fix a broken exploit, we want to understand the process of building exploits with scripting languages in order to apply them effectively in a practical context.

# Building Exploits With Python

Python is a popular language for building Proof of Concept (POC) exploits. Search for Python on exploit-db.com, a popular online database containing exploits for penetration testers, for examples. Python's network libraries and ability to quickly prototype code are main reasons for its popularity as a language. In this section we will build a POC exploit for a sample Linux binary. Long strings submitted as data will cause this application to crash in an exploitable manner; we will examine the exploit creation process from first crash to a working exploit.

# Setting Up

For this exercise we be using Kali Linux. By default, Linux has a number of protections including address randomization, nonexecutable stack, and a stack canary. In order to make this sample exploit work, we are going to have to disable a few of these things for our sample application.

To begin with, we need to disable stack randomization. This is a setting that can be manipulated through the proc filesystem. By issuing the command `echo 0 >/proc/sys/kernel/randomize_va_space`, the Address Layout Randomization will be disabled. This does not persist across a reboot, make sure to turn this off each time or you add the line `kernel.randomize_va_space = 0` to the file /etc/sysctl.conf.

We are going to create our vulnerable program. To do this, copy the following code to a file named vuln.c:

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <errno.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <arpa/inet.h>
// Returns the value of ESP
unsigned long getsesp()
{
    asm ("mov %esp, %eax");
}
// Vulnerable function that will crash if mystr is big
void crash(char *mystr, int myfd)
{
    char buf[256];
    // send the message back to the client
    send(myfd, mystr, strlen(mystr), 0);
    // perform the memory copy that will overwrite EIP
    memcpy(buf, mystr, strlen(mystr));
}
int main()
{
    int fd;
    struct sockaddr_in self;
    char buf[2048];
    // Make a new socket
    if (fd = socket(AF_INET, SOCK_STREAM, 0)) < 0 )
```
