```
```cpp
using namespace std::string_literals;

class CircularBuffer {
public:
    // place value into m_buffer
    void put(int value) {
        // critical section that requires a lock to modify shared data
        {
            // lock on m_mutex to be able to write to m_buffer
            std::unique_lock dataLock{m_mutex};

            // if no empty locations, wait on condition variable m_cv
            if (m_occupiedCells == m_buffer.size()) {
                std::cout << "Buffer is full. Producer waits.\n\n";

                // wait on the condition variable; the lambda argument
                // ensures that if the thread gets the processor before
                // the m_buffer has open cells, the thread continues waiting
                m_cv.wait(dataLock,
                    [&]{ return m_occupiedCells < m_buffer.size();});
            }

            m_buffer[m_writeIndex] = value; // write to m_buffer
            ++m_occupiedCells; // one more m_buffer cell is occupied
            m_writeIndex = (m_writeIndex + 1) % m_buffer.size();
            displayState(std::format("Producer writes {}", value));
        } // dataLock's destructor releases the lock on m_mutex here

        m_cv.notify_one(); // notify threads waiting to read from m_buffer
    }

    // return value from m_buffer
    int get() {
        int readValue; // will temporarily hold the next value read

        // critical section that requires a lock to modify shared data
        {
            // lock on m_mutex to be able to write to m_buffer
            std::unique_lock dataLock{m_mutex};

            // if no data to read, place thread in waiting state
            if (m_occupiedCells == 0) {
                std::cout << "Buffer is empty. Consumer waits.\n\n";

                // wait on the condition variable; the lambda argument
                // ensures that if the thread gets the processor before
                // there is data in the m_buffer, the thread continues waiting
                m_cv.wait(dataLock, [&](){ return m_occupiedCells > 0;});
            }

            readValue = m_buffer[m_readIndex]; // read value from m_buffer
```
```

**Fig. 17.9** | Synchronizing access to a shared three-element circular buffer. (Part 2 of 3.)