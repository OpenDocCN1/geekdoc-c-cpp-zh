```
// just sleep a little
Thread.sleep( new Random().nextInt(750) );
System.out.println( "Task: " + taskNumber );
} catch ( InterruptedException ex ) { }
return Boolean.TRUE;
} }); });
fileResults = new ArrayList<Future<Boolean>>();

@Override
protected void processInput( float delta ) {
    super.processInput( delta );
    if( keyboard.keyDownOnce( KeyEvent.VK_1 ) ) {
        if( !loading ) {
            for( Callable<Boolean> task : fileTasks ) {
                fileResults.add( singleThread.submit( task ) );
            }
        }
    }
    if( keyboard.keyDownOnce( KeyEvent.VK_2 ) ) {
        if( !loading ) {
            for( Callable<Boolean> task : fileTasks ) {
                fileResults.add( thirtyTwoThreads.submit( task ) );
            }
        }
    }
    if( keyboard.keyDownOnce( KeyEvent.VK_3 ) ) {
        if( !loading ) {
            for( Callable<Boolean> task : fileTasks ) {
                fileResults.add( unlimitedThreads.submit( task ) );
            }
        }
    }
}

@Override
protected void updateObjects( float delta ) {
    super.updateObjects( delta );
    Iterator<Future<Boolean>> it = fileResults.iterator();
    while( it.hasNext() ) {
        Future<Boolean> next = it.next();
        if( next.isDone() ) {
```