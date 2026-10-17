
我们的 `ThreadStart` 方法与原型匹配，这就是线程开始执行的地方。`CreateThread` API 的第四个参数被传递给线程例程。如果你需要多个参数，可以创建一个类或传递对象的地址。你可以在 MSDN（`http://cdn.microsoft.com/en-us/library/windows/desktop/ms68243d28-vs.8529.aspx`）上找到更多关于 `CreateThread` API 的信息。

# 线程使用

大多数应用程序都在使用数据库。在许多情况下，此类应用程序从不同的 PC 运行，并进行同步的读写操作。下面的示例将演示使用 MySQL 数据库的线程。

## 准备工作

对于下一个示例，你需要安装 MySQL C 连接器。详细解释可以在附录找到。成功安装 MySQL C 连接器后，启动 Visual Studio。

## 如何操作...

- 创建一个新的 C++ 控制台应用程序。命名为 `MultithreadedDBTest`。
- 打开解决方案管理器并添加一个新头文件。命名为 `CMSql.h`。
- 打开 `CMSql.h` 并粘贴以下代码：

```cpp
#include <stdafx.h>
#include <stdio.h>
```

### 进程与线程的概念

```cpp
#include <stdlib.h>
#include <mysql.h>
class CMYS {
public:
    static CMYS* CreateInstance(char* szHostname, char* szDatabase, char* szUserId, char* szPassword);
    static void ReleaseInstance();
    bool ConnectInstance();
    bool DisconnectInstance();
    bool ReadData(char* szQuery, char* szResult, size_t uLength);
    bool WriteData(char* szQuery, char* szResult, size_t uLength);
private:
    CMYS(char* szHostname, char* szDatabase, char* szUserId, char* szPassword);
    CMYS();
    char* szHostname;
    char* szDatabase;
    char* szUserId;
    char* szPassword;
    CMYS* mysqlConnection;
    static CMYS* mysqlInstance;
};
```

3. 打开解决方案管理器并添加一个新的 `CMYSQL.cpp` 文件。打开 `CMYSQL.cpp` 并粘贴以下代码：

```cpp
#include "stdafx.h"
#include "MySQL.h"
CMYSQL* CMYSQL::mysqlInstance = NULL;
CMYSQL* CMYSQL::CreateInstance(char* szHostname, char* szDatabase, char* szUserId, char* szPassword)
{
    if (mysqlInstance)
    {
        return mysqlInstance;
    }
    return new CMYSQL(szHostname, szDatabase, szUserId, szPassword);
}
```

# 第 2 章

```cpp
void MySQL::ReleaseInstance()
{
    if (mysqlInstance)
    {
        delete mysqlInstance;
    }
}
MySQL::MySQL(char* szHostName, char* szDatabase, char* szUserId, char* szPassword)
{
    size_t length = 0;
    this->szHostName = new char[length = strlen(szHostName) + 1];
    strcpy_s(this->szHostName, length, szHostName);
    this->szDatabase = new char[length = strlen(szDatabase) + 1];
    strcpy_s(this->szDatabase, length, szDatabase);
    this->szUserId = new char[length = strlen(szUserId) + 1];
    strcpy_s(this->szUserId, length, szUserId);
    this->szPassword = new char[length = strlen(szPassword) + 1];
    strcpy_s(this->szPassword, length, szPassword);
}
MySQL::~MySQL()
{
    delete szHostName;
    delete szDatabase;
    delete szUserId;
    delete szPassword;
}
bool MySQL::ConnectInstance()
{
    MYSQL* mysqlLink = NULL;
    try
    {
        mysqlConnection = mysql_init(NULL);
        mysqlLink = mysql_real_connect(mysqlConnection, szHostName, szUserId, szPassword, szDatabase, 3306, NULL, 0);
    }
    catch (...)
    {
        mysqlConnection = 0;
        return false;
    }
    return mysqlLink ? true : false;
}
bool MySQL::DisconnectInstance()
{
    try {
        mysql_close(mysqlConnection);
        return true;
    } catch (...) {
        return false;
    }
}
bool MySQL::ReadData(char* szQuery, char* szResult, size_t uLength)
{
    int mysqlStatus = 0;
    MYSQL_RES* mysqlResult = NULL;
    MYSQL_ROW mysqlRow = NULL;
    unsigned long numRows = 0;
    try {
        mysqlStatus = mysql_query(mysqlConnection, szQuery);
        if (mysqlStatus) {
            return false;
        } else {
            mysqlResult = mysql_store_result(mysqlConnection);
        }
        if (mysqlResult) {
            numRows = mysql_num_rows(mysqlResult);
            unsigned long numFields = mysql_num_fields(mysqlResult);
            mysqlRow = mysql_fetch_row(mysqlResult);
            if (mysqlRow) {
                if (!mysqlRow[0]) {
                    mysql_free_result(mysqlResult);
                    return false;
                } else {
                    mysql_free_result(mysqlResult);
                    return false;
                }
            }
            size_t szResultLength = strlen(mysqlRow[0]) + 1;
            strncpy(szResult, mysqlRow[0], szResultLength > uLength ? uLength : szResultLength);
            if (mysqlResult) {
                mysql_free_result(mysqlResult);
                mysqlResult = NULL;
            }
        }
    } catch (...) {
        return false;
    }
    return true;
}
bool MySQL::WriteData(char* szQuery, char* szResult, size_t uLength)
{
    try {
        int mysqlStatus = mysql_query(mysqlConnection, szQuery);
        if (mysqlStatus) {
            return false;
        }
        return true;
    } catch (...) {
        return false;
    }
}
```

