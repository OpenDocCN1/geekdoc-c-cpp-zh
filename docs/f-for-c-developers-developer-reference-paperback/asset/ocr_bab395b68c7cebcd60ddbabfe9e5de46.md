```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace CompiledName
{
    class Program
{
        static void Main(string[] args)
        {
            var x = PortableLibrary1.TestModule;
        }
    }
}
```

**FIGURE 7-5** Invoking a function decorated with the CompiledName attribute from a C# project

# # Exploring the Portable Library Samples

As previously mentioned, the portable library supports only a subset of the assemblies provided by .NET. This presents a good opportunity for you to apply F# features to some complex problems. In this section, algorithm and data structure samples, which are the foundation to completing complex logic, are presented. When solving these complex problems, I will also demonstrate how to use F# features to improve the overall code quality. I do not believe that code always be written in the same way. Different strokes for different folks. You should be able to recognize the features that are most useful to you with your existing skill set and apply them to your daily work.

> Note This section does not discuss algorithm design. If you are interested in this topic, I encourage you to reference other sources, such as The Algorithmist website at http://www.algorithmmist.com/index.php/Main_Page.

Let's start with a small number-cracking problem. Imagine that you did not have the module operator available to you. How would you check whether a number is divisible by 7? The math required for determining this, as illustrated by List 7-3, is a number in the following:
  10a + b is divisible by 7 and only if a - 2b is divisible by 7

**LIST 7-3** Checking that a number is divisible by 7

```
let rec `''??'' x =
    match x with
    | 0
    | 7 -> true
    | when x > 0 && x < 10 -> false
    | when x < 0 -> `''??'-x
    | ->
        let a = x / 10
```