```
    istr >> *value;
    return !istr ? UNKNOWN : STOP;
    }

    istringstream istr(line->c_str());
    istr >> *value;
    if (istr)
    {
        getline(istr, *line);
        return TEXT;
    }

    return UNKNOWN;
    }
```

All other input sensed by d_select is created by child processes. Because d_select's readFd member returns the corresponding input file descriptor, this descriptor can be passed to processChild. Using a IFdStreambuf (see section 23.1.2.1), its information is read from an input stream. The communication protocol used here is rather basic. For every line of input sent to a child, the child replies by sending back exactly one line of text. This line is then read by processChild:

```
void Monitor::processChild(int fd)
{
    IFdStreambuf ifdbuf(fd);
    istream istr(&ifdbuf);
    string line;

    getline(istr, line);
    cout << d_child[fd]->pid() << ": " << line << '\n';
}
```

The construction d_child[fd]->pid() used in the above source deserves some special attention. Monitor defines the data member map<int, shared_ptr<Child>> d_child. This map contains the child's order number as its key, and a (shared) pointer to the Child object as its value. A shared pointer is used here, rather than a Child object, since we want to use the facilities offered by the map, but don't want to copy a Child object time and again.

# **23.2.7.6 The class 'Monitor': example**

Now that run's implementation has been covered, we'll concentrate on the various commands users might enter:

+   - When the start command is issued, a new child process is started. A new element is added to d_child by the member createNewChild. Next, the Child object should start its activities, but the Monitor object can not wait for the child process to complete its activities, as there is no well-defined endpoint in the near future, and the user probably wants to be able to enter more commands. Therefore, the Child process must run as a *daemon*. So the forked process terminates immediately, but its own child process continues to run (in the background). Consequently, createNewChild calls the child's fork member. Although it is the child's fork function that is called, it is still the monitor program wherein that fork function is called. So, the *monitor* program is duplicated by fork. Execution then continues:
+     - At the Child's parentProcess in its parent process;
+     - At the Child's childProcess in its child process
+   
+   As the Child's parentProcess is an empty function, returning immediately, the Child's parent process effectively continues immediately below createNewChild's cp->fork() statement.