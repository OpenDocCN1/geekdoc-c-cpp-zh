![](bbox=[0.055, 0.077, 0.94, 0.347])

FIGURE 29.9  The STAThread attribute emitted on the Main entry-point method for WPF.

![](bbox=[0.055, 0.394, 0.94, 0.574])

FIGURE 29.10  Many UI components require a single-threaded apartment.

Other than using the STAThread and MTAThread attributes on entry-point methods, you can also specify the apartment state using the SetApartmentState method on a Thread instance. For further information, consult the MSDN documentation.

# Dealing with Exceptions

Unhandled exceptions occurring on any thread cause the application to be terminated by the common language runtime. Because of this, it’s essential to guard your thread entry-point methods against unhandled exceptions if specific types of exceptions are tolerable. For example, threads handling user requests should not be able to take down the entire web or application server unless something really exceptional happens (such as memory corruption, out-of-memory situations, stack overflows, and so on).

This does not imply you should use the “catch-all” technique because this could silence way too many exceptions that could cause damage later during the application’s execution (for example, because of broken invariants). In other words, one should know what’s safe to catch rather than be lazy. Also, if you decide to put in place a last-resort top-level catch in a thread’s entry-point method, it’s generally a good idea to put logging in place as well, so you can analyze failure modes you might need to address in a more disciplined way.