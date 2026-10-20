+   10. Modify the script in Problem 6 so that it removes all zero-length ordinary files in the directory passed as an optional argument. If you don’t specify the directory argument, the script uses the present working directory as the default argument. Do the appropriate error checking.
+   
+   11. Run the script in `if_demo2` in Section 12.6.1 with `if_demo2` as its argument. Does the output make sense to you? Why or why not?
+   
+   12. Write a shell script that takes a list of login names on your computer system as command line arguments and displays these login names and full names of the users who own these logins (as contained in the `/etc/passwd` file), one per line. If a login name is invalid (i.e., not found in the `/etc/passwd` file), display the login name but nothing for the full name. The format of the output line is `login name: username`.
+   
+   13. What happens when you run a stand-alone command enclosed in back quotes (grave accents), such as `date`? Why?
+   
+   14. What happens when you type the following sequence of shell commands?
+      a. `name=date`
+      b. `$name`
+      c. ``$name``
+   
+   15. Look at your `~/.profile` and `/etc/profile` files and list the environment variables that are exported along with their values. What is the purpose of each variable?

You have written three Bash scripts and placed them in files called **script1**, **script2**, and **script3**. The three scripts are placed in your `~/linux2e/ch12` directory. In the body of script3, you use script1 and script2. Suppose you run script3 and get error messages as shown in the following session.

```
```text
$ ./script3
./script3: line 4: script1: command not found
./script3: line 5: script2: command not found
$
```
```

Describe two methods that may be used to remove these error messages and enable script3 to work correctly by using script1 and script2.

+   16. Write a Bash script that takes a list of login names as its arguments and displays the number of terminals that each user is logged on to in a LAN environment.
+   
+   17. Write a Bash script **domain2ip** that takes a list of domain names as command line arguments and displays their IP addresses. Use the `nslookup` command. The following is a sample run of this program:

```
```text
$ domain2ip usc.edu up.edu redhat.com
Name: usc.edu
Address: 128.125.253.136
Name: up.edu
Address: 64.251.254.23
Name: redhat.com
Address: 209.132.183.105
$
```
```

+   18. Modify the script in the **case_demo** file in Section 12.6.6 so that it allows you to try any number of options and quits only when you use the q option.
+   
+   19. Write a Bash script that displays the following menu and prompts you for one-character input to invoke a menu option, as follows:
+      a. List all files in the present working directory
+      b. Display today’s date and time
+      c. Invoke the shell script for Problem 14