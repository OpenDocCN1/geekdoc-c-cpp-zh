21. What is the difference between the following commands?
a. grep "John Doe" Students > /dev/null 2>&1
b. grep "John Doe" Students 2>&1 > dev/null

22. Give a command for displaying the contents of (the files’ names in) the current directory, with three files per line.

23. Give a command that reads its input from a file called Phones, removes unnecessary spaces from the file, sorts the file, and removes duplicate lines from it.

24. Repeat Problem 23 for a version of the file that has unnecessary spaces removed from the file but still has duplicate lines in it.

25. What do the following commands do?
a. uptime | cat - who.log >> system.log
b. zcat secret_memo.Z | head -5

26. Give a command that performs the task of the following command but with the diff command running on the machine called server: ssh server cat ~/ research/pvm/datafile.server | diff datafile -

27. Give a command for displaying the lines in a file called employees that are not repeated. What is the command for displaying repeated lines only?

28. Give a command that displays a long list for the most recently created directory.

29. Create a FIFO, called myfifo1. What are the default access privileges set for it? Create a FIFO, myfifo2, with read and write access privileges for everyone. Show your commands and their output for performing these tasks.

30. Give a set of commands for producing the output of the session given in Section 9.15. Your command sequence should ensure that the order of output is always the following: the status of all the processes running on the system, the number of daemons running on the system, and the total number of processes running on the system.

31. The number of files a process can open simultaneously on a Linux system is dependent on the size of the per-process file descriptor table on the system. Use a shell command with the features discussed in this chapter to display the value of the NR_OPEN variable in the /usr/include/linux/limits.h file. Show your command and its output and explain your answer.
Hint: Look for a symbolic constant defined in the /usr/include/linux/limits.h file.

32. How much data can a pipe store on your system? Use a shell command to obtain your answer. What command did you use? Show the command and its output.
Hint: Look for a symbolic constant defined in the /usr/include/linux/limits.h file.

33. What is the output of the following command? Give reasons for your answer.
cat file1 file2 |& grep "John Doe" | sort |& wc -l

34. What is the purpose of the following command?
cat /usr/include/limits.h | nl | grep NR_MAX

35. What do the following commands do?
a. mail mike@somewhere.org < to_do
b. cat Phones | sort | uniq | pr | lpr

36. The ps -e command displays information about all the processes running on your system. These processes include multiple instances of some processes such as systemd and sshd. Show a command that displays the number of unique processes running on the system.

# Advanced Questions and Problems

37. What does the following command do? Clearly explain the purpose of every component and argument of the find and xargs commands.
find ~ 2> /dev/null -size +2G -print0 | xargs -0 -I '{}' mv '{}' ~/bigfiles