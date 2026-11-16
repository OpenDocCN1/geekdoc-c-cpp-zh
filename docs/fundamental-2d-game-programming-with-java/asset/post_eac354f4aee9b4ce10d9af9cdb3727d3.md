
```java
remove( asteroid );
bullets.remove( bullet );
explosions.add(
    new AsteroidExplosion( bullet.getPosition() )
);
explosion[ rand.nextInt( explosion.length ) ].fire();
}
}

private void remove( Asteroid asteroid ) {
    asteroids.remove( asteroid );
    state.updateScore( asteroid.getSize() );
    spawnBabies( asteroid );
}

private void spawnBabies( Asteroid asteroid ) {
    if ( asteroid.getSize() == Size.Large ) {
        asteroids.add(
            factory.getMediumAsteroid( asteroid.getPosition() )
        );
        asteroids.add(
            factory.getMediumAsteroid( asteroid.getPosition() )
        );
    }
    if ( asteroid.getSize() == Size.Medium ) {
        asteroids.add( factory.getSmallAsteroid( asteroid.getPosition() ) );
        asteroids.add( factory.getSmallAsteroid( asteroid.getPosition() ) );
    }
}

private boolean shouldRespawn() {
    return !ship.isAlive() && shipExplosion == null;
}

private void processRespawnShip( double delta ) {
    respawn += delta;
    if ( respawn > 1.0 ) {
        if ( state.getLives() > 0 ) {
            respawn = 0.0;
            state.setLives( state.getLives() - 1 );
            createShip( true );
        } else {
            getController().setState( new GameOver( asteroids, state ) );
        }
    }
}

private void checkForLevelWon() {
    if ( asteroids.isEmpty() && explosions.isEmpty() ) {
        state.setLevel( state.getLevel() + 1 );
        thruster.done();
        getController().setState( new LevelStarting( state ) );
    }
}

private void updateAsteroidExplosions( float delta ) {
    for( AsteroidExplosion explosion : new ArrayList<AsteroidExplosion>( explosions ) ) {
        explosion.update( delta );
        if( explosion.isFinished() ) {
            explosions.remove( explosion );
        }
    }
}

private void updateShipExplosion( float delta ) {
    if( shipExplosion != null ) {
        shipExplosion.update( delta );
        if( shipExplosion.isFinished() ) {
            shipExplosion = null;
        }
    }
}

@Override
public void render( Graphics2D g, Matrix3x3f view ) {
    background.render( g, view );
    ship.draw( g, view );
    for( Asteroid a : asteroids ) {
        a.draw( g, view );
    }
    for( AsteroidExplosion ex : explosions ) {
        ex.render( g, view );
    }
    for( Bullet b : bullets ) {
        b.draw( g, view );
    }
    if( shipExplosion != null ) {
        shipExplosion.render( g, view );
    }
    acme.drawLives( g, view, state.getLives() );
    acme.drawScore( g, state.getScore() );
}
```

## THE GAMEOVER STATE

The GameOver state, as shown in Figure 17.7, is entered when the player runs out of lives.

![](img/588a4cda8f2acae94a7e1987bf99400d_616_0.png)

Figure 17.7
Game Over.
© 2014 Timothy Wright.

If the score is large enough to make it into the top ten, the EnterHighScoreName state is reached. Otherwise, the HighScore attract state is entered and the attract state loop continues until the player starts another game or quits the application.

```java
package javagames.completegame.state;

import java.awt.Graphics2D;
import java.util.List;

import javagames.completegame.object.*;
import javagames.util.Matrix3x3f;
import javagames.util.Utility;

public class GameOver extends AttractState {
    GameState state;
    public GameOver( List<Asteroid> asteroids, GameState state ) {
        super( asteroids );
        this.state = state;
    }

    @Override
    protected float getWaitTime() {
        return 3.0f;
    }

    @Override
    protected AttractState getState() {
        if( highScoreMgr.newHighScore( state ) ) {
            return new EnterHighScoreName( state );
        } else {
            return new HighScore();
        }
    }

    @Override
    public void render( Graphics2D g, Matrix3x3f view ) {
        super.render( g, view );
        acme.drawScore( g, state.getScore() );
        Utility.drawCenteredString( g, app.getScreenWidth(),
                app.getScreenHeight() / 3, "GAME OVER" );
    }
}
```

## THE ENTERHIGHSCORENAME STATE

The EnterHighScoreName state, as shown in Figure 17.8, presents a list of characters, just like the example in Chapter 11, “Text.” The enter() method adds all the available characters and measures each one to find the maximum width to space the letters.

![](img/588a4cda8f2acae94a7e1987bf99400d_618_0.png)

Figure 17.8
Enter High Score Name.
© 2014 Timothy Wright.

The processInput() method moves the selected character around with the arrow keys and sets the value with the spacebar.

The updateHeldKey() and resetHeldKey() methods keep track of the arrow keys if they are held down. Instead of just zipping the selected character as fast as possible, this slows it down to the STEP value, which is a tenth of a second. That way it doesn't scroll too fast.

The render() method draws the score, the entered name, and the character list, rendering the selected character as red with a box around it.

