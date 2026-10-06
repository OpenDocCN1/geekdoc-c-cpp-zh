# The difference between foreground and background threads

.NET, there are two types of threads: foreground and background. Threads are, by default, created as background threads. You could set the thread state explicitly as background. The difference is that foreground threads keep an application alive as long as they are running; while background threads do not. In other words, when you close applications, all background threads are automatically terminated. So, when all the foreground threads complete execution, the application can exit before the background threads return. After all the foreground threads have stopped, or after the application exits, the system stops all background threads.

Our previous example used the Task object, which runs in the background by default. Our following example will be the same as the previous one, with the focus on foreground threads. That's why we will use the Thread object instead of Task.

# Getting ready

Make sure Visual Studio is up and running.

# How to do it...

Now, let's create our new project and explain its structure. Perform the following steps:

+   1. Create a new C++ CLR empty project application named CLApplication.
2. Open Solution Explorer and right-click on Source file. Add a new source named main. Open main.cpp. Copy and paste the following code:

```
#include <Windows.h>
#include <tchar.h>
#include "MyForm.h"

using namespace System::Forms;
using namespace System::Threading;
using namespace CLApplication2;

[STAThreadAttribute]
int APIENTRY _tWinMain(HINSTANCE hThis, HINSTANCE hPrev, LPTSTR
szCommandLine, int iCmdShow)
(
```