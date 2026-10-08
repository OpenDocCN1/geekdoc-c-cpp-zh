```
template<typename C>
class Checked_iter {
public:
    using value_type = typename C::value_type;
    using difference_type = int;

    Checked_iter() { throw Missing_container(); } // concept forward_iterator requires a default constructor
    Checked_iter(const C& cc) : pc(&cc), p(pp) {} {}
    Checked_iter(const Checked_iter& cc) : pc(&cc), p(pp) {}

    Checked_iter& operator++() { check_end(); ++p; return *this; }
    Checked_iter& operator++(int) { check_end(); auto t = *this; ++p; return t; }
    value_type& operator+=(const&) { check_end(); return *p; }

    bool operator==(const Checked_iter& a) const { return p==a.p; }
    bool operator!=(const Checked_iter& a) const { return p!=a.p; }
private:
    void check_end() const { if (p == pc->end()) throw Overflow(); }
    C* pc; // default initialize to nullptr
    typename C::iterator p = pc->begin();
};

```