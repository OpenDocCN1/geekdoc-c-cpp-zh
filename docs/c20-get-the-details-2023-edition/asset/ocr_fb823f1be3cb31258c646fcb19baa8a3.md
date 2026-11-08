```
Microsoft (R) C/C++ Optimizing Compiler Version 19.29.30133 for x64
Copyright (C) Microsoft Corporation. All rights reserved.

/std:c++latest is provided as a preview of language features from the latest C++
working draft, and we're eager to hear about bugs and suggestions for improvements.
However, note that these features are provided as-is without support, and subject
to changes or removal as the working draft evolves. See
https://go.microsoft.com/fwlink/?linkid=2045807 for details.

math.ixx
C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.29.30133\bin\HostX86\x64>dir
 Volume in drive C has no label.
 Volume Serial Number is 5CE7-E875

 Directory of C:\Users\seminar\build\empty

2021/08/21  11:10    <DIR>          .
2021/08/21  11:10    <DIR>          ..
2021/08/21  11:10             1,173 math.ifc
2021/08/21  11:10                90 math.ixx
2021/08/21  11:10               742 math.obj
2021/08/21  11:10               819 math.ixx
               3 File(s)          1,973 bytes
               2 Dir(s)  529,758,650,368 bytes free

C:\Users\seminar>
```

Implicitly created IFC file

For obvious reasons, I do not show the output of the program execution.

The Microsoft Visual C++ compiler provides various options for the creation of modules.

# #### 4.2.3.2.2 Module Options

The following table gives an overview of the modules compiler options.

Modules compiler options

| Modules Compiler Options | Description |
| --- | --- |
| /interface | Specifies that the input file is a module interface unit. |
| /internalPartition | Specifies that the input file is an internal partition unit. |
| /reference | Specifies that the input file is an IFC file. |
| /ifcSearchDir | Specifies the search path for the IFC file. |
| /ifcOutput | Specifies the name of the IFC file. If the name is a directory, the compiler generates a name based on the IFC file name or the header unit name. |
| /ifcOnly | Specifies that the compiler only produces an IFC file. |