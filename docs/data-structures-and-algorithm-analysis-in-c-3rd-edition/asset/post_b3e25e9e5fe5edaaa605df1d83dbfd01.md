
```cpp
// Linked queue implementation
template <typename E> class LQueue: public Queue<E> {
private:
    Link<E>* front;        // Pointer to front queue node
    Link<E>* rear;         // Pointer to rear queue node
    int size;              // Number of elements in queue

public:
    LQueue(int sz = defaultSize) // Constructor
    { front = rear = new Link<E>(); size = 0; }

    ~LQueue() { clear(); delete front; }        // Destructor

    void clear() {              // Clear queue
        while(front->next != NULL) { // Delete each link node
            rear = front->next;
            front->next = rear->next;
            delete rear;
        }
        rear = front;
        size = 0;
    }

    void enqueue(const E& it) { // Put element on rear
        rear->next = new Link<E>(it, NULL);
        rear = rear->next;
        size++;
    }

    E dequeue() {               // Remove element from front
        Assert(size != 0, "Queue is empty");
        E it = front->next->element;  // Store dequeued value
        Link<E>* ltemp = front->next; // Hold dequeued link
        front->next = ltemp->next;    // Advance front
        if (rear == ltemp) rear = front; // Dequeue last element
        delete ltemp;                  // Delete link
        size--;
        return it;                     // Return element value
    }

    const E& frontValue() const { // Get front element
        Assert(size != 0, "Queue is empty");
        return front->next->element;
    }

    virtual int length() const { return size; }
};
```

Figure 4.27 Linked queue class implementation.

are equal or not. That is enough to enable a sequential search through a database of records and find one that matches a given key. However, we typically would like for the keys to define a total order (see Section 2.1), which means that we can tell which of two keys is greater than the other. Using key types with total orderings gives the database implementor the opportunity to organize a collection of records in a way that makes searching more efficient. An example is storing the records in sorted order in an array, which permits a binary search. Fortunately, in practice most fields of most records consist of simple data types with natural total orders. For example, integers, floats, doubles, and character strings all are totally ordered. Ordering fields that are naturally multi-dimensional, such as a point in two or three dimensions, present special opportunities if we wish to take advantage of their multidimensional nature. This problem is addressed in Section 13.3.

Figure 4.28 shows the definition for a simple abstract dictionary class. The methods insert and find are the heart of the class. Method insert takes a record and inserts it into the dictionary. Method find takes a key value and returns some record from the dictionary whose key matches the one provided. If there are multiple records in the dictionary with that key value, there is no requirement as to which one is returned.

Method clear simply re-initializes the dictionary. The remove method is similar to find, except that it also deletes the record returned from the dictionary. Once again, if there are multiple records in the dictionary that match the desired key, there is no requirement as to which one actually is removed and returned. Method size returns the number of elements in the dictionary.

The remaining method is removeAny. This is similar to remove, except that it does not take a key value. Instead, it removes an arbitrary record from the dictionary, if one exists. The purpose of this method is to allow a user the ability to iterate over all elements in the dictionary (of course, the dictionary will become empty in the process). Without the removeAny method, a dictionary user could not get at a record of the dictionary that he didn’t already know the key value for. With the removeAny method, the user can process all records in the dictionary as shown in the following code fragment.

```cpp
while (dict.size() > 0) {
    it = dict.removeAny();
    doSomething(it);
}
```

There are other approaches that might seem more natural for iterating through a dictionary, such as using a “first” and a “next” function. But not all data structures that we want to use to implement a dictionary are able to do “first” efficiently. For example, a hash table implementation cannot efficiently locate the record in the table with the smallest key value. By using removeAny, we have a mechanism that provides generic access.

```cpp
// The Dictionary abstract class.
template <typename Key, typename E>
class Dictionary {
private:
    void operator =(const Dictionary&) {}
    Dictionary(const Dictionary&) {}
public:
    Dictionary() {} // Default constructor
    virtual ~Dictionary() {} // Base destructor
    // Reinitialize dictionary
    virtual void clear() = 0;
    // Insert a record
    // k: The key for the record being inserted.
    // e: The record being inserted.
    virtual void insert(const Key& k, const E& e) = 0;
    // Remove and return a record.
    // k: The key of the record to be removed.
    // Return: A matching record. If multiple records match
    // "k", remove an arbitrary one. Return NULL if no record
    // with key "k" exists.
    virtual E remove(const Key& k) = 0;
    // Remove and return an arbitrary record from dictionary.
    // Return: The record removed, or NULL if none exists.
    virtual E removeAny() = 0;
    // Return: A record matching "k" (NULL if none exists).
    // If multiple records match, return an arbitrary one.
    // k: The key of the record to find
    virtual E find(const Key& k) const = 0;
    // Return the number of records in the dictionary.
    virtual int size() = 0;
};
```

