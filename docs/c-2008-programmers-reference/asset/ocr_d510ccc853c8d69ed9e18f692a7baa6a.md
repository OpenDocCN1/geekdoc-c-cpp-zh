```
~~~csharp
        {
            _elements = new object[size];
            _pointer = 0;
        }

        public void Push(object item)
        {
            if (_pointer > _elements.Length - 1)
            {
                throw new Exception("Stack is full.");
            }
            _elements[_pointer] = item;
            _pointer++;
        }

        public object Pop()
        {
            _pointer--;
            if (_pointer < 0)
            {
                throw new Exception("Stack is empty.");
            }
            return _elements[_pointer];
        }
    }
~~~
```

One problem with this approach is that when you use the stack class, you may inadvertently pop out the wrong data type, as shown in the following highlighted code:

```
~~~csharp
            MyStack stack = new MyStack(3);
            stack.Push(1);
            stack.Push(2);
            stack.Push("A");

            //---invalid cast---
            int num = (int) stack.Pop();
~~~
```

Because the Pop() method returns a variable of Object type, IntelliSense cannot detect during design time if this code is correct. It is only during runtime that when you try to pop out a string type and try to typecast it into an int type that an error occurs. Besides, type casting (boxing and unboxing) during runtime incurs a performance penalty.

To resolve this inflexibility, you can make use of generics.