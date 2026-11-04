![](bbox=[0.323, 0.078, 0.611, 0.252])

# ## Updating the DLL

The Fibonacci() method defined in the MathUtil project contains a bug. When num is less than or equal to 1, the method should return 1 and not 2. In the real world, the application and the DLL may already been deployed to the end user's computer. To fix this bug, you simply need to modify the Utils class, recompile it, and then update the user's computer with the new DLL:

```
```csharp
namespace MathUtil
{
    public class Utils
    {
        public int Fibonacci(int num)
        {
            if (num <= 1) return 1; //----fixed!----
            return Fibonacci(num - 1) + Fibonacci(num - 2);
        }
    }
}
```
```

Copy the recompiled MathUtil.dll from the bin\Debug folder of the MathUtil project, and overwrite the original MathUtil.dll located in the bin\Debug folder of the Windows project. When the application runs again, it will display the correct value, 21 (previously it displayed 42).

> > *Because the MathUtil.dll assembly is not digitally signed, a hacker could replace this assembly with one that contains malicious code, and the client of this assembly (which is the WindowsApp-Utli application in this case) would not know that the assembly has been tampered with. Later in this chapter, you will see how to give the assembly a unique identity using a strong name.*

# ## Modules and Assemblies

An application using a library loads it only when necessary — the entire library is loaded into memory during runtime. If the library is large, your application uses up more memory and takes a longer time to load. To solve this problem, you can split an assembly into multiple modules and then compile each individually as a module. The modules can then be compiled into an assembly.

To see how you can use a module instead of an assembly, add a new Class Library project to the solution used in the previous section. Name the Class Library project StringUtil. Populate the default Class1.cs file as follows: