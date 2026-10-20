```
```cpp
not a known command"; 18 ui_.postMessage(
oss.str());
19 }
20 else
21 {
22 try
23 {
24 manager_.executeCommand( std::move(c)
);
25 }
26 catch(Exception& e)
27 {
28 ui_.postMessage( e.what() );
29 }
30 }
31 }
32
33 return;
34 }
```
```

Lines 5-10 handle special commands. A special command is any command that is not entered in the command repository. In the code above, this includes entering a new number, undo, and redo. If a special command is not encountered, then it is