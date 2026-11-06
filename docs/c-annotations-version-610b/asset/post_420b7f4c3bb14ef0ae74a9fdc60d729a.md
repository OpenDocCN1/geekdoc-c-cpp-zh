
```cpp
}
void Pipe::readFrom(int fd)
{
    readOnly();

    redirect(d_fd[READ], fd);
    close(d_fd[READ]);
}
```

- `writeOnly` and two `writtenBy` members are available to configure the writing end of a pipe. The former function is only used to configure the writing end of the pipe. It closes the reading end, and returns a file descriptor that can be used for writing to the pipe:

    ```cpp
    int Pipe::writeOnly()
    {
        close(d_fd[READ]);
        return d_fd[WRITE];
    }
    void Pipe::writtenBy(int fd)
    {
        writtenBy(&fd, 1);
    }
    void Pipe::writtenBy(int const *fd, size_t n)
    {
        writeOnly();

        for (size_t idx = 0; idx < n; idx++)
            redirect(d_fd[WRITE], fd[idx]);

        close(d_fd[WRITE]);
    }
    ```

    For the latter member two overloaded versions are available:

    - `writtenBy(int fd)` is used to configure *single* redirection, so that a specific file descriptor (usually `STDOUT_FILENO` or `STDERR_FILENO`) can be used to write to the pipe;
    - `writtenBy(int const *fd, size_t n)` may be used to configure *multiple* redirection, providing an array argument containing file descriptors. Information written to any of these file descriptors is actually written to the pipe.

- The class has one private data member, `redirect`, used to set up redirection through the `dup2` system call. This function expects two file descriptors. The first file descriptor represents a file descriptor that can be used to access the device’s information; the second file descriptor is an alternate file descriptor that may also be used to access the device’s information. Here is `redirect`’s implementation:

    ```cpp
    void Pipe::redirect(int d_fd, int alternateFd)
    {
        if (dup2(d_fd, alternateFd) < 0)
            throw "Pipe: redirection failed";
    }
    ```

Now that redirection can be configured easily using one or more `Pipe` objects, we’ll use `Fork` and `Pipe` in various example programs.

## 23.2.6 The class ‘ParentSlurp’

The class `ParentSlurp`, derived from `Fork`, starts a child process executing a stand-alone program (like `/bin/ls`). The (standard) output of the executed program is not shown on the screen but is read by the parent process.

For demonstration purposes the parent process writes the lines it receives to its standard output stream, prepending line numbers to the lines. It is attractive to redirect the parent’s standard input stream to allow the parent to read the output from the child process using its `std::cin` input stream. Therefore, the only pipe in the program is used as an input pipe for the parent, and an output pipe for the child.

The class ParentSlurp has the following characteristics:

- It is derived from `Fork`. Before starting `ParentSlurp’s` class interface, the compiler must have read `fork.h` and `pipe.h`. The class only uses one data member, a `Pipe` object `d_pipe`.

- As `Pipe’s` constructor already defines a pipe, and as `d_pipe` is automatically initialized by `ParentSlurp’s` default constructor, which is implicitly provided, all additional members only exist for `ParentSlurp’s` own benefit so they can be defined in the class’s (implicit) private section. Here is the class’s interface:

    ```cpp
    class ParentSlurp: public Fork
    {
        Pipe    d_pipe;

        virtual void childRedirections();
        virtual void parentRedirections();
        virtual void childProcess();
        virtual void parentProcess();
    };
    ```

- The `childRedirections` member configures the writing end of the pipe. So, all information written to the child’s standard output stream ends up in the pipe. The big advantage of this is that no additional streams are needed to write to a file descriptor:

    ```cpp
    inline void ParentSlurp::childRedirections()
    {
        d_pipe.writtenBy(STDOUT_FILENO);
    }
    ```

- The `parentRedirections` member configures the reading end of the pipe. It does so by connecting the reading end of the pipe to the parent’s standard input file descriptor (`STDIN_FILENO`). This allows the parent to perform extractions from `cin`, not requiring any additional streams for reading.

    ```cpp
    inline void ParentSlurp::parentRedirections()
    {
        d_pipe.readFrom(STDIN_FILENO);
    }
    ```

- The `childProcess` member only needs to concentrate on its own actions. As it only needs to execute a program (writing information to its standard output), the member can consist of one single statement:

    ```cpp
    inline void ParentSlurp::childProcess()
    {
        execl("/bin/ls", "/bin/ls", 0);
    }
    ```

