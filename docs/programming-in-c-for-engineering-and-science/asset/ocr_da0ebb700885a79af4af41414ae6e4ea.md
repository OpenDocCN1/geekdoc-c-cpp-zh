```
if (address == "STOP") break;

chopIPAddress(address, block1, block2, block3, block4);

cout << "The network/host blocks are:\n" << block1 << endl << block2 << endl << block3 << endl << block4 << endl;
}
```

```
/* Function to find the four network/host information blocks in a TCP/IP address.
Receive: TCP/IP address
Pass back: four network/host information blocks
Output: an error message if address is malformed
--------------------------------------------------------------------------*/
```

```
void chopIPAddress(const string & address, string & block1, string & block2, string & block3, string & block4)
{
int dot1 = address.find(".", 0);
assert(dot1 != string::npos);
block1 = address.substr(0, dot1);

int dot2 = address.find(".", dot1 + 1);
assert(dot2 != string::npos);
block2 = address.substr(dot1 + 1, dot2 - dot1 - 1);

int dot3 = address.find(".", dot2 + 1);
assert(dot3 != string::npos);
lock3 = address.substr(dot2 + 1, dot3 - dot2 - 1);

assert(address.find(".", dot3 + 1) == string::npos);
block4 = address.substr(dot3 + 1, address.size() - dot3 - 1);
}
```

# SAMPLE RUNS:

Enter an IP address (STOP to quit): titan.ksc.nasa.gov
The network/host blocks are:
titan
ksc
nasa
gov

Enter an IP address (STOP to quit): 163.205.10.1
The network/host blocks are:
163
205
10
1

Enter an IP address (STOP to quit): STOP