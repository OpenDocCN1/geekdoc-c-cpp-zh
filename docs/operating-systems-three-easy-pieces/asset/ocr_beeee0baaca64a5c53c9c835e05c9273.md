# 48 INTERLUDE: PROCESS API

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <fcntl.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    int rc = fork();
    if (rc < 0) {
        // fork failed
        fprintf(stderr, "fork failed\n");
        exit(1);
    } else if (rc == 0) {
        // child: redirect standard output to a file
        close(STDOUT_FILENO);
        open("/.p4.output", O_CREAT|O_WRONLY|O_TRUNC, S_IRWXU);

        // now exec "wc"...
        char *myargs[3];
        myargs[0] = strdup("wc"); // program: wc (word count)
        myargs[1] = strdup("p4.c"); // arg: file to count
        myargs[2] = NULL; // mark end of array
        execvp(myargs[0], myargs);
    } else {
        // parent goes down this path (main)
        int rc_wait = wait(NULL);
        return 0;
    }
}
```

> Figure 5.4: All Of The Above With Redirection (p4.c)

# 5.5 Process Control And Users

fork(), exec(), and wait(), there are a lot of other interfaces for interacting with processes in UNIX systems. For example, the kill() call is used to send signals to a process, including directives to pause, die, and other useful imperatives. For convenience, in most shells, certain keyboard combinations are configured to deliver a specific signal to the currently running process; for example, control-s sends a SIGINT (interrupt) to the process (normally terminating it) and control-z sends a SIGSTOP (stop) signal pausing the process in mid-execution (you can resume it with a command, e.g., the fg built-in command found in many shells).

The entire subsystem provides a rich infrastructure to deliver external events to processes, ways to receive and process those signals within individual processes, and ways to send signals to individual processes as well as entire process groups. To use this form of com

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG