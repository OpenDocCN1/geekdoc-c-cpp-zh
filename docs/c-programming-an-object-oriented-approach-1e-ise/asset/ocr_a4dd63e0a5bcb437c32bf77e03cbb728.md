An *association* between two classes shows the relationship between them. *Aggregation* is a special kind of association in which the relationship involves ownership, a “has-a” relationship. A *composition* is a special kind of aggregation in which the lifetime of the contained depends on the lifetime of the container.

*Dependency* is a weak relationship between classes. It models the “uses” relationship.

# Problems

**PR-1.** Assume we have defined the following two classes. Write the definition of the *set* and *print* functions for both classes using delegation.

```
```cpp
// Declaration of the class First
class First
{
    private:
        int a;
    public:
        void set (int a);
        void print () const;
};
// Declaration of the class Second
class Second : public First
{
    private:
        int b;
    public:
        void set (int a, int b);
        void print () const;
};
```
```

**PR-2.** Assume we have defined the following two classes. Write the definition of the *set* and *print* functions for both classes without using delegation.

```
```cpp
// Declaration of the class First
class First
{
    protected:
        int a;
    public:
        void set (int a);
        void print () const;
};
// Declaration of the class Second
class Second : public First
{
    private:
        int b;
    public:
        void set (int a, int b);
        void print () const;
};
```
```