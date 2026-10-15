.NET Framework 4 introduces the new Task Parallel Library (TPL), born in the multicore age and prepared to work with a new lightweight concurrency model. The TPL provides a lightweight framework that enables developers to work with the following parallelism scenarios, implementing task-based designs instead of working with heavyweight and complex threads:

+   Data parallelism — There is a lot of data and it is necessary to perform the same operations for each piece — for example, encrypting 100 Unicode strings using the Advanced Encryption Standard (AES) algorithm with a 256-bits key.

+   Task parallelism — There are many different operations that can run concurrently, taking advantage of parallelism — for example, generating hash codes for files, encrypting Unicode strings, and creating thumbnail representations of images.

+   Pipelining — A mix of task and data parallelism. It is the most complex scenario because it always requires the coordination between multiple concurrent specialized tasks — for example, encrypting 100 Unicode strings using the AES algorithm with a 256-bits key and then generating a hash code for each encrypted string. This pipeline could be implemented running two concurrent tasks: the encryption and the hash code generation. Each encrypted Unicode string would enter into a queue in order to be processed by the hash code generation algorithm.

The easiest way to understand how to work with parallel tasks is by using them. Thus, you can take your first step toward creating parallelized code with the methods offered by the System.Threading.Tasks.Parallel static class.

# System.Threading.Tasks.Parallel Class

The most important namespace for TPL is the new System.Threading.Tasks. It offers access to classes, structures, and enumerations introduced in .NET Framework 4, including the new System.Threading.Tasks.Parallel static class. Therefore, it is a good idea to import this namespace whenever you want to work with TPL:

```
Imports System.Threading.Tasks
```

This way, you will avoid large references. For example, instead of writing System.Threading.Tasks.Parallel.Invoke, you will be able to write Parallel.Invoke. In order to simplify the code, I will assume the aforementioned import is used in all the code snippets. However, remember that you can download the sample code for each code snippet and listing.

The main class is Task, representing an asynchronous and potentially concurrent operation. However, it is not necessary to work directly with instances of Task in order to create parallel code. Sometimes, the best option is to create parallel loops or regions, especially when the code seems to be appropriate for a sequential loop. In these cases, instead of working with the lower-level Task instances, it is possible to work with the methods offered by the Parallel static class (System.Threading.Tasks.Parallel):

+   Parallel.For — Offers a load-balanced, potentially parallel execution of a fixed number of independent For loop iterations

+   Parallel.ForEach — Offers a load-balanced, potentially parallel execution of a fixed number of independent ForEach loop iterations

+   Parallel.Invoke — Offers the potentially parallel execution of the provided independent actions

These methods are very useful when you are refactoring existing code to take advantage of potential parallelism. However, it is very important to understand that it is not as simple as replacing a For statement with Parallel.For. Many techniques for refactoring existing loops are covered in detail later in this chapter.

# Parallel.Invoke

The easiest way to try to run many methods in parallel is by using the new Invoke method provided by the Parallel class. For example, suppose that you have the following four independent subroutines that perform a format conversion, and you are sure it is safe to run them concurrently: