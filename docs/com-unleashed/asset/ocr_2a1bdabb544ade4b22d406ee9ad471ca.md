# Table 14.3 Continued

| IMoniker Function | Comments |
|---|---|
| `IMoniker::ComposeWith()` | If `pmkRight` is an anti-moniker, the returned moniker is `NULL`. If `pmkRight` is a composite whose left-most component is an anti-moniker, the returned moniker is the composite with the left-most anti-moniker removed. If `pmkRight` is neither an anti-moniker nor a composite moniker whose left-most component is an anti-moniker, the method checks the `fOnlyIfNotGeneric` parameter. If it is `FALSE`, the method combines the two monikers into a generic composite; if it is `TRUE`, the method sets `*ppmkComposite` to `NULL` and returns `MK_E_NONGENERIC`. |
| `IMoniker::Enum()` | This method returns `S_OK` and sets `*ppEnumMoniker` to `NULL`. |
| `IMoniker::IsEqual()` | This method returns `S_OK` if `*pmkOther` is an OBJREF moniker and the paths for both monikers are identical (using a not-case-sensitive comparison). Otherwise, the method returns `S_FALSE`. |
| `IMoniker::Hash()` | This method calculates a hash value for the moniker. |
| `IMoniker::IsRunning()` | Because OBJREF monikers represent a running object instance, this method returns `TRUE` unless the object is known to be no longer running because a recent call failed. The method ignores `pmkToLeft`. |
| `IMoniker::GetTimeOfLastChange()` | This method returns `E_NOTIMPL`. |
| `IMoniker::Inverse()` | This method returns an anti-moniker, such as the results of calling `CreateAntiMoniker()`. |
| `IMoniker::CommonPrefixWith()` | If the two monikers are equal, this method returns `MK_S_US` and sets `*ppmkPrefix` to `NULL`. If the other moniker is not an OBJREF moniker, this method passes both monikers to the `IMoniker::CommonPrefixWith()` function. This function correctly handles the case in which the other moniker is a generic composite. If there is no common prefix, this method returns `MK_E_NOPREFIX`. |
| `IMoniker::RelativePathTo()` | This method returns `E_NOTIMPL`. |
| `IMoniker::GetDisplayName()` | This method obtains the display name for the OBJREF moniker. The display name is a 64-bit encoding that encapsulates the machine location, process endpoint, and interface pointer ID (IPID) of the running object. For future compatibility, the display name is restricted to characters that can be specified as part of a URL. |
| `IMoniker::ParseDisplayName()` | If `pmkToLeft` is not `NULL`, this method returns `MK_E_SYNTAX`. |
| `IMoniker::IsSystemMoniker()` | This method returns `S_OK` and passes back `MKSYS_OBJREFMONIKER`. |