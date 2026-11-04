# CHAPTER 8

# Basics of Exceptions and Resource Management

# IN THIS CHAPTER

+   - Exception Handling 409
+   - Deterministic Resource Cleanup 438
+   - Locking on Objects 447

Continuing our exploration of statements in the C# programming language, we now look at concepts such as exceptions, locks, and proper resource disposal. Later chapters detail many of those aspects. For now, it’s essential for you to have a good understanding of the breadth of statements.

# Exception Handling

One strength of managed code lies in the structured approach to error handling using exceptions. Recall our native code fragment in the context of the goto statement’s discussion in Chapter 7, “Simple Control Flow,” in the section, “The goto Statement?” Let’s refresh our minds and highlight a few aspects of it:

```
```c
// Dealing with HRESULT return codes in C or C++.
HRESULT InitDownloadManager()
{
    IBackgroundCopyManager* g_pbc m = NULL;
    HRESULT hr;

    hr = CoInitializeEx(NULL, COINIT_APARTMENTTHREADED);
    if (FAILED(hr))
        goto Exit;

    hr =
    CoCreateInstance(__uuidof(BackgroundCopyManager), NULL,
    CLSCTX_LOCAL_SERVER,
    __uuidof(IBackgroundCopyManager),
    (void**) &g_pbc m);
```
```