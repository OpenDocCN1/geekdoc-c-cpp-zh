the multithreading API available to you. Perhaps most importantly, this content describes how to effectively interact with the earlier patterns using the TPL and C# 5.0 and above.

Throughout these examples, exception handling has been eliminated for the purposes of elucidation.

# Asynchronous Programming Model

One particularly prominent pattern established prior to the TPL is the Asynchronous Programming Model (APM) pattern. Given a long-running synchronous method X(), the APM pattern uses a BeginX() method to start X() equivalent work asynchronously and an EndX() method to conclude it. (Henceforth we will name these methods X, BeginX, and EndX.)

# Using the APM Pattern

Listing C.1 demonstrates the pattern by using the System.Net.WebRequest class to download a web page. The functionality is the same as that found in the section titled “The Task-Based Asynchronous Pattern” in Chapter 18; however, this time we assume that the TPL and TAP are not available, and instead use the APM pattern. To maintain backward compatibility prior to TPL-related asynchronous methods being added, WebRequest also supports the APM pattern with the methods BeginGetResponse() (BeginX) and EndGetResponse() (EndX)—that is, asynchronous versions of the synchronous GetResponse() (X) method.

# LISTING C.1: Using the APM Pattern with WebRequest

```
using System;
using System.IO;
using System.Net;
using System.Linq;

public class Program
{
    public static void Main(string[] args)
    {
        string url = "http://www.IntelliTect.com";
        if (args.Length > 0)
        {
            url = args[0];
        }

        Console.Write(url);
```