- The `parentProcess` member simply ‘slurps’ the information appearing at its standard input. Doing so, it actually reads the child’s output. It copies the received lines to its standard output stream prefixing line numbers to them:

    ```cpp
    void ParentSlurp::parentProcess()
    {
    ```

- `Selector()`: the (default) constructor. It clears the read, write, and execute `fd_set` variables, and switches off the alarm. Except for `d_max`, the remaining data members do not require specific initializations:

    ```cpp
    Selector::Selector()
    {
        FD_ZERO(&d_read);
        FD_ZERO(&d_write);
        FD_ZERO(&d_except);
        noAlarm();
        d_max = 0;
    }
    ```

- `int wait()`: this member blocks until the *alarm* times out or until activity is sensed at any of the file descriptors monitored by the `Selector` object. It throws an exception when the `select` system call itself fails:

    ```cpp
    int Selector::wait()
    {
        timeval t = d_alarm;

        d_ret_read = d_read;
        d_ret_write = d_write;
        d_ret_except = d_except;

        d_readidx = 0;
        d_writeidx = 0;
        d_exceptidx = 0;

        d_ret = select(d_max, &d_ret_read, &d_ret_write, &d_ret_except,
                       t.tv_sec == -1 && t.tv_usec == -1 ? 0 : &t);

        if (d_ret < 0)
            throw "Selector::wait()/select() failed";

        return d_ret;
    }
    ```

- `int nReady`: this member function’s return value is only defined when `wait` has returned. In that case it returns 0 for an alarm-timeout, -1 if `select` failed, and otherwise the number of file descriptors on which activity was sensed.

    ```cpp
    inline int Selector::nReady()
    {
        return d_ret;
    }
    ```

- `int readFd()`: this member function’s return value is also only defined after `wait` has returned. Its return value is -1 if no (more) input file descriptors are available. Otherwise the next file descriptor available for reading is returned:

    ```cpp
    inline int Selector::readFd()
    {
        return checkSet(&d_readidx, d_ret_read);
    }
    ```

- `int writeFd()`: operating analogously to `readFd`, it returns the next file descriptor to which output is written. It uses `d_writeidx` and `d_ret_write` and is implemented analogously to `readFd`;

- `int exceptFd()`: operating analogously to `readFd`, it returns the next exception file descriptor on which activity was sensed. It uses `d_exceptidx` and `d_ret_except` and is implemented analogously to `readFd`;

- `void setAlarm(int sec, int usec = 0)`: this member activates `Selector`’s alarm facility. At least the number of seconds to wait for the alarm to go off must be specified. It simply assigns values to `d_alarm`’s fields. At the next `Selector::wait` call, the alarm fires (i.e., `wait` returns with return value 0) once the configured alarm interval has passed:

    ```cpp
    inline void Selector::setAlarm(int sec, int usec)
    {
        d_alarm.tv_sec  = sec;
        d_alarm.tv_usec = usec;
    }
    ```

- `void noAlarm()`: this member switches off the alarm, by simply setting the alarm interval to a very long period:

    ```cpp
    inline void Selector::noAlarm()
    {
        setAlarm(-1, -1);
    }
    ```

- `void addReadFd(int fd)`: this member adds a file descriptor to the set of input file descriptors monitored by the `Selector` object. The member function `wait` returns once input is available at the indicated file descriptor:

    ```cpp
    inline void Selector::addReadFd(int fd)
    {
        addFd(&d_read, fd);
    }
    ```

- `void addWriteFd(int fd)`: this member adds a file descriptor to the set of output file descriptors monitored by the `Selector` object. The member function `wait` returns once output is available at the indicated file descriptor. Using `d_write`, it is implemented analogously to `addReadFd`;

- `void addExceptFd(int fd)`: this member adds a file descriptor to the set of exception file descriptors to be monitored by the `Selector` object. The member function `wait` returns once activity is sensed at the indicated file descriptor. Using `d_except`, it is implemented analogously to `addReadFd`;

- `void rmReadFd(int fd)`: this member removes a file descriptor from the set of input file descriptors monitored by the `Selector` object:

    ```cpp
    inline void Selector::rmReadFd(int fd)
    {
        FD_CLR(fd, &d_read);
    }
    ```

- `void rmWriteFd(int fd)`: this member removes a file descriptor from the set of output file descriptors monitored by the `Selector` object. Using `d_write`, it is implemented analogously to `rmReadFd`;

- `void rmExceptFd(int fd)`: this member removes a file descriptor from the set of exception file descriptors to be monitored by the `Selector` object. Using `d_except`, it is implemented analogously to `rmReadFd`;
