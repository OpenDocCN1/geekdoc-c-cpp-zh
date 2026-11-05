| Code | Category |
|------|----------|
| `public void Add(T item) { if (count == Capacity) Capacity = count * 2; items[count] = item; count++; OnChanged(); } protected virtual void OnChanged() { if (Changed != null) Changed(this, EventArgs.Empty); } public override bool Equals(object other) { return Equals(this, other as List<T>); } static bool Equals(List<T> a, List<T> b) { if (a == null) return b == null; if (b == null || a.count != b.count) return false; for (int i = 0; i < a.count; i++) { if (!object.Equals(a.items[i], b.items[i])) { return false; } } return true; }` | Methods |
| `public event EventHandler Changed;` | Event |
| `public static bool operator ==(List<T> a, List<T> b) { return Equals(a, b); } public static bool operator !=(List<T> a, List<T> b) { return !Equals(a, b); }` | Operators |
| `}` |  |

# 1.6.7.1 Constructors

C# supports both instance and static constructors. An instance constructor is a member that implements the actions required to initialize an instance of a class. A static constructor is a member that implements the actions required to initialize a class itself when it is first loaded.

A constructor is declared like a method with no return type and the same name as the containing class. If a constructor declaration includes a static modifier, it declares a static constructor. Otherwise, it declares an instance constructor.