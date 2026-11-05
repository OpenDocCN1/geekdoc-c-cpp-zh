```
class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;
    int[,] cells = new int[NumRows, NumCols];

    public int this[char row, int col]
    {
        get {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z') {
                throw new ArgumentOutOfRangeException("row");
            }
            if (col < 0 || col >= NumCols) {
                throw new ArgumentOutOfRangeException ("col");
            }
            return cells[row - 'A', col];
        }
        set {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z') {
                throw new ArgumentOutOfRangeException ("row");
            }
            if (col < 0 || col >= NumCols) {
                throw new ArgumentOutOfRangeException ("col");
            }
            cells[row - 'A', col] = value;
        }
    }
}

end example]
```

# 15.10 Operators

# 15.10.1 General

An operator is a member that defines the meaning of an expression operator that can be applied to instances of the class. Operators are declared using operator-declarations:

operator-declaration:
    attributes_opt operator-modifiers operator-declarator operator-body
operator-modifiers:
    operator-modifier
    operator-modifiers operator-modifier
operator-modifier:
    public
    static
    extern
operator-declarator:
    unary-operator-declarator
    binary-operator-declarator
    conversion-operator-declarator
unary-operator-declarator:
    type operator overloadable-unary-operator ( fixed-parameter )
overloadable-unary-operator: one of
    +  -  !  ~  ++  --  true  false
binary-operator-declarator:
    type operator overloadable-binary-operator ( fixed-parameter , fixed-parameter )