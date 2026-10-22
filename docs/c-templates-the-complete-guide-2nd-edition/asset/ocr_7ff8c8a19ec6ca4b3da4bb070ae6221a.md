```
class SomeCompilerSpecificNameY {
    private
        int _x, _y;
    public:
        SomeCompilerSpecificNameY(int x, int y) // only callable by the compiler
            : _x(x), _y(y) {
        }
        bool operator() (int i) const {
            return i > _x && i < _y;
        }
};
```