```
struct Event {
    vector<int> data = vector<int>(512);
};

list<shared_ptr<Event>> q;

void producer()
{
    for (int n = 0; n!=LOTS; ++n) {
        lock_guard lk{m}; // m is a mutex; see §18.3
        q.push_back(make_shared<Event>());
        cv.notify_one(); // cv is a condition_variable; see §18.4
    }
}
```