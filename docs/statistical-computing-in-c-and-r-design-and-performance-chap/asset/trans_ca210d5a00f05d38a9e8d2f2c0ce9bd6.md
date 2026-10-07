

# 366 抽象数据结构

```cpp
void Heap::downHeapify(int i, int size){
    int temp = i, newTemp;
    bool done = 0;
    while (temp + 1 <= size && !done){//还有剩余节点
        if(2*temp + 1 == size)//没有右子节点：堆的底部
            if (A.pa[temp] > A.pa[2*temp + 1]) {
                swap(temp, 2*temp + 1);
                done = 1;
            }
        else if (A.pa[2*temp + 1] < A.pa[2*temp + 2] && !done){
            if (A.pa[temp] > A.pa[2*temp + 1]) {
                swap(temp, 2*temp + 1);
                newTemp = 2*temp + 1;
            }
        else if (A.pa[2*temp + 1] >= A.pa[2*temp + 2] && !done){
            if (A.pa[temp] > A.pa[2*temp + 2]) {
                swap(temp, 2*temp + 2);
                newTemp = 2*temp + 2;
            }
        else
            done = 1;
            temp = newTemp;
        }
    }
}
```

如算法 9.12 所示，必须考虑几种情况。如果我们处于堆的底部且没有右子节点，只要父节点节点较小，就交换这两个元素。否则，将有两个子节点，父节点与键值最小的子节点交换，前提是该子节点是两者中较小的。整个过程由一个 `while` 循环管理，该循环将索引为 `i` 的节点在由大小决定的层级向下移动。另一种情况是没有任何 `if` 或 `else` 语句结果为 `true`，这意味着堆属性已经恢复。当条件为 `true` 时使用 `break` 语句的替代方案是使用临时变量 `newTemp`，在 `while` 循环执行期间存储索引值。这允许在第一个 `else` 块中重置值，而不必在迭代结束前修改 `temp` 循环变量。

`dArray` 的 `append` 方法将新对象作为堆的最后一个节点包含。然后，`upHeapify` 完成剩余工作并将节点移动到其正确位置。同样，`extractMin` 使用下方列表中的 `downHeapify` 来执行其从堆中移除最小键元素的功能。

```cpp
void Heap::insert(const int& x){
    A.append(x);
    upHeapify(A.Size - 1);
}
```

```cpp
int* Heap::extractMin(){
    if(A.Size == 1)//堆中只有1个对象
        return A.pa[0];
```

# ADT 优先级队列

```cpp
swap(A.Size - 1, 0);
A.Size--;

downHeapify(0, A.Size);

return A.pa[A.Size];
```

如果堆中只有一个元素，则将该元素返回给调用程序。否则，将顶部（或索引 0）节点与底部（A.Size - 1 索引）节点交换，并对新节点进行下堆化处理。请注意，“最小”节点并没有真正被提取出来，而是允许留在动态数组 A 中。A 的 `Size` 参数被减了，这意味着现在由“最小”值占据的槽位被 A 视为空空间。其内容将被下一个插入堆的项所覆盖。

最后，让我们考虑下一个列表中的 `heapSort` 方法。

```cpp
void Heap::heapSort(){
  for(int i = A.Size - 1; i > 0; i--){
    swap(0, i);
    downHeapify(0, i);
  }

  for(int i = 0; i <= (A.Size - 1)/2; i++){
    swap(1, A.Size - i);
  }
}
```

该方法按顺序从堆的顶部移除对象并将其插入底部，它们在底部按递减顺序排列。重排是通过逐步使用子树完成的，每一步通过排除当前的底部节点形成一个子树。例如，在第一次迭代中，代表最小键值对象的底部节点将被“排除”，以产生具有 `A.Size - 2` 个槽位的 A 子树，下一个子树将包含 A 的最后两个（非空）元素，依此类推。在排序过程结束时，对象将排列动态数组中，`heapSort` 方法反转了从左到右的顺序，使得最小键对象成为数组中的第一个元素。

作为我们 `Heap` 类的简单应用，让我们用它对图 9.1 中的值进行排序。实现此目的的程序主函数所示。

```cpp
int main(){
    Heap H(5);
    H.insert(6); H.insert(8); H.insert(12); H.insert(7);
    H.insert(9); H.insert(18); H.insert(15); H.insert(25);
    H.insert(13); H.insert(11); H.insert(10);
    H.printHeap();
    H.heapSort();
    H.printHeap();
    return 0;
}
```

首先，初始化一个堆。实现此目的的程序主函数所示。

