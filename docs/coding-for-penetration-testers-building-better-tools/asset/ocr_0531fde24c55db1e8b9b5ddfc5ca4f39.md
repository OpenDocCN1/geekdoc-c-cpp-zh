the range of attacks we can carry out increases significantly.

One of the stumbling blocks in using PowerShell on a system is dealing with the execution policies that are in place to prevent us from using our scripts in exactly the manner in which we are likely to want to do so. The Restricted, AllSigned, and RemoteSigned policies all place limitations on what we can run on the system in the way of PowerShell scripts, largely revolving around where and how they are signed. Ideally, we would like to do to Unrestricted, allowing us to do anything, but this requires changes to the system that we may not be able to make. Unfortunately, based on the code from Peters, Kelley, and Kennedy, we can bypass these policies with relative ease.

Getting into the system to execute our PowerShell code may may not present us with a challenge, depending on the particular operating system in use, the version, and the patch level. There are many common exploits that often go unpatched on Windows systems, as well as a plethora of weak places that we might check for a way in. One option is to use WinRM to remote management, and we can interact with it from Kali using Python.

Once we have gained access to the system, we can put PowerShell to a number of penetration testing uses. We can take control of the processes on the system in order to start or stop those that the system is running, so we can ease our penetration testing efforts. We can interface with the event logs in order to read or manipulate them. We can tweak the Registry, adding, deleting, or changing portions of it. We can get or send files over the network. The possibilities are nearly limitless when we have administrative access to a Microsoft system.

Last but not least, we can use Metasploit to interface with PowerShell. There are several great modules that allow us to spawn shells and make use of some of the code through Metasploit that we discussed using manually in this chapter.

# References

+   1. DEF CON Communications, Inc. DEF CON 18 media archives [Online]. defcon.org.