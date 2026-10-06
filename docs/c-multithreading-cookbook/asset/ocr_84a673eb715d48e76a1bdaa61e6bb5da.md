In our following example, we'll show how to abort a thread using the Abort method.

# Getting ready

Make sure Visual Studio is up and running.

# How to do it...

Now, let's create our program and explain its structure. Perform the following steps:

+   1. Create a new C++ CLR empty project named CLRAApplication.
2. Open Solution Explorer and right-click on Source file. Add a new source file named. Open main.cpp.

```
#include <Windows.h>
#include <tchar.h>
#include "MyForm.h"

using namespace System::Forms;
using namespace System::Threading;
using namespace CLRAApplication;

[STAThreadAttribute]
int APIENTRY tWinMain(HINSTANCE hInstance, HINSTANCE hPrev, LPTSTR szCommandLine, int iCmdShow)
{
Application::EnableVisualStyles();
Application::SetCompatibleCompatibleTextRenderingDefault(false);

Application::Run(gcnew MyForm());

return 0;
}
```

+   3. Open Solution Explorer and right-click on Header file. Under Visual C++, select Ui. Add a new Windows Form named MyForm.h.
4. Add the following code:

```
#pragma once
namespace CLRAApplication
{
using namespace System;
using namespace System::Threading;
using namespace System::Windows::Forms;
```