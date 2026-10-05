```
struct BigStruct
{
    // Many, many fields here!
    ...
}
...
var myData = new BigStruct();
ProcessData(ref myData);
...
void ProcessData(ref BigStruct data)
{
    // data is a reference to myData, not a copy
    ...
}
```