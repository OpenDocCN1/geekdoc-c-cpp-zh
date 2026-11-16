
)?
RPAREN
SEMI
// ... RPC parameter
parameterDefinition :
IDENT // type
IDENT // name
;

The first function identifier number can be defined anywhere, even outside of the IDL file, but it's usually less confusing to keep the definition within the IDL file.

The backend of our compiler should generate these files based on the semantic information from the frontend (discovered by the parser). In general, an IDL output consists of several source code files:

- Proxy source code and its header
- Stub source code and its header

Going back and looking at Listings 6.4.1 and 6.4.2, we can see that these code patterns correlate to Listing 6.4.4, where FunctionName stands for an RPC function name, ParameterDeclarations stands for C++ declarations for all the function parameters in the RPC function, and Parameters stands for the parameter list separated by commas. See Listing 6.4.5.

## Listing 6.4.5 Our Proxy and Stub Code Pattern

```
// common
static const RPCMessage RPC_ID_FunctionName=(10+0);
//FunctionIdentifierDefinitionsForOtherFunctions

// proxy
RPCResult FunctionName(RPCSendTo sendTo, RPCSendContext sendContext, ParameterDeclarations)
{
    CMessage m;
    Message_Write(m, RPC_ID_FunctionName);
    Message_Write(m, FirstParameter);
    ...
    Message_Write(m, LastParameter);
    return RPC_Send(sendTo, sendContext, m);
}

ProxyDefinitionsForOtherFunctions

// stub
RPCResult RPC_DoStub(RPCSendTo recvFrom, RPCSendContext recvContext, CMessage& m)
{
    RPCHeader msgID;
    m.SetCursor(0);
    Message_Read(m,msgID);
    switch(msgID)
    {
    case RPC_ID_FunctionName:
    {
        FirstParameterDefinition;
        Message_Read(m,FirstParameter);
        ...
        LastParameterDefinition;
        Message_Read(m,LastParameter);
        FunctionName(
        recvFrom,
        recvContext,
        Parameters);
    }
    break;
    CasesForOtherFunctions
    }
}
```

Note that RPCHeader, RPCSendTo, and RPCSendContext are just our own local type definitions. In these examples, they're defined as unsigned int.

For simplicity, the backend code described here uses printf() or cout, with several for() statements. However, this will get cumbersome when the code patterns get more complex. So it will be helpful to adopt a text generator based on text templates such as eNTTL [Breck99].

It may be hard to keep maintaining and modifying the IDL compiler as we add more functionality to our RPC system. We can drive some parts of them into a common library, which contains several typedefs, helper functions, and some classes. The example in this article has a very little common library called MyRPC. MyRPC has a class CMessage and several read and write functions for the most frequently used primitive data types such as int, float, and std::string.

## RPC: Usage

To use our RPC implementation within our application, we should add the IDL file to our project and configure custom build options for the IDL files. In the case of Visual Studio.Net, we may configure these per Figure 6.4.4.

In addition, the compiled output files and common library need to be added to our project configurations. As the generated proxy and stub code is a kind of compilation output, it is recommended to add generated proxy and stub .h and .cpp files indirectly to your source code using #include clauses.

RPCHeader, RPCSendTo, and RPCSendContext are used for sending and receiving tasks via your networking module. If the number of RPC functions defined is under 255, a traffic conservation trick would be to change RPCHeader to unsigned char.

![](img/672fe9a2d008ba627b1991e15d70f43e_687_0.png)

FIGURE 6.4.4 Configuration of Test.IDL.

RPCSendTo identifies the remote computer that receives the messages. RPCSendContext defines other parameters such as protocol selection (TCP or UDP), timeout options, or invocation identifiers for multiple asynchronous responses. You may change these typedefs as you wish. This RPC implementation automatically adds RPCSendTo and RPCSendContext into generated RPC functions' declarations as the first and second parameter, respectively.

You then need to add a networking module to the application, because our RPC system itself doesn't have any. When the proxy constructs a message, it calls RPC_Send() to pass it to your network modules. Meanwhile, when a message is received at your network modules, it should pass the message to the stub through RPC_Stub(), which exists in the generated stub file.

