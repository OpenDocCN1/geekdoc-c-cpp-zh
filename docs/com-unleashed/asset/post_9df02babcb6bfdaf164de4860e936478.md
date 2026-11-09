
through the ISubscriberControl interface. This interface enables clients to discard or redirect particular events.

Take for instance an order entry system. During design it was decided that availability information could be sent once the order was received, but wasn’t essential to the real-time order entry. This decision could be the result of a traffic estimate. The loosely coupled architecture (where no real-time availability information is available) can more effectively amortize the use of the application servers over time. After an order is placed, the subscriber can be notified of any availability problems.

> **Note**
>
> LCE is yet another very powerful tool in the COM+ kit. Much like queued components, LCE services address a critical gap in previous COM implementations. Queued components offer COM-level one-way decoupled method invocation, and LCE provides a native COM broadcast mechanism. The features presented through the queued component and LCE services of COM+ solve problems that have caused many a developer to invent extensive custom software.

## Accessing Data with COM+

Data access in COM+ is much the same as that presented in MTS. In particular, OLE DB and ADO are the access mechanisms of choice. OLE DB supplies a very powerful and extensible architecture supporting various types of underlying data stores, including any ODBC source. OLE DB is necessarily complex because of its flexibility and performance. ATL Consumer and producer templates can ease the burden of OLE DB development in C++. By far, the most popular mechanism for programming OLE DB is, of course, ActiveX Data Objects (ADO). ADO provides a dual interface COM component implementation operating on top of OLE DB that can easily be used by compiled applications and scripts alike. Of course, if you’re like many developers, you already have very large ODBC-based systems that are fully supported in this environment as well.

### Read Optimized Data Access

IMDB is a smart in-memory database caching system optimized for read operations. IMDB allows static data to be loaded once and queried against many times. The performance advantages achievable with this type of in-memory data support are enormous. Queries satisfied locally through IMDB require neither network nor disk access. IMDB also supports write operations. It backlogs updates until they are committed. At that point, changes are submitted to the underlying database. Obviously, the real performance advantages lie in the arena of caching static-read weighted data.

Applications access the IMDB in much the same way as they would any other modern database. IMDB is an OLE DB provider, which ensures built-in support for most programming languages and scripting environments through ADO.

### The Transactional Shared Property Manager

The MTS Shared Property Manager (SPM) is a valuable asset to JIT-activated and early released components, providing a stable shared data store within a particular server process. COM+ implements the Shared Property Manager interfaces on top of IMDB. This new construct is referred to as the Transactional Shared Property Manager. Make sure that if you’re out with your COM+ buddies, you pronounce SPM as “spam.”

## COM+ Security

COM+ presents the same basic application server security features introduced by MTS. COM+ applications can use standard COM security, as well as declarative and procedural role-based security. COM+ has extended role-based security to the interface method, enabling administrators to control access at the most fundamental level (recall that MTS supports role membership only to the interface level). Unlike MTS, COM+ also supports role-based security in library packages. Enhanced security information is provided in COM+ through the ISecurityCallContext interface. The ISecurityCallContext interface supersedes the MTS ISecurityProperty interface and provides detailed information about all callers in the chain back to the base client. COM+ security is covered in more detail in Chapter 18.

## Base COM Features

MTS and COM/DCOM represent distinct paths of development supported by distinct development units at Microsoft. Such is the case with COM+ (the MTS successor) and the core COM services in Windows 2000. In this section, you’ll look at some of the new base COM services that are packaged along with COM+ in Windows 2000.

### Structured Storage

Structured storage is a storage compound file management service, supporting a file system within a file. The great thing about structured storage is that it is a standard mechanism supported directly by Windows and many application products. Windows 2000 promises to integrate structured storage into even more file system and shell features. Link tracking is a new feature enabling Windows 2000 to update OLE links within a structured storage file when the target object is moved. All the Win32 MoveFile() routines coordinate with the link tracking service, including the new MoveFileWithProgress() routine. The link tracking feature only functions on NTFS volumes, but presents a long-awaited solution to a common problem.

The structured storage system also introduces new routines for creating and opening compound files. These are as follows:

- `StgCreateStorageEx()`
- `StgOpenStorageEx()`

The `StgCreateStorageEx()` routine supersedes the `StgCreateDocfile()` routine and should be used by all new Windows 2000 applications. Enhancements to the structured storage system will be exposed through the two new Ex routines.

Windows 2000 includes an upgraded version of NTFS (NTFS v5) that enables many of the new disk-based services. Compound documents residing on NTFS v5 volumes can take advantage of the STGFM_NATIVE storage format. NTFS Native Structured Storage (NSS) uses the native property-based storage features of NTFS to improve compound document efficiency.

Windows 2000 structured storage also supports the new IDirectWriterLock interface, which enables a writer to obtain exclusive access to a root storage object opened in direct mode. Several readers can then concurrently access the storage.

### Canceling Outstanding COM Calls

Synchronous COM calls can block for extended periods of time while waiting for failed server requests to timeout. On the other hand, the very nature of asynchronous calls can introduce the need for some applications to cancel outstanding calls that have not completed before an outdating event takes place. COM supplies several call control interfaces that can be used to manage asynchronous method calls. COM+ creates and manages Cancel objects for all calls that use standard marshaling by calling `CoSetCancelObject()` before and after each method call. COM Cancel objects support the `ICancelMethodCalls` interface. The `ICancelMethodCalls` interface of a particular Cancel object can be obtained by calling the `CoGetCancelObject()` component library routine with the `IID_ICancelMethodCalls` interface ID. The `CoGetCancelObject()` prototype is displayed as follows:

```
HRESULT CoGetCancelObject(
    DWORD dwThreadId,    // Thread with pending call
    REFIID riid,         // IID of requested interface
    void ** ppUnk);      // Pointer to the requested interface
```

The `ICancelMethodCalls` interface supports the methods in Table 3.1.

**Table 3.1  ICancelMethodCalls Methods**

| ICancelMethodCalls Method | What It Does |
|---|---|
| `Cancel()` | Requests that the method be canceled. |
| `TestCancel()` | Checks to see whether the call has been canceled. |
| `SetCancelTimeout()` | Sets an automatic cancel timeout for the call. |

The process of getting the Cancel object interface and invoking the `Cancel()` method has a wrapper equivalent in the `CoCancelCall()` routine. `CoTestCancel()` provides a similar shortcut for the call to the `TestCancel()` method. Together these features make it easy to take call-level control of pending methods.

## Summary

COM+ is the next logical step in COM evolution. It isn’t a radical departure from COM, keeping the best of the COM architecture and adding enhancements.

One of the greatest advances is the capability to load balance and pool, unlike MTS that didn’t actually implement these features.

Many of the COM+ additions are improvements for the performance and functionality of its MTS predecessor. The MTS/COM+ model is a mandate from Microsoft, and you should be sure that you’re following its lead. COM+ makes MTS and COM inseparable and entices you by adding even more performance advantages.

The rest of the book shows you how to use COM+ to develop component applications and maximize its effectiveness.
