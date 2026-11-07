```
```cpp
m_readIndex = (m_readIndex + 1) % m_buffer.size();
--m_occupiedCells; // one fewer m_buffer cells is occupied
displayState(std::format("Consumer reads {}", readValue));
} // dataLock's destructor releases the lock on mutex here

m_cv.notify_one(); // notify threads waiting to write to m_buffer
return readValue;
}

// display current operation and m_buffer state
void displayState(std::string_view operation) const {
    std::string s;

    // add operation argument and number of occupied m_buffer cells
    s += std::format("{} (buffer cells occupied: {:<15}",
        operation, m_occupiedCells, "buffer cells:");

    // add values in m_buffer
    for (int value : m_buffer) {
        s += std::format(" {:2d} ", value);
    }

    s += std::format("\n{:<15}", ""); // padding

    // add underlines
    for (int i{0}; i < m_buffer.size(); ++i) {
        s += "-----";
    }

    s += std::format("\n{:<15}", ""); // padding

    for (int i{0}; i < m_buffer.size(); ++i) {
        s += std::format("  {}  ",
            (i == m_writeIndex ? 'W' : '-'),
            (i == m_readIndex ? 'R' : '-'));
    }

    s += "\n\n";
    std::cout << s; // display the state string
}

private:
    std::condition_variable m_cv;
    std::mutex m_mutex;

    std::array<int, 3> m_buffer{-1, -1, -1}; // shared m_buffer
    int m_occupiedCells{0}; // number of buffers used
    int m_writeIndex{0}; // index of next element to write to
    int m_readIndex{0}; // index of next element to read
};
```
```

Fig. 17.9 | Synchronizing access to a shared three-element circular buffer. (Part 3 of 3.)