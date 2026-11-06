# Observers and the Standard C++ Library

![](bbox=[0.163, 0.126, 0.228, 0.201])

If you’re interested in using templates and the Standard C++ Library, you can make the `Subject` class a bit more sophisticated by using a list rather than an array. (A list allows you to easily add and remove items without constantly rebuilding the list, as you would need to do with an array.) You can do this by using the standard `list` class. The only catch is that the `list` class doesn’t seem to do well with abstract classes. So you need to “de-abstractify” your `Observer` class, which you do by setting it up like this:

```
```cpp
class Observer {
public:
  virtual void Respond() {}
};
```
```

Then you can modify the `Subject` class and its methods, like so:

```
```cpp
class Subject {
protected:
  list<Observer *> OList;
public:
  void AddObserver(Observer *Item);
  void RemoveObserver(Observer *Item);
  void Event();
};

void Subject::AddObserver(Observer *Item) {
  OList.push_back(Item);
}

void Subject::RemoveObserver(Observer *Item) {
  OList.remove(Item);
}

void Subject::Event() {
  list<Observer *>::iterator iter;
  for (iter=OList.begin(); iter!=OList.end(); iter++) {
    Observer *item = (*iter);
    item->Respond();
  }
}
```
```

Note that the list saves pointers to Observer; not the Observer instances themselves. That’s because, by default, the list class makes a copy of whatever you put in the array. If you put in an actual instance, the list class will make a copy (which creates problems with derived classes because the list copies only the