```java
package javagames.completegame.state;

import java.awt.*;
import java.awt.event.*;
import java.util.Vector;
import javagames.util.Matrix3x3f;

public class EnterHighScoreName extends AttractState {
    class GameLetter {
        public String letter;
        public int width;
        public GameLetter( String letter, int width ) {
            this.letter = letter;
            this.width = width;
        }
    }
    private static final long STEP = (long)0.10E9;
    private static final int FONT_SIZE = 32;
    private int maxWidth;
    private GameLetter[] letters;
    private int rowCount;
    private int colCount;
    private String name = "";
    private long heldDown = 0;
    private long last = 0;
    private int selectedRow = 0;
    private int selectedCol = 0;
    private GameState state;
    private boolean finished = false;
    public EnterHighScoreName( GameState state ) {
        this.state = state;
    }
    @Override
    public void enter() {
        super.enter();
        Font font = new Font( "Arial", Font.BOLD, FONT_SIZE );
        FontMetrics fm = app.getFontMetrics( font );
        Vector<GameLetter> temp = new Vector<GameLetter>();
        maxWidth = Integer.MIN_VALUE;
        maxWidth = addLetter( fm, " ", maxWidth, temp );
        maxWidth = addLetters( fm, (int)'A', (int)'Z', maxWidth, temp );
        maxWidth = addLetters( fm, (int)'a', (int)'z', maxWidth, temp );
        maxWidth = addLetters( fm, (int)'0', (int)'9', maxWidth, temp );
        maxWidth = addLetter( fm, "!", maxWidth, temp );
        maxWidth = addLetter( fm, "'", maxWidth, temp );
        maxWidth = addLetter( fm, "-", maxWidth, temp );
        maxWidth = addLetter( fm, "?", maxWidth, temp );
        maxWidth = addLetter( fm, "**", maxWidth, temp );
        maxWidth = addLetter( fm, "*", maxWidth, temp );
        maxWidth = addLetter( fm, "del", maxWidth, temp );
        maxWidth = addLetter( fm, "end", maxWidth, temp );
        letters = temp.toArray( new GameLetter[ 0 ] );

        colCount = 10;
        rowCount = letters.length / colCount;
    }

    private int addLetters( FontMetrics fm, int start, int end, int maxWidth,
        Vector<GameLetter> letters ) {
        for ( int i = start; i <= end; ++i ) {
            maxWidth = addLetter( fm, "" + (char)i, maxWidth, letters );
        }
        return maxWidth;
    }

    private int addLetter( FontMetrics fm, String letter, int max,
        Vector<GameLetter> letters ) {
        int strWidth = fm.stringWidth( letter );
        max = Math.max( max, strWidth );
        letters.add( new GameLetter( letter, strWidth ) );
        return max;
    }

    @Override
    public void processInput( float delta ) {
        if ( keys.keyDownOnce( KeyEvent.VK_LEFT ) ) {
            selectedCol = roll( selectedCol - 1, 0, colCount - 1 );
            resetHeldKey();
        }

        if ( keys.keyDown( KeyEvent.VK_LEFT ) && updateHeldKey() ) {
            selectedCol = roll( selectedCol - 1, 0, colCount - 1 );
        }

        if ( keys.keyDownOnce( KeyEvent.VK_RIGHT ) ) {
            selectedCol = roll( selectedCol + 1, 0, colCount - 1 );
            resetHeldKey();
        }

        if ( keys.keyDown( KeyEvent.VK_RIGHT ) && updateHeldKey() ) {
            selectedCol = roll( selectedCol + 1, 0, colCount - 1 );
        }

        if ( keys.keyDownOnce( KeyEvent.VK_UP ) ) {
            selectedRow = roll( selectedRow - 1, 0, rowCount - 1 );
            resetHeldKey();
        }

        if ( keys.keyDown( KeyEvent.VK_UP ) && updateHeldKey() ) {
            selectedRow = roll( selectedRow - 1, 0, rowCount - 1 );
        }

        if ( keys.keyDownOnce( KeyEvent.VK_DOWN ) ) {
            selectedRow = roll( selectedRow + 1, 0, rowCount - 1 );
            resetHeldKey();
        }

        if ( keys.keyDown( KeyEvent.VK_DOWN ) && updateHeldKey() ) {
            selectedRow = roll( selectedRow + 1, 0, rowCount - 1 );
        }

        if ( keys.keyDownOnce( KeyEvent.VK_SPACE ) ) {
            int selected = getSelectedIndex( selectedRow, selectedCol );
            updateHighScoreRecord( letters[ selected ].letter );
        }
    }

    private void resetHeldKey() {
        last = System.nanoTime();
        heldDown = -STEP;
    }

    private boolean updateHeldKey() {
        long current = System.nanoTime();
        heldDown += current - last;
        last = current;
        if ( heldDown > STEP ) {
            heldDown -= STEP;
            return true;
        }
        return false;
    }

    @Override
    public void render( Graphics2D g, Matrix3x3f view ) {
        super.render( g, view );
        g.setColor( Color.GREEN );
        g.setRenderingHint( RenderingHints.KEY_TEXT_ANTIALIASING,
            RenderingHints.VALUE_TEXT_ANTIALIAS_ON );
        Font font = new Font( "Arial", Font.BOLD, FONT_SIZE );
        g.setFont( font );
        FontMetrics fm = g.getFontMetrics();
        int sh = fm.getAscent() + fm.getDescent() + fm.getLeading();
        // draw the score
        String score = "Score: " + highScoreMgr.format( state.getScore() );
        int scoreX =
            ( ( app.getScreenWidth() - fm.stringWidth( score ) ) / 2 );
    }
}
```
