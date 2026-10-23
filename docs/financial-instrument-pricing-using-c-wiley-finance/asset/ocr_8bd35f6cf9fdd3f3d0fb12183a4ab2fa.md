![](bbox=[0.12, 0.12, 0.88, 0.38])

# FIGURE 27.2 Wrapping legacy C++ code

+   - S2: Make the library more readable.
+   - S3: Reduce dependencies between client code and the inner workings of a library, since most code uses the façade, thus allowing more flexibility in developing the system.
+   - S4: Wrap a poorly designed collection of APIs with a single well-designed API.

The third design pattern is the Proxy:

> A proxy, in its most general form, is a class functioning as an interface to something else. The proxy could interface to anything: a network connection, a large object in memory, a file, or some other resource that is expensive or impossible to duplicate. In short, a proxy is a wrapper or agent object that is being called by the client to access the real object behind the scenes. Use of the proxy can simply be forwarding to the real object, or can provide additional logic. In the proxy, extra functionality can be provided, for example caching when operations on the real object are resource intensive, or checking preconditions before operations on the real object are invoked. For the client, usage of a proxy object is similar to using the real object, because both objects implement the same interface.

Our first application of these patterns is sketched in Figure 27.2. In this case we create a C++/CLI class that is composed of a native C++ class and whose member functions delegate to those of the latter class. In this case we are interested in wrapping functions from both Boost and Quantlib. We first create a C++/CLI Class Library dll and then a C# Console project that references this dll. To this end, the wrapper class for Boost and Quantlib (we do not show the headers here; they can be found on the distribution medium) is:

```
#include "stdafx.h"

#include "BoostMath.hpp"
#include "BVNWrapper.hpp"
```