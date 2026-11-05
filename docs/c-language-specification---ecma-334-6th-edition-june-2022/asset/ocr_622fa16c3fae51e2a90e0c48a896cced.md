```
abstract class C : IMethods
{
    public abstract void F();
    public abstract void G();
}
```

Here, the implementation of IMethods maps F and G onto abstract methods, which shall be overridden in non-abstract classes that derive from C.

end example

Explicit interface member implementations cannot be abstract, but explicit interface member implementations are of course permitted to call abstract methods.

Example:

```
interface IMethods
{
    void F();
    void G();
}
```

```
abstract class C: IMethods
{
    void IMethods.F() { FF(); }
    void IMethods.G() { GG(); }
    protected abstract void FF();
    protected abstract void GG();
}
```

Here, non-abstract classes that derive from C would be required to override FF and GG, thus providing the actual implementation of IMethods.

end example