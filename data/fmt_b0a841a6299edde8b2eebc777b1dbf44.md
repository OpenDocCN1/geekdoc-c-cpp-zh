
`ret = pthread_create (&thread_producer, NULL, producer, &loops);`

`if (ret)`

```
{
    printf("\n pthread_create() failed with error [%s]\n", strerror(errno));
    return -1;
}
int c = getchar(); // hold app to exit
pthread_mutex_destroy(&lock);
pthread_cond_destroy(&empty);
pthread_cond_destroy(&get);
return 0;
}
```

在 `producer()` 函数中，我们在获得信号 `empty` 后插入数据。然后我们调用 `pthread_cond_broadcast()` 来通知所有消费者线程。

```c
void *producer(void *arg)
{
    int i;
    int *loops = (int *)arg;
    for (i = 0; i < (*loops); i++)
    {
        pthread_mutex_lock(&lock);
        while (count == BUFF_LEN)
            pthread_cond_wait(&empty, &lock);
        buffer[index_put] = i;
        index_put = (index_put + 1) % BUFF_LEN;
        count++;
        pthread_cond_broadcast(&get); //broadcast to consumer
        pthread_mutex_unlock(&lock);
    }
    printf("exit from producer\r\n");
}
```

在 `consumer()` 函数中，我们在获得信号 `get` 后从数组获取数据。之后，我们使用 `pthread_cond_signal()` 通知生产者线程。

```c
void *consumer(void *arg)
{
    int i;
```

# 9. 数据库编程

本章解释如何使用 C 创建数据库应用程序。

## 9.1 用于 C 的数据库库

C 可以通过数据库驱动程序与数据库服务器通信。在开始开发数据库应用程序之前，我们必须安装用于 C 的数据库驱动程序。

在本章中，我只关注 MySQL 场景。基本上，我已经将这些代码发布到 Github，`https://github.com/agusk/crud-mysql-c`，去年。你可以下载并改进这些代码。

## 9.2 MySQL

要在 Ubuntu 及其数据库驱动程序中安装 MySQL 服务器和客户端，你可以尝试在终端中编写此命令

```bash
$ sudo apt-get install mysql-server mysql-client
$ sudo apt-get install libmysqlclient-dev
```

完成后，我们可以进行测试。

首先，我们可以开始创建一个简单的 C 应用程序来检查 MySQL 版本。编写此代码

```c
#include <my_global.h>
#include <mysql.h>
int main(int argc, char **argv)
{
    printf("MySQL client version: %s\n", mysql_get_client_info());
    exit(0);
}
```

将此程序保存到一个文件中，名为 `demo-mysql-version.c`。

现在你可以编译并运行此文件。

```bash
$ gcc -c -I/usr/include/mysql demo-mysql-version.c
$ gcc -o demo-mysql-version demo-mysql-version.o -L/usr/lib/mysql -lmysql
$ ./demo-mysql-version
```

如果成功，你将获得 MySQL 客户端版本。

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_111_0.png)

## 9.3 连接测试

在本节中，我们尝试测试到 MySQL 服务器的连接。创建一个文件，名为 `demo-connection.c` 并编写此代码。

```c
#include <my_global.h>
#include <mysql.h>
int main(int argc, char **argv)
{
    MYSQL *con = mysql_init(NULL);
    if (con == NULL)
    {
        fprintf(stderr, "%s\n", mysql_error(con));
        exit(1);
    }
    printf("connecting to mysql server...\r\n");
    // change host, username, and password
    if (mysql_real_connect(con, "localhost", "root", "password", NULL, 0, NULL, 0) == NULL)
    {
        printf("error: %s\r\n", mysql_error(con));
        mysql_close(con);
        exit(1);
    }
    printf("connected.\r\n");
    printf("closing connection...\r\n");
    mysql_close(con);
    printf("closed.\r\n");
    exit(0);
}
```

保存此程序。

现在你可以编译并运行此文件。

```bash
$ gcc -c -I/usr/include/mysql demo-connection.c
$ gcc -o demo-connection demo-connection.o -L/usr/lib/mysql -lmysqlclient
$ ./demo-connection
```

程序输出：

```
agusk@ubuntu15:~/books/cprog$ gcc -c -I/usr/include/mysql demo-connection.c
agusk@ubuntu15:~/books/cprog$ gcc -o demo-connection demo-connection.o -L/usr/lib/mysql -lmysqlclient
agusk@ubuntu15:~/books/cprog$ ./demo-connection
connecting to mysql server...
connected.
closing connection...
closed.
agusk@ubuntu15:~/books/cprog$ 
```

```c
MYSQL_STMT  *stmt;
stmt = mysql_stmt_init(con);
if (!stmt)
{
    printf(" mysql_stmt_init(), out of memory\r\n");
    exit(0);
}
if (mysql_stmt_prepare(stmt, CREATE_DATA, strlen(CREATE_DATA)))
{
    printf("mysql_stmt_prepare(), INSERT failed\r\n");
    printf("error: %s\r\n", mysql_stmt_error(stmt));
    exit(0);
}
int i;
time_t now = time(NULL);
char name[10];
unsigned long str_length;
float price;
MYSQL_BIND  bind[3];
MYSQL_TIME  ts;
memset(bind, 0, sizeof(bind));
bind[0].buffer_type= MYSQL_TYPE_VAR_STRING;
bind[0].buffer= (char *)&name;
bind[0].is_null= 0;
bind[0].length= &str_length;
bind[1].buffer_type= MYSQL_TYPE_FLOAT;
bind[1].buffer= (char *)&price;
bind[1].is_null= 0;
bind[1].length= 0;
bind[2].buffer_type= MYSQL_TYPE_DATETIME;
bind[2].buffer= (char *)&ts;
bind[2].is_null= 0;
bind[2].length= 0;
// bind parameters
if (mysql_stmt_bind_param(stmt, bind))
{
    printf("mysql_stmt_bind_param() failed\r\n");
    printf("%s\r\n", mysql_stmt_error(stmt));
    exit(0);
}
for(i=1;i<=10;i++)
{
    // set values
```

