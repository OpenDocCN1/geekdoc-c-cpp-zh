and std::unique_lock to simplify mutex usage and prevent common pitfalls.

Following is the example of using a mutex with

```
```
#include

#include

#include

#include

std::mutex mu;

int sharedData = 0;

void incrementSharedData(){

std::lock_guard< mutex> lock(mu); // Locks mu upon construction
and unlocks on destruction
```
```