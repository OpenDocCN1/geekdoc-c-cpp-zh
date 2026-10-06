# Appendix

6. Under Configuration Properties, expand the Linker node. open the combobox next to **Additional Dependencies** and enter C:\Program Files\MySQL\MySQL Connector C 6.1.lib\libmysql.lib, as shown in the following screenshot:

![](bbox=[0.176, 0.206, 0.823, 0.549])

7. Using the Windows file explorer, navigate to C:\Program Files\MySQL\MySQL Connector C 6.1.lib. Copy the mysql.dll file to C:\Windows\System32.

Now, you can compile and run the **MultithreadedDBTest** project or any other project that uses MySQL Connector/C.

# # Installing WinDK – Driver Development Kit

In order to use Windows Driver Kit, you need to perform the following operations:

+   1. Open your web browser and navigate to http://msdn.microsoft.com/en-us/library/windows/hardware/hh852365.aspx. Since we are using Visual Studio 2013, you'll need to download WDK 8.1 or use the following address:
   http://go.microsoft.com/fwlink/link/p?LinkId=393659. The following is a screenshot of the WDK download page: