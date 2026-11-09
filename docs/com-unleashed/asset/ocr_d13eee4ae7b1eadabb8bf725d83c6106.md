COM+ provides a few useful macros for working with HRESULTs, as shown in Table 13.1.

# Table 13.1  Macros for Working with HRESULTs

| Macros | Definition |
|---|---|
| `SUCCEEDED()` | Returns TRUE if the severity is success (zero) and FALSE if the severity is failure (one). |
| `FAILED()` | Opposite of `SUCCEEDED()`. |
| `HRESULT_FACILITY()` | Returns the facility code of the HRESULT. |
| `HRESULT_SEVERITY()` | Returns the severity bit of the `HRESULT_CODE()`. |
| `HRESULT_CODE()` | Returns the status code of the HRESULT. |
| `MAKE_HRESULT()` | Builds an HRESULT from its three components (facility, severity, status code). |

# Error-Handling Strategies

There are three strategies for handling HRESULT values. The first strategy is to simply test for S_OK, zero, and nonzero values. As you remember, earlier in this chapter you encountered the E_ACCESSDENIED HRESULT from the CoCreateInstance() function. In order to test for an error condition, you tested the HRESULT for a nonzero value. This caught the error adequately and terminated the program somewhat appropriately. This error-handling strategy is acceptable for some situations that do not require clean error handling.

The preferred method is to test the HRESULT using the SUCCEEDED() and FAILED() macros. This strategy is no harder to implement and is a better strategy for production-quality applications. Listing 13.8 is an example of using this strategy. Notice in the code that the FAILED() macro is used to test for an error.

# Listing 13.8  Using FAILED() for Error Handling

```
HRESULT hresult = ::CoCreateInstance(clsid, NULL, CLSCTX_SERVER,
                                  IID_IUnknown, (LPVOID FAR *) &punk);
if FAILED(hresult)
{
    // CoCreateInstance failed
    return hresult;
};
```

The third strategy is to test using specific HRESULTs. The difference between the second and third strategies is the difference between testing with an if statement and testing with a case statement. Listing 13.9 is an example of using the third strategy.