Figure 4.28 The ADT for a simple dictionary.

```cpp
// A simple payroll entry with ID, name, address fields
class Payroll {
private:
    int ID;
    string name;
    string address;

public:
    // Constructor
    Payroll(int inID, string inname, string inaddr) {
        ID = inID;
        name = inname;
        address = inaddr;
    }

    ~Payroll() {}  // Destructor

    // Local data member access functions
    int getID() { return ID; }
    string getname() { return name; }
    string getaddr() { return address; }
};
```

Figure 4.29 A payroll record implementation.

Given a database storing records of a particular type, we might want to search for records in multiple ways. For example, we might want to store payroll records in one dictionary that allows us to search by ID, and also store those same records in a second dictionary that allows us to search by name.

Figure 4.29 shows an implementation for a payroll record. Class Payroll has multiple fields, each of which might be used as a search key. Simply by varying the type for the key, and using the appropriate field in each record as the key value, we can define a dictionary whose search key is the ID field, another whose search key is the name field, and a third whose search key is the address field. Figure 4.30 shows an example where Payroll objects are stored in two separate dictionaries, one using the ID field as the key and the other using the name field as the key.

```cpp
int main() {
    // IDdict organizes Payroll records by ID
    UALdict<int, Payroll*> IDdict;
    // namedict organizes Payroll records by name
    UALdict<string, Payroll*> namedict;
    Payroll *foo1, *foo2, *findfoo1, *findfoo2;

    foo1 = new Payroll(5, "Joe", "Anytown");
    foo2 = new Payroll(10, "John", "Mytown");

    IDdict.insert(foo1->getID(), foo1);
    IDdict.insert(foo2->getID(), foo2);
    namedict.insert(foo1->getname(), foo1);
    namedict.insert(foo2->getname(), foo2);

    findfoo1 = IDdict.find(5);
    if (findfoo1 != NULL) cout << findfoo1;
    else cout << "NULL ";
    findfoo2 = namedict.find("John");
    if (findfoo2 != NULL) cout << findfoo2;
    else cout << "NULL ";
}
```

Figure 4.30 A dictionary search example. Here, payroll records are stored in two dictionaries, one organized by ID and the other organized by name. Both dictionaries are implemented with an unsorted array-based list.

The fundamental operation for a dictionary is finding a record that matches a given key. This raises the issue of how to extract the key from a record. We would like any given dictionary implementation to support arbitrary record types, so we need some mechanism for extracting keys that is sufficiently general. One approach is to require all record types to support some particular method that returns the key value. For example, in Java the Comparable interface can be used to provide this effect. Unfortunately, this approach does not work when the same record type is meant to be stored in multiple dictionaries, each keyed by a different field of the record. This is typical in database applications. Another, more general approach is to supply a class whose job is to extract the key from the record. Unfortunately, this solution also does not work in all situations, because there are record types for which it is not possible to write a key extraction method.²

The fundamental issue is that the key value for a record is not an intrinsic property of the record’s class, or of any field within the class. The key for a record is actually a property of the context in which the record is used.

A truly general alternative is to explicitly store the key associated with a given record, as a separate field in the dictionary. That is, each entry in the dictionary will contain both a record and its associated key. Such entries are known as key-value pairs. It is typical that storing the key explicitly duplicates some field in the record. However, keys tend to be much smaller than records, so this additional space overhead will not be great. A simple class for representing key-value pairs is shown in Figure 4.31. The insert method of the dictionary class supports the key-value pair implementation because it takes two parameters, a record and its associated key for that dictionary.

> ²One example of such a situation occurs when we have a collection of records that describe books in a library. One of the fields for such a record might be a list of subject keywords, where the typical record stores a few keywords. Our dictionary might be implemented as a list of records sorted by keyword. If a book contains three keywords, it would appear three times on the list, once for each associated keyword. However, given the record, there is no simple way to determine which keyword on the keyword list triggered this appearance of the record. Thus, we cannot write a function that extracts the key from such a record.
