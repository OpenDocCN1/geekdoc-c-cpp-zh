
```cpp
#if DEBUG

BOOL bSuccess = CreateProcess(

TEXT("../Debug/tmpProcess.exe"), NULL, NULL,

NULL, FALSE, 0, NULL, &startupInfo,

&processInformation);

#else

BOOL bSuccess = CreateProcess(

TEXT("../Release/tmpProcess.exe"), NULL, NULL,

NULL, FALSE, 0, NULL, &startupInfo,

&processInformation);

#endif
```

```cpp
WaitForSingleObject(hThread, INFINITE);

CloseHandle(hThread);

return system("pause");
```

- 4. 创建名为 `tmpProcess` 的新 C++ 控制台应用程序。
- 5. 打开解决方案管理器。右键点击 `tmpThread` 项目。在“选择项目依赖”中。在下拉列表中选择 `tmpThread`。在下方空间中，勾选 `tmpProcess` 项目。
- 6. 打开 `tmpProcess.cpp`。
- 7. 将以下代码添加：

```cpp
#include <afx.h>

#include <iostream>

int main(int argc, TCHAR* argv[])

{

    std::cout << "Hello. I am a very simple process."

    << "I am used to demonstrate process creation."

    << std::endl;

    return 0;

}
```
