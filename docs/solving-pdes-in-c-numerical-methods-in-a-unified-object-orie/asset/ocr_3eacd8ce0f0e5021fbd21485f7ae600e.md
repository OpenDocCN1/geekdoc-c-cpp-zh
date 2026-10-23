The copy constructor and assignment operator are only declared in the class block above. Here is the actual definition:

```
template<class T>
list<T>::list(const list<T>&l):number(l.number),
  item(l.number ? new T*[l.number] : 0){
    for(int i=0; i<l.number; i++)
      if(l.item[i])
        item[i] = new T(*l.item[i]);
      else
        item[i] = 0;
  } // copy constructor
```

Here is the definition of the assignment operator:

```
template<class T>
const list<T>&
list<T>::operator=(const list<T>& l){
  if(this != &l){
```

We have just entered the "if" block that makes sure that the assignment operator has not been called by a trivial call of the form "l = l". Now, we make sure that the current list contains the same number of items as the list "l" that is passed as an argument. (In other words, the array "item[]" is modified to have the same dimension as the array "l.item[]"):

```
if(number != l.number){
  delete [] item;
  item = new T*[l.number];
}
```

We can now go ahead and copy the items in 'l' to the current "list" object:

```
for(int i = 0; i < l.number; i++)
  if(l.item[i])
    item[i] = new T(*l.item[i]);
  else
    item[i] = 0;
  number = l.number;
}
return *this;
} // assignment operator
```

Finally, we implement the function that prints the items in the list to the screen:

```
template<class T>
void print(const list<T>&l){
  for(int i=0; i<l.size(); i++){
    printf("i=%d:\n",i);
    print(l[i]);
  }
} // printing a list
```