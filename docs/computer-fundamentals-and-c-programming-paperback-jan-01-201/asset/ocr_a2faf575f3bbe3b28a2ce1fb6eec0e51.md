# ## 11.11 CALLING A FUNCTION FROM ANOTHER FUNCTION

Just as **main** calls a function, a function can also call another function. The called function can in turn call another function, and so on. In this scenario, the returns of all intermediate functions are kept pending until the innermost function returns. The remaining functions then return in the reverse sequence of their invocation. Ultimately, the outermost function returns control to **main** (Fig. 11.2).

As long as the return of a function is kept pending, its parameters and local variables continue to occupy space in memory. Freeing of memory begins with the return of *fn* and continues progressively as the other functions return. However, the return value, if any, of every function is captured by its caller before the called function is extinguished.

![](bbox=[0.072, 0.287, 0.927, 0.408])

**FIGURE 11.2** Functions Calling Other Functions

# ### 11.11.1 **time_diff.c**: Program to Compute Difference Between Two Times

Let’s now take up Program 11.8, which computes the difference between two times input by the user, each in *hh mm* format. The **main** function calls the **time_diff** function, which computes the elapsed time in minutes. This function in turn calls the **absolute** function to ensure that a negative value is converted to positive before it is returned to **main**. The function call sequence is shown below:

![](bbox=[0.332, 0.593, 0.692, 0.609])

Even though the **absolute** function is called from **time_diff**, it must be declared before **main**. This is because a function can’t be declared in the body of another function. **scanf** accepts the two times as four variables, which are then passed as arguments to **time_diff**. After **time_diff** returns, its return value is printed. Note that **main** can’t return until **time_diff** returns, which can do so only after **absolute** returns.

The **time_diff** function converts the two times to minutes elapsed since 00:00 hours (on the same day) before they are subtracted. (The UNIX clock is maintained as the number of seconds elapsed since January 1, 1970, 00:00 hours.) Because the times are not validated, a negative value is possible, so a call to the **absolute** function is made. This function simply returns the absolute value of the number using a conditional expression.

> > **Note:** Most implementations of C allocate a fixed chunk of memory (the stack) for function variables and parameters. This space, which is usually adequate for multiple invocations of functions, is progressively eaten up as one function calls another, which in turn calls another, and so on. The space may be totally consumed when a function calls itself by recursion and fails to terminate. The functioning of the stack is taken up later in the chapter.