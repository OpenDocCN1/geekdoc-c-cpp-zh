```
```cpp
size_t chunkSize;

size_t poolSize;

public:

PoolAllocator(size_t chunkSize, size_t numChunks):
chunkSize(chunkSize), poolSize(chunkSize * numChunks) {

poolStart = operator new(poolSize);

freeList = static_cast<FreeNode*>(poolStart);

FreeNode* current = freeList;

for (size_t i = 1; i < numChunks; ++i) {

current->next = reinterpret_cast<FreeNode*>(reinterpret_cast<char*>(poolStart) + i * chunkSize);

current = current->next;

}

current->next = nullptr;
```
```