# **Listing 4-7. The Implementation of executeCommand()**

```
```cpp
1 void
2 CommandDispatcher::CommandDispatcherIn
3 string&
4 command)
5 {
6 double d;
7 if( isNum(command, d ) )
8 manager_.executeCommand(
9 MakeCommandPtr<EnterNumber>(d) );
10 else if(command == "undo")
11 manager_.undo();
12 else if(command == "redo")
13 manager_.redo();
14 else
15 {
16 auto c =
17 CommandRepository::Instance().allocateCom
18 if(!c)
19 {
20 ostringstream oss;
21 oss << "Command " << command << " is
```
```