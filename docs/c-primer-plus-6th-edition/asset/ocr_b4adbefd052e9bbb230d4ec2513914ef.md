```
// template prototypes
template <typename T> void counts();
template <typename T> void report(T &);

// template class
template <typename TT>
class HasFriendT {
private:
    TT item;
    static int ct;
public:
    HasFriendT(const TT & i) : item(i) {ct++;}
    ~HasFriendT() {ct--;}
    friend void counts<TT>();
    friend void report(HasFriendT<TT> &);
};

template <typename T>
int HasFriendT<T>::ct = 0;

// template friend functions definitions
template <typename T>
void counts() {
    cout << "template size: " << sizeof(HasFriendT<T>) << " ";
    cout << "template counts(): " << HasFriendT<T>::ct << endl;
}

template <typename T>
void report(T &T) {
    cout << T.item << endl;
}

int main() {
    counts<int>();
    HasFriendT<int> hf1(10);
    HasFriendT<int> hf2(20);
    HasFriendT<double> hfdb(10.5);
    report(hf1); // generate report (HasFriendT<int> &)
    report(hf2); // generate report (HasFriendT<int> &)
    report(hfdb); // generate report (HasFriendT<double> &)
    cout << "counts<int>() output:\n";
    counts<int>();
}
```