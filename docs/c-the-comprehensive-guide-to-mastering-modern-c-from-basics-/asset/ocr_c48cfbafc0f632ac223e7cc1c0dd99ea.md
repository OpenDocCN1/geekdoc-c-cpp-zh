```
    return sHash(a.city_j);
}
int main() {
    unordered_multiset<Entry, Hash, EqEntry> directory({
        Entry("New York", 10001);
        Entry("New York", 10002);
        Entry("New York", 10003);
        Entry("Chicago", 60601);
        Entry("Chicago", 60602);
    });
    const Entry search("New York", // ZIP code does not matter in search
    cout << "New York has " << directory.count(search) << " ZIP codes.\n";
    cout << "The ZIP codes of New York are:\n";
    auto (where, until) = directory.equal_range(search);
    while (where != until) {
        cout << where->zip_j << '\n';
    }
}
```

# **Listing 24.85** You can use only part of your object as a key.

The output, of course, is as follows:

New York has 3 ZIP codes.
The ZIP codes of New York are:
10001
10002
10003

The EqEntry and HashEntry functors, which are specified as template arguments, ensure that all entries with the same city_name are considered equal. It would not be enough to define only the hash function or only the equality; both operations must match as-otherwise otherwise the entries will get mixed up and not end up in the correct buckets. Therefore, you must carefully select and program the two functors.

For example, if you include more elements in equality in the hash function, you will not find an entry with count(search), but only with count(Entry("New York", 10001)). It may be that this is what you wanted, but then your hash function is not optimal, and you should have included zip_:

```
struct EqEntry {
    bool operator()(const EqEntry& a, const EqEntry& b) const {
        return tie(a.city_j, a.zip_j) == tie(b.city_j, b.zip_j); // Really?
    }
}
struct HashEntry {
    std::hash sHash;
    size_t operator()(const HashEntry& a) const {
        return sHash(a.city_j);
    }
}
```