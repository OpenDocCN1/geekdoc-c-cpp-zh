To see more details about the terminated application, double-click a terminated application in Reliability Monitor. The details will look something like Figure 20-3 and the meaning of the problem signatures are described in Table 20-2. All unhandled exceptions produced by managed applications are placed in the CLR203r buffer.

![](bbox=[0.158, 0.135, 0.703, 0.493])

FIGURE 20-3 Reliability Monitor showing more details about the failed application.

# TABLE 20-2 Problem Signatures

| Problem Signature | Description* |
|---|--- |
| 01 | EXE file's name (32-character limit) |
| 02 | EXE file's assembly version number |
| 03 | EXE file timestamp |
| 04 | EXE file's full name (64-character limit) |
| 05 | Faulting assembly's version |
| 06 | Faulting assembly's timestamp |
| 07 | Faulting assembly's type (stripping off the 0x06 high byte) identifying the method that threw the exception. From this value, you can use ILDasm.exe to determine the offering type and method. |
| 08 | Faulting method's IL instruction. This value is an offset within the faulting method of the IL instruction that threw the exception. From this value, you can use ILDasm.exe to determine the offending instruction. |
| 09 | Exception type thrown (32-character limit) |

* If a string is beyond the allowed limit, then some intelligent truncations are performed, like removing "Exception" from the exception type or "dll" from a name. If the resulting string is still too long, the CLR will create a value by hashing or base64-encoding the string.