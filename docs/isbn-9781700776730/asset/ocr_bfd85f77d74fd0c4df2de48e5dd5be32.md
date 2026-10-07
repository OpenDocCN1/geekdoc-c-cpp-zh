```
void test7() {
  cout << "7. Testing S7, T7, U7: String assignment."
  cout << endl << endl;
  csis << "7. Testing S7, T7, U7: String assignment."
  csis << endl << endl;
  String s7("Sally Ride"), t7, u7;
  t7 = u7 = s7;
  s7.print();
  t7.print();
  u7.print();
  wait();
}

void test8() {
  cout << "8. Testing S8: String assignment."
  cout << endl << endl;
  csis << "8. Testing S8: String assignment."
  csis << endl << endl;
  String s8("ABC");
  s8 = s8;
  s8.print();
  wait();
}

void test9() {
  cout << "9. Testing S9: Implicit type conversion."
  cout << endl << endl;
  csis << "9. Testing S9: Implicit type conversion."
  csis << endl << endl;
  String s9;
  s9 = "ABC";n  s9.print();
  wait();
}

void test10() {
  cout << "10. Testing S10, T10, U10: String concatenation."
  cout << endl << endl;
  csis << "10. Testing S10, T10, U10: String concatenation."
  csis << endl << endl;
  String s10("DEF");
  String t10(\'H\');
  String u10("ABC" + s10 + "G" + t10 + 'I\');
  u10.print();
  String v10(\'X' + u10);
  v10.print();
  wait();
}
```