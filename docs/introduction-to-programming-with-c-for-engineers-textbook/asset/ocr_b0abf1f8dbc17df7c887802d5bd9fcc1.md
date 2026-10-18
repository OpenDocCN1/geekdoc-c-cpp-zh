runtime, we have no other choice than to throw an exception, as coded on lines [128–129]. Instead of devising our own exceptions from scratch, it is a good idea to use those provided in the SL. Hence, we use std::out_of_range. But if position is in the valid range 0..kMaxNumbers, a proper digit is returned on line [131]. The type of a nibble is determined by IsFirstNibble. Finally, the ReComputeIndex function converts the value of position to the index in the fData array.

```
public:
    int GetNumberAt( int position ) const
    {
    assert( position < kMaxNumbers );
    if( position >= kMaxNumbers )
    throw std::out_of_range( "GetNumberAt position out of range" );
    return IsFirstNibble( position ) ?
    fData[ ReComputeIndex( position ) ].fFirst :
    fData[ ReComputeIndex( position ) ].fSecond;
}
```

SetNumberAt, defined on line [135], does the opposite action – it writes the value passed by val at the digit position indicated by the position parameter. The two preconditions on lines [137–138] verify the correct range of the two parameters. Again, if a position is not correct at runtime on line [139], then a std::out_of_range exception is thrown on line [140]. However, such an action is not performed if the wrong val is passed. Then, similar to GetNumberAt, on lines [141–143], a digit value is written at the correct index in the fData array.

```
void SetNumberAt( int position, int val )
{
    assert( val >= 0 && val <= 9 );  // check that we don't abuse it
    assert( position < kMaxNumbers );
    if( position >= kMaxNumbers )
    throw std::out_of_range( "SetNumberAt position out of range" );
    IsFirstNibble( position ) ?
    ( fData[ ReComputeIndex( position ) ].fFirst = val ) :
    ( fData[ ReComputeIndex( position ) ].fSecond = val );
}
```

A simple ClearAll function, defined on line [146], fills all the digits with the value 0. This is accomplished on line [148] by calling the fill member function on the fData object. As its argument, the default value of NibbleArray is passed.

```
// Resets all numbers to 0
void ClearAll( void )
{
    fData.fill( NibbleArray::value_type() );  // set all to 0
}
```

In array-like structures, it is always convenient to have the subscriber operator. A version of operator [], which lets us read only digit values, is presented on line [152]. It simply delegates the action on line [155] to the GetNumberAt function.