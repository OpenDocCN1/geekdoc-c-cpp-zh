Proxy and stub communicate by means of an RPC (remote procedure call) channel, which utilizes the system’s RPC infrastructure for interprocess communication. The RPC channel implements a single interface `IRpcChannelBuffer`, an internal interface to which both interface proxies and stubs hold a pointer. The proxy and stub call the interface to obtain a marshaling packet, send the data to their counterpart, and destroy the packet when they are done. The interface stub also holds a pointer to the original object.

# Defining the IID, TypeLib GUID, and CLSID

Listing 11.5 is the mymidlexperiment_i.c source file. This source file contains the definitions of the interface (IID), type library (TypeLib GUID) and class identifiers (CLSID).

**LISTING 11.5**  Output from MIDL Compiler (mymidlexperiment_i.c)

```
```c
/* this file contains the actual definitions of */
/* the IIDs and CLSIDs */

/* link this file in with the server and any clients */

/* File created by MIDL compiler version 3.03.0110 */
/* at Mon Aug 31 09:51:22 1998
*/
/* Compiler settings for MyMidlExperiment.idl:
    Oicf (OptLev=2), W1, Zp8, env=Win32, ms_ext, c_ext
    error checks: none
*/
//@@MIDL_FILE_HEADER( )
#ifdef __cplusplus
extern "C"{
#endif

#ifndef __IID_DEFINED__
#define __IID_DEFINED__

typedef struct _IID
{
    unsigned long x;
    unsigned short s1;
    unsigned short s2;
    unsigned char c[8];
} IID;

#endif // __IID_DEFINED__

#ifndef CLSID_DEFINED
#define CLSID_DEFINED
```
```