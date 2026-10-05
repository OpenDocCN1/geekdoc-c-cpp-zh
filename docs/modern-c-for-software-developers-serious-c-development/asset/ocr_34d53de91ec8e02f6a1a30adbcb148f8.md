```
using ms = std::chrono::milliseconds;

int ret = m1.try_lock_for(ms(200));
if (ret == false) {
    std::cout << "resource is locked\n";
    return;
}

std::cout << "resource is not locked\n";
// this is the critical section code
balance += amount;
std::cout << "critical section processed" << std::endl;
m1.unlock();

int main() {
{
    std::cout << "balance is: " << balance << std::endl;

    m1.lock();
    std::thread t1(deposit, 100);
    t1.join();

    m1.unlock();

    std::thread t2(deposit, 100);
    t2.join();

    std::cout << "balance is: " << balance << std::endl;
}
return;
}

output:
balance is: 500
resource is locked
resource is not locked
critical section processed
balance is: 600
```

In this example, we wait for up to 200 milliseconds to acquire a lock on a shared resource.

Note that the shared resource has to be unlocked after the critical section has finished.