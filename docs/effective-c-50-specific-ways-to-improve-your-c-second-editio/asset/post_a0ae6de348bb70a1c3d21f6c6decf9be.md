
CLR will place on your assemblies. If the CLR does not fully trust an assembly, it limits the allowed actions. This is called code access security (CAS). On another axis, the CLR enforces role-based security, in which code might or might not execute based on a particular user account’s privileges. You’ll also see these effects when you create Silverlight applications that run in a browser. The browser model imposes security restrictions on any code running in that environment.

Security violations are runtime conditions; the compiler cannot enforce them. Furthermore, they are far less likely to show up on your development machine; code that you compile is loaded from your hard drive and, therefore, has a higher trust level. Discussing all the implications of the .NET Security model fills volumes, but you can take a small set of reasonable actions to enable your assemblies to interact with the .NET security model more easily. These recommendations apply only if you are creating library components, or components and programs that might be delivered across the Web.

Throughout this discussion, remember that .NET is a managed environment. The environment guarantees a certain amount of safety. The bulk of the .NET Framework library is granted full trust through the .NET config policy when it is installed. It is verifiably safe, which means that the CLR can examine the IL and ensure that it does not perform any potentially dangerous actions, such as accessing raw memory. It does not assert any particular security rights needed to access local resources. You should try to follow that same example. If your code does not need any particular security rights, avoid using any of the CAS APIs to determine your access rights; all you do is decrease performance.

You will use the CAS APIs to access a small set of protected resources that demand increased privileges. The most common protected resources are unmanaged memory and the file system. Other protected resources include databases, network ports, the Windows Registry, and the printing subsystem. In each case, attempting to access those resources fires exceptions when the calling code does not have the proper permissions. Furthermore, accessing those resources might cause the runtime to perform a security stack walk to ensure that all assemblies in the current callstack have the proper permissions. Let’s look at memory and the file system, discussing the best practices for a secure and safe program.

You can avoid unmanaged memory access by creating verifiably safe assemblies whenever possible. A safe assembly is one that does not use any pointers to access either the managed or unmanaged heaps. Whether you knew it or not, almost all the C# code that you create is safe. Unless you turn on the /unsafe C# compiler option, you’ve created verifiably safe code. /unsafe allows the use of pointers, which the CLR cannot verify.

The reasons to use unsafe code are few, with the most common being performance. Pointers to raw memory are faster than safe reference checks. In a typical array, they can be up to ten times faster. But when you use unsafe constructs, understand that unsafe code anywhere in an assembly affects the entire assembly. When you create unsafe code blocks, consider isolating those algorithms in their own assembly (see Item 50). This limits the effect that unsafe code has on your entire application. If it’s isolated, only callers who need the particular feature are affected. You can still use the remaining safe functionality in more restrictive environments. You might also need unsafe code to deal with P/Invoke or COM interfaces that require raw pointers. The same recommendation applies: Isolate it. Unsafe code should affect its own small assembly and nothing else.

The advice for memory access is simple: Avoid accessing unmanaged memory whenever possible. When you do need to access unmanaged memory, you should isolate that access in a separate assembly.

The next most common security concern is the file system. Programs store data, often in files. Code that has been downloaded from the Internet does not have access to most locations on the file system—that would be a huge security hole. Yet, not accessing the file system at all would make it far more difficult to create usable programs. This problem is solved by using isolated storage. Isolated storage can be thought of as a virtual directory that is isolated based on the assembly, the application domain, and the current user. Optionally, you can use a more general isolated storage virtual directory that is based on the assembly and the current user.

Partially trusted assemblies can access their own specific isolated storage area but nowhere else on the file system. The isolated storage directory is hidden from other assemblies and other users. You use isolated storage through the classes in the System.IO.IsolatedStorage namespace. The IsolatedStorageFile class contains methods very similar to the System.IO.File class. The IsolatedStorageFileStream class is derived from the System.IO.FileStream class. The code to write to isolated storage is almost the same as writing to any file:

```
IsolatedStorageFile iso =
    IsolatedStorageFile.GetUserStoreForDomain();

IsolatedStorageFileStream myStream =
    new IsolatedStorageFileStream("SavedStuff.txt",
    FileMode.Create, iso);
StreamWriter wr = new StreamWriter(myStream);
// several wr.Write statements elided
wr.Close();
```

Reading is equally familiar to anyone who has used file I/O:

```
IsolatedStorageFile isoStore =
    IsolatedStorageFile.GetUserStoreForDomain();

string[] files = isoStore.GetFileNames("SavedStuff.txt");
if (files.Length > 0)
{
    StreamReader reader = new StreamReader(new
        IsolatedStorageFileStream("SavedStuff.txt",
        FileMode.Open, isoStore));

    // Several reader.ReadLine() calls elided.

    reader.Close();
}
```

You can use isolated storage to persist reasonably sized data elements that enable partially trusted code to save and load information from a carefully partitioned location on the local disk. The .NET environment defines limits on the size of isolated storage for each application. This prevents malicious code from consuming excessive disk space, rendering a system unusable. Isolated storage is hidden from other programs and other users. Therefore, it should not be used for deployment or configuration settings that an administrator might need to manipulate. Even though it is hidden, however, isolated storage is not protected from unmanaged code or from trusted users. Do not use isolated storage for high-value secrets unless you apply additional encryption.

To create an assembly that can live within the possible security restrictions on the file system, isolate the creation of your storage streams. When your assembly might be run from the Web or might be accessed by code run from the Web, consider isolated storage.

You might need other protected resources as well. In general, access to those resources is an indication that your program needs to be fully trusted. The only alternative is to avoid the protected resource entirely. Consider the Windows Registry, for example. If your program needs to access the Registry, you must install your program to the end user’s computer so that it has the necessary privileges to access the Registry. You simply can’t safely create a Registry editor that runs from the Web. That’s the way it should be.

The .NET Security model means that your program’s actions are checked against its rights. Pay attention to the rights your program needs and try to minimize them. Don’t ask for rights you don’t need. The fewer protected resources your assembly needs, the less likely it will generate security exceptions. Avoid using secure resources, and consider alternatives whenever possible. When you do need higher security permissions for some algorithms, isolate that code in its own assembly.

## Item 49: Prefer CLS-Compliant Assemblies

The .NET environment is language agnostic: Developers can incorporate components written in different .NET languages without limitations. In practice, it’s almost true. You must create assemblies that are compliant with the Common Language Specification (CLS) to guarantee that developers writing programs in other languages can use your components.

One of C#’s advantages is that because it was designed to run on the CLR, almost all of your C# assemblies will be CLS compliant. That’s not true for many other languages. Many F# constructs do not compile down to CLS-compliant types. DLR languages, such as IronPython and IronRuby, do not create CLS-compliant assemblies in this release. That’s one of the reasons C# is an excellent choice for component development in .NET. C# components can be consumed by all the languages that run on the CLR. That’s because it’s not that hard to create C# components that are CLS compliant.

CLS compliance is a new twist on that least common denominator approach to interoperability. The CLS specification is a subset of operations that every language must support. To create a CLS-compliant assembly, you must create an assembly whose public interface is limited to those features in the CLS specification. Then any language supporting the CLS specification must be capable of using the component. This does not mean you must limit your entire programming palette to the CLS-compliant subset of the C# language, however.
