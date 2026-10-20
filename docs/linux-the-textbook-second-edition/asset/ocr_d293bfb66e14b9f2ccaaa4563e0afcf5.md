+   - w: To see who’s logged in
+   - q: To quit this program

```
$ ./case_demo
Use one of the following options:
d: To display today’s date and present time
l: To see the listing of files in your present working directory
w: To see who’s logged in
q: To quit this program

Enter your option and hit <Enter>: d
Thu Jul 13 12:55:25 PKT 2017
```

```
$ ./case_demo
Use one of the following options:
d: To display today’s date and present time
l: To see the listing of files in your present working directory
w: To see who’s logged in
q: To quit this program

Enter your option and hit <Enter>: w
root ttyp1 2017-04-06 18:57
sarwar pts/0 2017-07-13 12:55 (119.160.96.110)
javis tty8 2017-04-12 11:22 (:0)
jacob tty2 2017-04-13 19:07
```

```
$ ./case_demo
Use one of the following options:
d: To display today’s date and present time
l: To see the listing of files in your present working directory
w: To see who’s logged in
q: To quit this program

Enter your option and hit <Enter>: l
case_demo export_demo if_demo2 shift_demo while_demo
display_change_name for_demo1 if_demo3 until_demo
display_name for_demo1 if_demo1 set_demo user_info
```

```
$ ./case_demo
Use one of the following options:
d: To display today’s date and present time
l: To see the listing of files in your present working directory
w: To see who’s logged in
q: To quit this program

Enter your option and hit <Enter>: q
```

From the output of the w option, it seems that davis is using the system through a remote login, most likely through a secure shell (ssh) session. Note that, when you enter a valid option, the expected output is displayed. However, when you enter input that is not a valid option (a in the preceding session), the program does not give you any feedback. The reason is that the case statement matches your input with all the patterns, one by one, and exits when there is no match. We need to modify the script slightly so that when you enter an invalid option, the script tells you so and then terminates. To do so, we add the following code.

```
*)
	echo "Invalid option; try running the program again."
	exit 1
;;
```

We also enhance the script so that uppercase and lowercase inputs are considered to be the same. We use the pipe symbol (|) in the patterns to specify a logical OR operation. The enhanced code and some sample runs are shown in the following session.

```
$ cat case_demo
echo "Use one of the following options:"
echo " d or D: To display today’s date and present time"
echo " l or L: To see the listing of files in your present working directory"
echo " w or W: To see who’s logged in"
echo " q or Q: To quit this program"
echo -n "Enter your option and hit <Enter>: "
read option
case $option in
d|D) date
l|L) ls
w|W) who
q|Q) exit
esac
```