# INTERLUDE: PROCESS API

> TIP: GETTING IT RIGHT (LAMPPSON'S LAW)
As Lampson states in his well-regarded “Hints for Computer Systems Design” [L83], **Get it right**. Neither abstraction nor simplicity is a subtitle for getting right. Sometimes, you just have to do the right thing, and when you do, it is better than the alternatives. There are lots of ways to design APIs for process creation; however, the combination of `fork()` and `exec()` are simple and immensely powerful. Here, the UNIX designers got it right. And because Lampson often “got it right”, we name the law in his honor.

executable and overwrites its current code segment (and static data) with it; the heap and stack and other parts of the memory space of the program are re-initialized. Then the OS runs that program, passing in any arguments the argv of that process. Thus, it does not create a new process; rather, it transforms the currently running program (formerly p3) into a different running program (wc). After the exec() in the child, it is almost as if successful call to exec() never returns.

# 5.4 Why? Motivating The API

Of course, one question you might have: why we would build such an interface to what should be the act of creating a new process? Well, as it turns out, the separation of fork() and exec() is essential in building a UNIX shell, which lets the shell run after the call to fork() but before the call to exec(); this code can alter the environment of the out-to-be-run program, and thus enables a variety of interesting features to be readily.

The shell is just a user program. It shows a prompt and then waits for you to type something into it. When you type a command (i.e. the name of an executable program, plus arguments) into it; in most cases, the shell figures out where in the file system it resides, calls fork() to create a new process to run the command, calls some variant of exec() to run the command, and waits for completion by calling wait(). When the child completes, the shell returns from wait() and prints a prompt, ready for your next command.

The separation of fork() and exec() allows the shell to do a whole bunch of things really easily. For example:

```
prompt> p3.c > newfile.txt
```

^And there are lots of shells; tsch, bash, and zsh to name a few. You should pick one, read its man pages, and learn more about it; all UNIX experts do.

OPERATING SYSTEMS
[VERSION 1.01]

WWW.OSTEP.ORG