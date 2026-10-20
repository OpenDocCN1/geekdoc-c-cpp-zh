```
// Time2 constructor: hour and minute supplied, second defaulted to 0
public Time2( int h, int m )
{
    this( h, m, 0 ); // invoke Time2 constructor with three arguments
} // end Time2 two-argument constructor

// Time2 constructor: hour, minute and second supplied
public Time2( int h, int m, int s )
{
    setTime( h, m, s ); // invoke setTime to validate time
} // end Time2 three-argument constructor

// Time2 constructor: another Time2 object supplied
public Time2( Time2 time )
{
    // invoke Time2 three-argument constructor
    this( time.getHour(), time.getMinute(), time.getSecond() );
} // end Time2 constructor with a Time2 object argument

// Set Methods
// set a new time value using universal time;
// validate the data
public void setTime( int h, int m, int s )
{
    setHour( h ); // set the hour
    setMinute( m ); // set the minute
    setSecond( s ); // set the second
} // end method setTime

// validate and set hour
public void setHour( int h )
{
    if ( h >= 0 && h < 24 )
        hour = h;
    else
        throw new IllegalArgumentException( "hour must be 0-23" );
} // end method setHour

// validate and set minute
public void setMinute( int m )
{
    if ( m >= 0 && m < 60 )
        minute = m;
    else
        throw new IllegalArgumentException( "minute must be 0-59" );
} // end method setMinute

// validate and set second
public void setSecond( int s )
{
    if ( s >= 0 && s < 60 )
        second = ( ( s >= 0 && s < 60 ) ? s : 0 );
```