```
commander const& get_commander() const;

private:
    mutable commander* m_commander; // Immune from const constraint

    template <class T>
    static auto get_commander_impl(T& t)
        -> decltype(t.get_commander) {
        if (!t.m_commander->is_alive()) {
            ... // Find the new commander
            t.m_commander = new_commander; // Always
amenable to change
        }
        return *t.m_commander;
    }
};
```

The m_commander member is now mutable. This means it is amenable to modification from a const reference.

# Surprises with const

Obviously, mutable should not be scattered liberally through your class. It should decorate the data that is used for bookkeeping, rather than for modeling the abstraction. In the case of decorating a mutex member, we can see that this is a sensible policy. In the above example, though, it is not so clear. Raw pointers are confusing things that muddy the waters of ownership, as discussed in Core Guideline I.11: “Never transfer ownership by a raw pointer (T*) or reference (T&),” and they also trip up API design when it comes to separating the view from the controller.

For example, this piece of code is legal: