System.MissingFieldException
System.MissingMethodException
System.Resources.MissingManifestResourceException
System.Resources.MissingSatelliteAssemblyException
System.MulticastNotSupportedException
System.NotImplementedException
System.NotSupportedException
System.PlatformNotSupportedException
System.NullReferenceException
System.OperationCanceledException
System.Threading.Task.CanceledException
System.OutOfMemoryException
System.InsufficientMemoryException
System.Security.Policy.PolicyException
System.RankException
System.Reflection.ReflectionTypeException
System.Runtime.Remoting.RemotingException
System.Runtime.Remoting.RemotingTimeoutException
System.Runtime.InterServices.SafeAreaRankMismatchException
System.Runtime.InterServices.SafeAreaMismatchException
System.Security.SecurityException
System.Threading.SemaphoreException
System.Runtime.Serialization.SerializationException
System.Runtime.Remoting.ServerException
System.StackOverflowException
System.Threading.SynchronizationLockException
System.Threading.ThreadAbortedException
System.Threading.ThreadStartException
System.Threading.ThreadStateException
System.TimeoutException
System.TypeInitializationException
System.TypeLoadException
System.D01NotFoundException
System.EntryPointNotFoundException
System.TypeAccessException
System.TypeUnloadedException
System.UnauthorizedAccessException
System.Security.AccessControl.PrivilegeNotHeldException
System.Security.VerificationException
System.Security.XmlSyntaxException
System.Threading.Tasks.TaskNotFoundException
System.TimeNotFoundException

The original idea was that Exception, would be the base for all exceptions and for two other types, System.Exception and System.ApplicationException, would be the only types immediately derived from Exception. Furthermore, exceptions from the CLR would be derived from SystemException, and all application-exceptions would be derived from ApplicationException. This way, developers could write a catch block that catches all CLR-exceptions or all application-exceptions.

However, as we can see, this rule was not followed well; some exceptions are immediately derived from Exception (IsolatedStorageException), some CLR-exceptions are derived from ApplicationException (TargetInvocationException), and some application-