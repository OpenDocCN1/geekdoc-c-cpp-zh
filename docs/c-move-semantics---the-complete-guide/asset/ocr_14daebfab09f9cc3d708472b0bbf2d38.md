In this case, you are in trouble because the default generated move operation may create invalid Tasks states. Consider the following example:

```
```cpp
#include "tasksbug.hpp"
#include <iostream>
#include <chrono>
#include <exception>

int main()
{
	try {
		Tasks ts;
		ts.start([]{
			std::this_thread::sleep_for(std::chrono::seconds{2});
			std::cout << "\nt1 done" << std::endl;
		});
		ts.start([]{
			std::cout << "\nt2 done" << std::endl;
		});
		// OOPS: move tasks:
		Tasks other{std::move(ts)};
	}
	catch (const std::exception& e) {
		std::cerr << "EXCEPTION: " << e.what() << std::endl;
	}
}
```
```

At the beginning we start two tasks by passing them to the Tasks object ts. Therefore, in ts, the threads array has two entries and numThreads is 2. Unfortunately, the move operations of containers move the elements, so that after the std::move(), ts no longer contains any thread objects that represent a running thread. Therefore, numThreads is just copied, which means that we create an inconsistent/invalid state. The destructor will finally loop over the first two elements calling join(), which throws an exception (which is a fatal error in a destructor).

The general problem is that two members together define a valid state and the default generated move semantics creates an inconsistency so that even the destructor fails. You cannot always avoid this problem, because you may always explicitly have to do something with a subset of the elements an object contains when the object is destroyed. In all these cases, the default generated move operations might not work and you should either disable or fix them.

A fix might be:

+   - Fixing the destructor to deal with the moved-from state (in this case, we could, for example, only call join() if the thread object is joinable())
+   - Implementing the move operations yourself