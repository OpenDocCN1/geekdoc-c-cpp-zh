the values that have been set.
Now that we know the basics of creating packets and interacting with them through the Scapy shell, let's put this to use and build a script that will allow us to send data outside an organization using ICMP echo-replies. This type of script may be useful if most of the ports are blocked leaving an organization, but ICMP packets are allowed.

```
import sys
from scapy.all import *
conf.verb = 0
f = open(sys.argv[1])
data = f.read()
f.close()
```

To import Scapy code, we use the scapy.all module. This variation on import says to import everything from this module. This will give us full Scapy access.

# Note

So, why didn't we just import scapy.all? Note that when we use methods from sys, we have to specify sys.method to use them. With the syntax we used to import scapy.all, we don't have to use scapy.all.method to use a component of the module.

However, by importing all the contents of the Scapy framework so that we can access them easily, we have made our program use more memory. As Scapy becomes more familiar, the import list can be reduced to only the functions and classes that are needed.

We turn verbosity to zero so that we don't debug output when we send code. We will use the command line to pass arguments to the script. We will pass two things on the command line: the file to send and the host we want to send the file to. We open the first option, the file we want to send, and read it into data.

```
host = sys.argv[2]
print "Data size is %d " % len(data)
i = 0
while i < len(data):
```