```
);
void abc();
void def();
void ghi();
void main() {
{
  try {
    A_main(1);
    cout<<"calling abc()\n";
    abc();
  }
  catch(char * s) {
    cout<<s<<endl;
  }
}
void abc() {
{
  A_abc(2) ;
  cout<<"calling def()\n"\n  def();
}
void def() {
{
  A_def(3) ;
  cout<<"calling ghi()\n";
  ghi();
}
void ghi() {
{
  A_ghi(4);
  throw "Exception from ghi()";
}
```

# Output

+   A 1
calling abc()
A 2
calling def()
A 3
calling ghi()
A 4
~A 4
~A 3
~A 2
~A 1
Exception from ghi

In Listing 11.8, the try block does not contain a direct call to a function throwing an exception but it calls a function that throws an exception. Still, the control jumps from the