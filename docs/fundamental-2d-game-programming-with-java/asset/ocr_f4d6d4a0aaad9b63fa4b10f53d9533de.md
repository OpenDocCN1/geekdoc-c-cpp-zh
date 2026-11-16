```
```java
private volatile boolean on = false;
private volatile boolean started = false;
private FakeHardware hardware;
private List<BlockingHardwareListener> listeners =
Collections.synchronizedList(
new ArrayList<BlockingHardwareListener>() );

public BlockingHardware( String name ) {
hardware = new FakeHardware( name );
hardware.addListener( new FakeHardwareListener() {
@Override
public void event( FakeHardware source, FakeHardwareEvent event ) {
handleHardwareEvent( source, event );
}
} );
}

public boolean addListener( BlockingHardwareListener listener ) {
return listeners.add( listener );
}

public void start( int ms, int slices ) {
lock.lock();
try {
hardware.start( ms, slices );
while ( !started ) {
cond.await();
}
System.out.println( "It's Started" );
} catch ( InterruptedException e ) {
e.printStackTrace();
} finally {
lock.unlock();
}
}

public void stop() {
lock.lock();
try {
hardware.stop();
while ( !started ) {
cond.await();
}
} catch ( InterruptedException ex ) {
ex.printStackTrace();
}
```
```