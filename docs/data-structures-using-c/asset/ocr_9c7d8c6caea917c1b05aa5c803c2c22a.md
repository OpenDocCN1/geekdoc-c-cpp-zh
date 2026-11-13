the text editor and then recompiling it. A _template_ is a variable that can be instantiated to any data type. This data type could be of the built-in or the user-defined types. Program Code 5.4 represents a queue using templates.

# PROGRAM CODE 5.4

```
template<class T>
class queue : public Queue<T>
{
    private:
        int Front; // 1 counterclockwise from the
        Front element
        int Rear; // position of the Back element
        int ArrayLength; // queue capacity
        T *Queue; // element array
    public:
        queue(int InitialCapacity = 20);
        ~ queue()
        {
            delete[] queue;
        }
        bool Empty() const
        {
            return Front == Rear;
        }
        int Size() const
        {
            return(Rear - Front + ArrayLength) % ArrayLength;
        }
        T& Front()
        {
            if(Front == Rear)
            cout << "Sorry queue empty" << endl;
            return Queue[(Front + 1) % ArrayLength];
        }
        T& Back()
        {
            // return Rear element
            if(Front == Rear)
            cout << "Sorry queue empty" << endl;
            return Queue[Rear];
        }
        void Delete()
```