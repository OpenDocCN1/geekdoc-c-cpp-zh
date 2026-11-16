```
public class ReflectionVectorExample extends SimpleFramework {

    private static final float EPSILON = 0.00001f;

    private Vector2f s0, s1, p0, p1;
    private Vector2f intersection;
    private Vector2f reflection;

    public ReflectionVectorExample() {
        appTitle = "Reflection Vector Example";
        appBackground = Color.WHITE;
        appFPSCColor = Color.BLACK;
    }

    @Override
    protected void initialize() {
        super.initialize();

        s0 = new Vector2f( -0.75f, -0.3f );
        s1 = new Vector2f( 0.75f, -0.1f );
        p0 = new Vector2f();
        p1 = new Vector2f();
    }

    @Override
    protected void processInput( float delta ) {
        super.processInput( delta );

        p1 = getWorldMousePosition();
        if( mouse.buttonDownOnce( MouseEvent.BUTTON1 ) ) {
            p0 = new Vector2f( p1 );
        }
    }

    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );

        intersection = getIntersection( p0, p1, s0, s1 );
        if( intersection != null ) {
            Vector2f Sv = s1.sub( s0 );
            Vector2f n = Sv.perp().norm();
            Vector2f V = p1.sub( intersection );
            Vector2f reflect = getReflectionVector( V, n );
            reflection = intersection.add( reflect );
        } else {
            reflection = null;
        }
    }
}
```