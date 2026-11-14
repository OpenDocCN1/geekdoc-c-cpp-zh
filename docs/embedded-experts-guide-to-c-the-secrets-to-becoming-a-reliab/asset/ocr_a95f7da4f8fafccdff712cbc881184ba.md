handler or a custom signal handler may be invoked. The C Standard defines six signals:

+   - SIGABRT (abort),
+   - SIGFPE (floating point error),
+   - SIGILL (illegal instruction),
+   - SIGINT (interrupt),
+   - SIGSEGV (segmentation violation), and
+   - SIGTERM (terminate).

```
#include
/* A simple program that waits for SIGINT. */
/* The signal handler. */
static void on_signal(int signum)
{
/* Do something with the signal. */
}

/* main() registers the handler and then loops. */
void main(void)
{
/* Register the SIGINT handler.
* Assume this is successful; a more complete
* implementation should check for errors. */
signal(SIGINT, on_signal);
```