```
#include <random>
#include <thread>
#include <utility>
#include <vector>

using std::async;
using std::boolalpha;
using std::cout;
using std::deque;
using std::distance;
using std::for_each;
using std::find_if;
using std::future;
using std::lock_guard;
using std::make_move_iterator;
using std::make_pair;
using std::move;
using std::mt19937;
using std::mutex;
using std::packaged_task;
using std::pair;
using std::random_device;
using std::sort;
using std::thread;
using std::uniform_int_distribution;
using std::vector;

class IsPrime {
public:
    pair<bool, int> operator()(int i) {
        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) return make_pair(false, i);
        }
        return make_pair(true, i);
    }
};

class ActiveObject {
public:

    future<pair<bool, int>> enqueueTask(int i) {
        IsPrime isPrime;
        packaged_task<pair<bool, int>(int)> newJob(isPrime);
        auto isPrimeNew = newJob.get_future();
        auto pair = make_pair(move(newJob), i);
```