## Sample Programs

There are two executable examples with this article: SimpleTest and RPCDuel. SimpleTest is basically a Hello World application. It has an IDL file and a main() function, which calls some RPC proxy functions, which just saves the generated message to its local memory. Then assuming it has already received the message sent by the proxy, it calls a stub function, which resolves the message and calls the appropriate RPC body. While trivial, it should serve as a quick example of how the more complex RPC samples work.

RPCDuel is a modified version of a simple game called Duel in the Microsoft DirectX SDK sample. RPCDuel is an example of RPC based on DirectPlay, which Duel is also based on. The original application messages have been changed to MyRPC ones, while commenting out the original portions. You can examine how RPC works by searching for the comment before RPC in the RPCDuel source files.

## Further Features

There is a proverb in Korea, “A journey of a thousand miles starts with but a single step.” Although the implementation here, as a first footstep, is written in a simple manner and only begins to show the practical use of RPC, it should be easy to improve and extend the system based on your needs. Here are some areas for improvements worth investigating.

## Allow Multiple Proxy/Stub Instances of an IDL in a Program

This implementation generates global functions and typedefs. This means there’s a limitation on multiple instantiations of the RPC functions for multiple game sessions or other re-use. One solution is to have the IDL compiler generate a proxy class and an abstract stub class, capable of handling several clients at once.

## Error Detection and Recovery

Most online game servers or peers have to program in a tolerance against erroneous messages, which may cause various exceptions such as buffer overrun, invalid message format, and networking failure. One of the solutions is to add boundary checking to our serialization and deserialization functions. Of course, if you enable your IDL grammar to accept value ranges specified by the game programmers, it may reduce having to write vulnerability checking codes.

## More Data Types

In our example, only some primitive data types such as integer, floating number, and strings have serialization and deserialization functions. However, we may want to support more data types in our RPC functions, even arrays and structures. There is a serializable class Vector3D in the SimpleTest example. It has these two functions.

```
void Message_Write(CMessage& m, const Vector3D &val);
void Message_Read(CMessage& m, Vector3D &val);
```

We can continue defining as many serialization and deserialization functions as necessary. Some C++ template functions might be more convenient for generic structures such as array and list, however.

## Message Encryption

In many online games, not all the messages need highly secured encryption, and due to performance issues, only a few types of communicated messages are made secure.

When we add an encryption option to our IDL grammar, and IDL output code pattern and encryption facilities to our streaming class, we can make use of encryption easily just with one definition such as:

```
[encrypted] RequestLogin(string id, string password);
```

## Message Compression

Message compression is easily implemented by enhancing our streaming class and our IDL grammar. For example, we may want to add a "number of bits" option for each parameter, which we can define like this:

```
Knight_Attack(int type:4,int magicBuff:7,int critical:1);
```

Variable type takes four bits and magicBuff takes seven bits, while critical takes one bit. Of course, we would then need to modify our streaming class for bitwise manipulation.

## Switch-Case Optimization

For better performance, it is also a good approach to substitute switch-cases in RPC stub to a binary search tree, to get O(logn) for n as number of RPC functions.

## Debugging and Profiling Tools

It may be easier to profile servers by adding some probe code to the RPC proxy and stub code templates. For example, when we want to trace every incoming or outgoing message, we can do so just by adding code that prints the function name and parameter values to console or debug output. Of course, we can also view the trace log records showing what functions and parameters have been passed. This is a great way to help detect vulgarity received from a bad game client or RPC body functions that cause long process times.

## Synchronous RPC

Most games will typically not require synchronous RPC; however, if it is needed for your programs, you can add this faculty to your RPC at runtime.

Adding synchronous RPC to our example requires some more work:

- We need to define more sequences that wait until the RPC body returns and passes the return values to the RPC function caller.
- Only guaranteed messages are acceptable with synchronous RPC.
- We need to add a parameter direction option, which are input parameters (inparam) and output parameters (outparam). Inparam is sent to the RPC server
