If multiple fire() events are sent to the event task while it is already running, they are simply ignored.

```
package javagames.threads;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;
public class LoopEvent implements Runnable {
	private enum State {
		WAITING,
		RUNNING;
	};
	private enum Event {
		FIRE,
		RESTART,
		DONE;
	};
	private BlockingQueue<Event> queue;
	private BlockingHardware hardware;
	private State currentState;
	private Thread consumer;
	private int ms;
	private int slices;
	public LoopEvent( int ms, int slices ) {
		this.ms = ms;
		this.slices = slices;
	}
	public void initialize() {
		hardware = new BlockingHardware( "looper" );
		hardware.addListener( getListener() );
		queue = new LinkedBlockingQueue<Event>();
		currentState = State.WAITING; // default state
		// start the consumer thread
		consumer = new Thread( this );
		consumer.start();
	}
	public void fire() {
		try {
			queue.put( Event.FIRE );
```