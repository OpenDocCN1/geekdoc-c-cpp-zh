enabled, and in most cases they will be a great help to find the reason for the crash. However, this requires that the crashing situation is reproducible and that the program in slower debug mode reaches the critical section in reasonable time.

# 1.6.2 Exceptions

In the preceding section, we looked at how assertions help us detect programming errors. However, there are many critical situations that we cannot prevent even with the smartest programming, like files that we need to read but which are deleted. Or our program needs more memory than is available on the actual machine. Other problems are preventable in theory but the practical effort is disproportionally high, e.g., to check whether a matrix is regular is feasible but might be as much or even more work than the actual task. In such cases, it is usually more efficient trying to accomplish the task and checking for Exceptions along the way.

# 1.6.2.1 Motivation

Before illustrating the old-style error handling, we introduce our anti-hero Herbert[^1] who is an ingenious mathematician and considers programming a necessary evil for demonstrating how magnificently his algorithms work. He is immune to the newfangled nonsense of modern programming.

11. To all readers named Herbert: Please accept our honest apology for having picked your name.

His favorite approach to deal with computational problems is to return an error code (like the `main` function does). Say we want to read a matrix from a file and check whether the file is really there. If not, we return an error code of 1:

Click here to view code image

```
int read_matrix_file(const char* fname, matrix& A)
{
    fstream f(fname);
    if (!f.is_open())
    **return 1**;
    ...
    **return 0**;
}
```