```c
sprintf(name,"product-%d",i);
str_length = strlen(name);
price = 0.23*i;
// time_t to MYSQL_TIME
struct tm *now_struct = gmtime(&now);
ts.year = now_struct->tm_year + 1900;
ts.month = now_struct->tm_mon + 1;
ts.day = now_struct->tm_mday;
ts.hour = now_struct->tm_hour;
ts.minute = now_struct->tm_min;
ts.second = now_struct->tm_sec;

printf("executing data %d...\\r\\n",i);
if (mysql_stmt_execute(stmt))
{
        printf("mysql_stmt_execute(), 1 failed\\r\\n");
        printf("%s\\r\\n", mysql_stmt_error(stmt));
        exit(0);
}
}
printf("done.\\r\\n");
printf("closing connection...\\r\\n");
/* Close the statement */
if (mysql_stmt_close(stmt))
{
        printf("failed while closing the statement\\r\\n");
        printf("%s\\r\\n", mysql_stmt_error(stmt));
        exit(0);
}
mysql_close(con);
printf("closed.\\r\\n");
exit(0);
}
```

保存该代码。

现在你可以编译并运行该文件。

```bash
$ gcc -c -I/usr/include/mysql demo-create-data.c
$ gcc -o demo-create-data demo-create-data.o -L/usr/lib/mysql -lmysqlclient
$ ./demo-create-data
```

程序输出：

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_117_0.png)

## 9.4.2 读取数据

在本节中，我们将尝试从 MySQL 读取数据。为便于演示，创建一个名为 `demo-read-data.c` 的文件，并编写如下代码。

```c
#include <my_global.h>
#include <mysql.h>
int main(int argc, char **argv)
{
    MYSQL *con = mysql_init(NULL);
    if (con == NULL)
    {
        fprintf(stderr, "%s\n", mysql_error(con));
        exit(1);
    }
    printf("connecting to mysql server...\r\n");
    // change host, username, and password
    if (mysql_real_connect(con, "localhost", "root", "password", "mydatabase", 0, NULL, 0) == NULL)
    {
        printf("error: %s\r\n", mysql_error(con));
        mysql_close(con);
        exit(1);
    }
    printf("connected.\r\n");
```

```c
printf("show data product\r\n");
if (mysql_query(con, "SELECT * FROM product"))
{
    printf("error: %s\r\n", mysql_error(con));
    mysql_close(con);
    exit(1);
}
MYSQL_RES *result = mysql_store_result(con);
if (result == NULL)
{
    printf("error: %s\r\n", mysql_error(con));
    mysql_close(con);
    exit(1);
}
int num_fields = mysql_num_fields(result);
MYSQL_ROW row;
int i;
while ((row = mysql_fetch_row(result)))
{
    for(i = 0; i < num_fields; i++)
    {
        printf("%s\t", row[i] ? row[i] : "NULL");
    }
    printf("\r\n");
}
mysql_free_result(result);
printf("closing connection...\r\n");
mysql_close(con);
printf("closed.\r\n");
exit(0);
}
```

保存该代码。

现在你可以编译并运行该文件。

```bash
$ gcc -c -I/usr/include/mysql demo-read-data.c
$ gcc -o demo-read-data demo-read-data.o -L/usr/lib/mysql -lmysqlclient
$ ./demo-read-data
```

程序输出：

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_119_0.png)

## 9.4.3 更新数据

在本节中，我们将尝试更新数据，例如更新 id=5 的数据。创建一个名为 `demo-update-data.c` 的文件，并编写如下代码。

```c
#include <my_global.h>
#include <mysql.h>
#include <string.h>
#define UPDATE_DATA "update product set name = ?, price=? where idproduct=?"
int main(int argc, char **argv)
{
    MYSQL *con = mysql_init(NULL);
    if (con == NULL)
    {
        fprintf(stderr, "%s\n", mysql_error(con));
        exit(1);
    }
```

```c
printf("connecting to mysql server...\\r\\n");
// change host, username, and password
if (mysql_real_connect(con, "localhost", "root", "password",
                       "mydatabase", 0, NULL, 0) == NULL)
{
    printf("error: %s\\r\\n", mysql_error(con));
    mysql_close(con);
    exit(1);
}
printf("connected.\\r\\n");
MYSQL_STMT *stmt;
stmt = mysql_stmt_init(con);
if (!stmt)
{
    printf(" mysql_stmt_init(), out of memory\\r\\n");
    exit(0);
}
if (mysql_stmt_prepare(stmt, UPDATE_DATA, strlen(UPDATE_DATA)))
{
    printf("mysql_stmt_prepare(), UPDATE failed\\r\\n");
```
