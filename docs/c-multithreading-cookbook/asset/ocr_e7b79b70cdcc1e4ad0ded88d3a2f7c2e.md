# Understanding Concurrent Code Design

```
virtual TCHAR* ObjectName(void) const { return _T("SchwefelMT");
}
private:
    static DWORD WINAPI StartAddress(LPVOID lParameter);
    struct ThreadParams
{
        CShwefelMT* ptr;
        unsigned uThreadIndex;
    };

endif
```

3. Open **Solution Explorer** and right-click on **Source file**. Add a new source file named SchwefelMT. Copy and paste the following code to:
#include "stdfax.h"

```
DWORD WINAPI SchwefelMT::StartAddress(LPVOID lParameter)
{
    ThreadParams* params = (ThreadParams*)lParameter;
    unsigned uChunk = ((unsigned)params->this_ptr->Size()) /
    ThreadNumber; // Note: original text seems incomplete here
    unsigned uMax = (params->uThreadIndex + 1) * uChunk;

    for (unsigned i = params->uThreadIndex * uChunk; i < uMax; i++)
    {
        params->this_ptr->Sum() += params->this_ptr->Allele(i);
    }

    if (params->this_ptr->Min() > params->this_ptr->Allele(i))
    {
        params->this_ptr->Min() = params->this_ptr->Allele(i);
    }

    double dInnerSum = 0;
    for (unsigned j = 0; j < i; j++)
    {
        dInnerSum += params->this_ptr->Allele(j);
    }

    double dTmp = dInnerSum * dInnerSum;
```