```
```cpp
export class Trouble
{
public:
  explicit Trouble(std::string_view message = "There's a problem")
    : m_message{message}
  {}
  std::string what() const { return m_message; }
private:
  std::string m_message;
};
```
```

Objects of the Trouble class simply store a message indicating a problem and are thus ideally suited as simple exception objects. A default message is defined in the parameter list for the constructor, so you can use the default constructor to get an object that contains the default message. Whether you should be using such default messages is another matter entirely, of course. Remember, the idea is usually to provide information regarding the cause of the problem to aid with problem diagnosis. The `what()` member function returns the current message. To keep the logic of exception handling manageable, your functions should ensure that member functions of an exception class don’t throw exceptions. Later in this chapter, you’ll see how you can explicitly signal that a member function will never throw exceptions.

Let’s find out what happens when a class object is thrown by throwing a few. As in the previous example, we won’t bother to create errors. We’ll just throw exception objects so that you can follow what happens to them under various circumstances. We’ll exercise the exception class with a simple example that throws some exceptions in a loop:

```
```cpp
// Ex16_02.cpp
// Throw an exception object
import <iostream>;
import troubles;

void trySomething(int i);

int main()
{
  for (int i {}; i < 2; ++i)
  {
    try
    {
      trySomething(i);
    }
    catch (const Trouble& t)
    {
      // What seems to be the trouble?
      std::cout << "Exception: " << t.what() << std::endl;
    }
  }
}
```
```