The general catch block will catch all exceptions, regardless of whether they derive from System.Exception, assuming an earlier catch block does not catch them. The disadvantage of such a block is simply that there is no exception instance to access and therefore no way to know the appropriate course of action. It wouldn't even be possible to recognize the unlikely case where such an exception is innocuous. The best course of action is to handle the exception with some cleanup code before shutting down the application. The catch block could save any volatile data, for example, before shutting down the application or rethrowing the exception.

# ### ADVANCED TOPIC

# #### General Catch Block Internals

The Common Intermediate Language (CIL) code corresponding to a general catch block is, in fact, a catch(object) block. Thus, regardless of the type thrown, the general catch block will catch it. Interestingly, it is not possible to explicitly declare a catch(object) exception block within C# code. Therefore, there is no means of catching a non-System.Exception-derived exception and having an exception instance to scrutinize.

In fact, unmanaged exceptions from languages such as C++ generally result in System.Runtime.InteropServices.SEHException-type exceptions, which derive from the System.Exception type. Therefore, not only can the unmanaged type exceptions be caught using a general catch block, but the non-System.Exception-managed types that are thrown can be caught as well—for instance, types such as string.

# ## Guidelines for Exception Handling

Exception handling provides much-needed structure to the error-handling mechanisms that preceded it. However, it can still lead to some unwieldy results if used haphazardly. The following guidelines offer some best practices for exception handling.

+   * Catch only the exceptions that you can handle.

Generally it is possible to handle some types of exceptions but not others. For example, opening a file for exclusive read-write access