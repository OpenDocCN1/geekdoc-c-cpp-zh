+   6. Write a slight modification of the previous program, this time using waitpid() instead of wait(). When would waitpid() be useful?

+   7. Write a program that creates a child process, and then in the child closes standard output (STDOUT_FILENO). What happens if the child calls printf() to print some output after closing the descriptor?

+   8. Write a program that creates two children, and connects the standard output of one to the standard input of the other, using the pipe() system call.