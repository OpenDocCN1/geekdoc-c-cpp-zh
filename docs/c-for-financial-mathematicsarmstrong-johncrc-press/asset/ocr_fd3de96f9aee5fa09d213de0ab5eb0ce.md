```
```
Position::Position( Instrument* instrument ) {
instrument( instrument ) {
```

```

You should notice that the Position contains a pointer to an Instrument and not an actual Instrument. You can see this because the type of the field Instrument is Instrument*. The code below initialises a vector of Position objects that both point to the same Instrument. This achieves our goal of sharing data.

```
```cpp
vector<Position> constructPositions() {
// the caller of this function
// should call delete on the instrument
// when they are done with all the positions
vector<Position> positions;

Instrument* instrument = new Instrument;
instrument->companyName = "Google";
instrument->bloombergTicker = "GOOG US Equity";
instrument->ricCode = "GOOG.OQ";

Position p1(instrument);
p1.trader = "Han";
p1.quantity = 100.00;
positions.push_back( p1 );

Position p2(instrument);
p2.trader = "Leia";
p2.quantity = -100.00;
p2.instrument = instrument;
positions.push_back( p2 );

return positions;
}
```

```

However, there is a catch, the caller of this function has been given the task of deleting the instruments.

```
```cpp
void testConstructPositions() {
vector<Position> r = constructPositions();
int n = r.size();
for( int i=0; i<n; i++) {
cout << "Position "<<i<<"\n";
Position& p=r[i];
cout << "Trader "<<p.trader<<"\n";
cout << "Quantity "<<p.quantity<<"\n";
cout << "Instrument ";
```

```