```
if (leftChild < heap.size() && heap[leftChild] > heap[largest]) {
    largest = leftChild;
}

if (rightChild < heap.size() && heap[rightChild] > heap[largest]) {
    largest = rightChild;
}

if (largest != index) {
    std::swap(heap[index], heap[largest]);
    heapifyDown(largest);
}
}

public:
    void insert(T value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    T extractMax() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }

        T max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);

        return max;
    }

    bool isEmpty() const {
        return heap.empty();
    }
};

int main() {
    // Using a max heap as a priority queue
```