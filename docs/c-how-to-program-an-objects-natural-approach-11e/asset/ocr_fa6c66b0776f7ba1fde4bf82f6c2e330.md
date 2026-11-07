```
```cpp
#include <vector>

// get current thread's ID as a string
std::string id() {
    std::ostringstream out;
    out << std::this_thread::get_id();
    return out.str();
}

// Function printTask sleeps for a specified period in milliseconds.
// When it continues executing, it prints its name and completes.
void printTask(std::string name, std::chrono::milliseconds sleep) {
    std::cout << std::format(
        "{} (thread ID: {}) going to sleep for {} ms\n",
        name, id(), sleep.count());

    // put the calling thread to sleep for sleep milliseconds
    std::this_thread::sleep_for(sleep);

    std::cout << std::format("{} (thread ID: {}) done sleeping\n",
        name, id());
}

int main() {
    // set up the concurrencypp runtime for scheduling tasks to execute
    concurrencypp::runtime runtime;

    std::cout << std::format("main's thread ID: {}\n\n", id());

    // set up random number generation for random sleep times
    std::random_device rd;
    std::default_random_engine engine{rd()};
    std::uniform_int_distribution<int> sleepTimes{0, 5000};

    // stores the tasks so we can wait for them to complete later;
    // concurrencypp::result<void> indicates that each task returns void
    std::vector<concurrencypp::result<void>> results;

    std::cout << "STARTING THREE CONCURRENCYPP TASKS\n";

    // schedule three tasks
    for (int i{1}; i < 4; ++i) {
        std::chrono::milliseconds sleepTime{sleepTimes(engine)};
        std::string name{std::format("Task {}", i)};

        // use a concurrencypp thread_pool_executor to schedule a call
        // to printTask with name and sleepTime as its arguments
        results.push_back(runtime.thread_pool_executor()->submit(
            printTask, name, sleepTime));
    }

    std::cout << "\nALL TASKS STARTED\n";
    std::cout << "\nWAITING FOR TASKS TO COMPLETE\n";
}
```
```

**Fig. 18.2** | Setting up the `concurrencypp::runtime` and scheduling tasks with it. (Part 2 of 3.)