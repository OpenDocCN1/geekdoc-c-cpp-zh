```
void test11() {
    cout << "11. Overloaded equality operator (different size arrays): IntArray q1( 3 );"
    << endl;
    cout << "r1: "
    << endl;
    cout << endl;
    q = r;
    cs1s << "11. Overloaded equality operator (different size arrays): IntArray q1( 3 );"
    << endl;
    cs1s << "r1: "
    << endl;
    cs1s << endl;
    q = r;
    IntArray q1( 3 );
    for(int i = q1.low(); i <= q1.high(); i++)
        q1[i] = i * 10;
    q.setName("q");
    cout << q << endl;
    cs1s << q << endl;
    IntArray r1( 4 );
    for(int i = r1.low(); i <= r1.high(); i++)
        r1[i] = i * 10;
    r.setName("r");
    cout << r << endl;
    cs1s << "Returns " << ( q == r ? "True." : "False." ) << endl << endl;
    cs1s << r << endl;
    cs1s << "Returns " << ( q == r ? "True." : "False." ) << endl << endl;
    wait();
}

void test12() {
    cout << "12. Overloaded inequality operator (identical elements): IntArray s( 3, 7 );"
    << endl;
    cout << "t: "
    << endl;
    cout << endl;
    s != t;
    cs1s << "12. Overloaded inequality operator (identical elements): IntArray s( 3, 7 );"
    << endl;
    cs1s << "t: "
    << endl;
    cs1s << endl;
    s != t;
    IntArray s( 3, 7 );
    for(int i = s.low(); i <= s.high(); i++)
        s[i] = s.low();
    s.setName("s");
    cout << s << endl;
    cs1s << s << endl;
    IntArray t( 3, 7 );
    for(int i = t.low(); i <= t.high(); i++)
        t[i] = t.low();
    t.setName("t");
    cout << t << endl;
    cs1s << t << endl;
    wait();
    s = t;
    cout << s << endl;
    cs1s << s << endl;
    cout << "Returns " << ( s != t ? "True." : "False." ) << endl << endl;
    cs1s << s << endl;
    cs1s << t << endl;
    cs1s << "Returns " << ( s != t ? "True." : "False." ) << endl << endl;
    wait();
}
```