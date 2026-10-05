```
interface IRawInt
{
  bool this { int index } { get; set; }
}
struct RawInt : IRawInt
{
  ...
  public bool this [ int index ]
  {
    get { ... }
}
```