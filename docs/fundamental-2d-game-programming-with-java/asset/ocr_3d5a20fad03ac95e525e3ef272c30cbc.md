```
```java
Element xml = loadXML( "ship.xml" );
factory.loadFactory( xml );
controller.setAttribute( "ship-factory", factory );
Acme acme = (Acme)controller.getAttribute( "ACME" );
acme.setShip( factory.createShip() );
return Boolean.TRUE;
});
```
```

```
```java
loadTasks.add( new Callable<Boolean>() {
@Override
public Boolean call() throws Exception {
byte[] soundBytes = loadSound( "DRONE9RE.WAV" );
QuickLooper clip = new QuickLooper( new BlockingDataLine( soundBytes ) );
clip.initialize();
clip.open();
controller.setAttribute( "thruster-clip", clip );
return Boolean.TRUE;
});
```
```

```
```java
loadTasks.add( new Callable<Boolean>() {
@Override
public Boolean call() throws Exception {
byte[] soundBytes = loadSound( "WEAPON_sifi_fire_02.wav" );
QuickRestart restartClip = new QuickRestart( new BlockingDataLine(
soundBytes
));
restartClip.initialize();
restartClip.open();
controller.setAttribute( "fire-clip", restartClip );
return Boolean.TRUE;
});
```
```

```
```java
loadTasks.add( new Callable<Boolean>() {
@Override
public Boolean call() throws Exception {
ArrayList<QuickRestart> explosion =
new ArrayList<QuickRestart>();
for( String path : explosions ) {
byte[] soundBytes = loadSound( path );
```
```