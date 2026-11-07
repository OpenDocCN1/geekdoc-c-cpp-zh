```
```cpp
++sharedData;

std::cout << "Data incremented to " << sharedData << std::endl;

}

int main() {

std::vector<std::thread> threads;

for(int i = 0; i < 5; ++i) {

threads.emplace_back(incrementSharedData);

}

for (auto& t : threads) {

t.join();

}

return 0;
```
```