4. 打开 `MultithreadedTest.cpp` 并粘贴以下代码：

```cpp
#include "stdafx.h"
#include "mysql.h"
#define BLOCK_SIZE 4096
#define THREADS_NUMBER 3
typedef struct {
    char szQuery[BLOCK_SIZE];
    char szResult[BLOCK_SIZE];
    bool bIsRead;
} QUERYDATA, *PQUERYDATA;
CRITICAL_SECTION cs;
CMYS* mysqlInstance = NULL;
WORD WINAPI StartAddress(LPVOID lpParameter)
{
    QUERYDATA pQueryData = (PQUERYDATA)lpParameter;
    EnterCriticalSection(&cs);
    if (mysqlInstance->ConnectInstance()) {
        if (pQueryData->bIsRead) {
            memset(pQueryData->szResult, 0, BLOCK_SIZE-1);
            mysqlInstance->ReadData(pQueryData->szQuery, pQueryData->szResult, BLOCK_SIZE - 1);
        }
        else {
            mysqlInstance->WriteData(pQueryData->szQuery, pQueryData->szResult, BLOCK_SIZE - 1);
        }
        mysqlInstance->DisconnectInstance();
    }
    LeaveCriticalSection(&cs);
    return 0;
}
int main() {
    InitializeCriticalSection(&cs);
    mysqlInstance = MySQL::CreateInstance("mysql.services.expertit_its.me", "expertit_9790OS", "expertit_9790", "$dbpass_1342");
    if (mysqlInstance) {
        HANDLE hThreads[THREADS_NUMBER];
        QUERYDATA queryData[THREADS_NUMBER] = {
            {"select address from clients where id = 3;", "", true},
            {"update clients name='Merrill & Lynch' where id=2;", "", false},
            {"select name from clients where id = 2;", "", true}
        };
        for (int iIndex = 0; iIndex < THREADS_NUMBER; iIndex++) {
            hThreads[iIndex] = CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)StartAddress, &queryData[iIndex], 0, 0);
        }
    }
}
```

```cpp
WaitForMultipleObjects(THREADS_NUMBER, hThreads, TRUE, INFINITE);
for (int iIndex = 0; iIndex < THREAD_NUMBER; iIndex++)
{
    printf("%s\n", queryData[iIndex].szResult);
    MySQL:ReleaseInstance();
}
DeleteCriticalSection(&cs);
return system("pause");
```

## 工作原理...

上一个示例演示了操作 MySQL 数据库的应用程序中的同步。该示例仅展示了实现此目标的方法，而另一种方法是使用数据库管理系统（DBMS）本身的表锁来实现同步。这里的关键点是，当一个线程执行读或写操作时，禁用另一个线程同时进行读或写操作。我们假设三个线程中有两个必须读取，第三个必须写入某些数据。你可以假设在读取之后，线程必须向主应用程序或或其他处理程序发送数据以继续处理。对于必须写入的线程，情况也是如此——它将从某个处理程序获取数据并执行必要的操作。对于线程同步，我们使用了“临界区对象”（`critical section object`）。关于临界区对象的详细解释将在第 5 章《线程管理》中介绍。

## 更多内容...

正如我们所说，还有另一种更容易的方法可以在线程操作 MySQL 数据库时对其进行同步。在如今的 MySQL DBMS 中，我们可以使用表锁来实现这一点。为了给用户一个提示，我们将演示从两个线程执行查询的一种方法，同时保持同步的读写操作，且互不干扰。

- 1. 读取线程：
   `lock table TABLE_NAME read;`
   `select something from TABLE_NAME;`
   `unlock tables;`

- 2. 写线程：
   `lock table TABLE_NAME write;`
   `insert into TABLE_NAME values( _ );`

```sql
update TABLE_NAME set something;
unlock tables;
```
