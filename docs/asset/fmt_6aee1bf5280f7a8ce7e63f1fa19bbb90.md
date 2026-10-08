
```
// 等待计算完成
for (size_t i = 0; i < NUMBER_OF_THREADS; ++i) {
    thrd_join(threads[i], NULL);
}
```
