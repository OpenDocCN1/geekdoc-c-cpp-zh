To give an example, the interface IRemoteLandmarkStoreListener which is part of the Osp::Locations namespace defines a method OnLandmarksReceivedN(). This method is called when an application queries a remote server about its stored landmarks. If there are landmarks available that match the search criteria, they are stored in one of the parameters of the method. This parameter is local to the calling application, hence, the object ownership changes. The following code should exemplify this.

```
void
OnLandmarksReceivedN(RequestId reqId, IList* pResults, int pageNo, int countPerPage, int totalPageCount, int totalCount, result r,
const String& errorCode, const String& errorMsg)
{
    if (!IsFailed(r) && pResults)
    {
        // Do something with the results stored in pResults...
        pResults->RemoveAll(true);
        // You have to explicitly delete the object !!!
        delete pResults;
    }
}
```

# Exception Handling

Exception handling arrived in C++ not exactly as an afterthought, but a long time after the first release.⁴ Efficiency was an important design goal,⁵ in particular avoiding adding time or space cost to code that doesn’t use exceptions. That goal was certainly achieved, but quantifying the cost for code that does use exceptions is more controversial.

At least in the unoptimised case, ‘turning on’ standard C++ exception handling can add as much as a 10% code size increase to a system,⁶ with a measurable runtime performance penalty when exceptions are thrown and handled.

For those reasons, as well as for reasons of simplicity, bada does not support native C++ exceptions, but instead implements a simple error handling mechanism.

In bada:

+   - All exceptions are caught and returned as a simple type-defined result value.

⁴See B. Stroustrup, The Design and Evolution of C++ (Addison-Wesley, 1994). C++ 1.0 was released in 1986, exceptions were included in 1992.

⁵Stroustrup, Design and Evolution, p. 385.

⁶See B. Morris, Symbian OS Architecture Source Book (Wiley, 2007). The example is Symbian.