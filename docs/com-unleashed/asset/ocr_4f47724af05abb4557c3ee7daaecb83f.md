Again, before you attempt the next experiment, don’t forget to remove the Deny Launch permissions and Deny Access permissions that you created in the previous experiments. You should also kill any running instances of the server.

This is an experiment you won’t soon forget. Modify and recompile the COM+ server you built in the beginning of the chapter. Modify Listing 13.5 with the change in Listing 13.7. Run the code once and you’ll note that the current username is output to the C:\USER.LOG log file.

# **LISTING 13.7** Test the RunAs Property

```
```cpp
// MyObject.cpp : Implementation of CMyObject
#include "stdafx.h"
#include <fstream>
#include "MyProject.h"
#include "MyObject.h"

//////////////////////////////////////////////
// CMyObject


STDMETHODIMP CMyObject::get_MyProperty(long * pVal)
{
    // TODO: Add your implementation code here
    char sz[256];
    DWORD l = 255;
    ::GetUserName(sz, &l);
    ofstream of;
    of.open("C:\\USER.LOG", ios::out | ios::app);
    of << sz << endl;
    *pVal = 10;


    return S_OK;
}
```
```

Now, change the identity of the user by setting the user to some non-administrator local account other than your current user account. Now run Listing 13.6. Oops! This account does not have sufficient rights to access the object. Oh, well, kill it from the process list and restart the experiment. Oops! The current user does not have sufficient rights to kill the process. So, how do you kill the process? Reboot? No. In order to kill it, you must log off and log on as the user who launched the process.

This time before you run the listing, add Custom Access Permissions (under Server Security\Setting Launch Permissions) to the COM+ server for Everyone. If you run the code Listing 13.6 again, the C:\USER.LOG file will contain the username of the RunAs user, not the current user.