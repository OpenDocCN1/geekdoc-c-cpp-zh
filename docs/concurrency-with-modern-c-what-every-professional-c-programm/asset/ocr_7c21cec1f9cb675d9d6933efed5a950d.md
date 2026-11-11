# Exclusive mutex variations

| Member function | mutex | recursive_mutex | timed_mutex | recursive_timed_mutex |
|---|---|---|---|---|
| m.lock | yes | yes | yes | yes |
| m.try_lock | yes | yes | yes | yes |
| m.try_lock_for |  |  | yes | yes |
| m.try_lock_until |  |  | yes | yes |
| m.unlock | yes | yes | yes | yes |

A recursive mutex allows the same thread to lock the mutex many times. The mutex stays locked until it was unlocked as many times as it was locked. The maximum number of times that a recursive mutex can be locked is unspecified. If the maximum number is reached, an std::system_error¹ exception is thrown.

With C++14 we have a std::shared_timed_mutex and with C++17 a std::shared_mutex. std::shared_mutex and std::shared_timed_mutex are quite similar. You can use both mutexes for exclusive or shared locking. Additionally, with std::shared_timed_mutex you can specify a time point or a time duration.

# Shared mutex variations

| Member function | shared_timed_mutex | shared_mutex |
|---|---|---|
| m.lock | yes | yes |
| m.try_lock | yes | yes |
| m.try_lock_for | yes |  |
| m.try_lock_until | yes |  |
| m.unlock | yes | yes |
| m.lock_shared | yes | yes |
| m.try_lock_shared | yes | yes |
| m.try_lock_shared_for | yes |  |
| m.try_lock_shared_until | yes |  |

¹http://en.cppreference.com/w/cpp/error/system_error