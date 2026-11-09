# LISTING 11.6  Continued

```
```c
#include "rpcproxy.h"
#ifndef __RPCPROXY_H_VERSION__
#error this stub requires an updated version of <rpcproxy.h>
#endif // __RPCPROXY_H_VERSION__

#include "MyMidlExperiment.h"

#define TYPE_FORMAT_STRING_SIZE   1
#define PROC_FORMAT_STRING_SIZE   19

typedef struct _MIDL_TYPE_FORMAT_STRING
{
    short             Pad;
    unsigned char     Format[ TYPE_FORMAT_STRING_SIZE ];
} MIDL_TYPE_FORMAT_STRING;

typedef struct _MIDL_PROC_FORMAT_STRING
{
    short             Pad;
    unsigned char     Format[ PROC_FORMAT_STRING_SIZE ];
} MIDL_PROC_FORMAT_STRING;

extern const MIDL_TYPE_FORMAT_STRING __MIDL_TypeFormatString;
extern const MIDL_PROC_FORMAT_STRING __MIDL_ProcFormatString;

/* Object interface: IUnknown, ver. 0.0,
   GUID={0x00000000,0x0000,0x0000,
         {0xC0,0x00,0x00,0x00,0x00,0x00,0x00,0x46}} */

/* Object interface: IMyInterface, ver. 0.0,
   GUID={0xCE0056E,0x40F0,0x011D2,
         {0xBE,0xA0,0x00,0x00,0xC0,0x4F,0x8B,0x72,0xE7}} */

extern const MIDL_STUB_DESC Object_StubDesc;

extern const MIDL_SERVER_INFO IMyInterface_ServerInfo;

#pragma code_seg(".orpc")

static const MIDL_STUB_DESC Object_StubDesc =
{
    0,
    NdrOleAllocate,
```
```