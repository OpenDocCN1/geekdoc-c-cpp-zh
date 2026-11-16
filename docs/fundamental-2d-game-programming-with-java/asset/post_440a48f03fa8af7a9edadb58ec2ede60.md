
public void drawScore( Graphics2D g, int score ) {
    g.setRenderingHint(
        RenderingHints.KEY_TEXT_ANTIALIASING,
        RenderingHints.VALUE_TEXT_ANTIALIAS_ON
    );
    String toShow = "" + score;
    while( toShow.length() < 6 ) {
        toShow = "0" + toShow;
    }
    g.setFont( new Font( "Arial", Font.BOLD, 20 ) );
    g.setColor( Color.GREEN );
    Utility.drawCenteredString( g, app.getScreenWidth(), 0, toShow );
}

public void drawLives( Graphics2D g, Matrix3x3f view, int lives ) {
    float w = ship.getWidth();
    float h = ship.getHeight();
    float x = -0.95f + w;
    float y = 1.0f - h / 2.0f;
    for( int i = 0; i < lives; ++i ) {
        x += w * i;
        ship.setAngle( (float)Math.toRadians( 90 ) );
        ship.setPosition( new Vector2f( x, y ) );
        ship.update( 0.0f );
        ship.draw( g, view );
    }
}

## THE GAMESTATE CLASS

The GameState class will keep track of the current level, the number of remaining lives, and the current score while the game is running. This state object is passed around the different state objects while the game is playing, but not while the attract screens are looping.

```
package javagames.completegame.state;

import javagames.completegame.object.Asteroid.Size;

public class GameState {
    private int level;
    private int lives;
    private int score;

    public void setLevel( int level ) {
        this.level = level;
    }

    public int getLevel() {
        return level;
    }

    public void setLives( int lives ) {
        this.lives = lives;
    }

    public int getLives() {
        return lives;
    }

    public int getScore() {
        return score;
    }

    public void updateScore( Size size ) {
        switch( size ) {
        case Small: score += 500; break;
        case Medium: score += 300; break;
        case Large: score += 100; break;
        }
    }
}
```

## THE SCORE CLASS

The Score class is a simple Comparable<> object used to sort the score objects stored in the high-score file.

```
package javagames.completegame.state;
public class Score implements Comparable<Score> {
    public String name = "";
    public int score = 0;
    public Score( String name, int score ) {
        this.name = name;
        this.score = score;
    }
    public int compareTo( Score o ) {
        if( score == o.score )
            return 0;
        if( score < o.score )
            return -1;
        return 1;
    }
}
```

## THE QUICKLOOPER CLASS

The QuickLooper class is an updated sound loop event that can be opened and closed only once, instead of every time the sound is played. This reduces the latency for the sound event. Also, there is an addition to the processEvent() method that keeps taking events off of the queue. This prevents loop events from getting backed up when the sound is used for multiple start and stop events from rapid keypresses. Because there is a 50ms buffer, there can be a delay from starting and stopping the sound in quick succession.

```
package javagames.completegame.admin;

import javagames.sound.AudioStream;
import javagames.sound.SoundEvent;

public class QuickLooper extends SoundEvent {
    public static final String STATE_CLOSED = "closed";
    public static final String STATE_WAITING = "waiting";
    public static final String STATE_RUNNING = "running";

    public static final String EVENT_FIRE = "fire";
    public static final String EVENT_DONE = "done";
    public static final String EVENT_OPEN = "open";
    public static final String EVENT_CLOSE = "close";

    private String currentState;

    public QuickLooper( AudioStream audio ) {
        super( audio );
        currentState = STATE_CLOSED;
    }

    public void open() {
        put( EVENT_OPEN );
    }

    public void close() {
        put( EVENT_CLOSE );
    }

    public void fire() {
        put( EVENT_FIRE );
    }

    public void done() {
        put( EVENT_DONE );
    }

    protected void processEvent( String event ) throws InterruptedException {
        while( queue.peek() == EVENT_DONE || queue.peek() == EVENT_FIRE ) {
            event = queue.take();
        }

        if( currentState == STATE_CLOSED ) {
            if( event == EVENT_OPEN ) {
                audio.open();
                currentState = STATE_WAITING;
            }
        } else if( currentState == STATE_WAITING ) {
            if( event == EVENT_CLOSE ) {
                audio.close();
                currentState = STATE_CLOSED;
            }

            if( event == EVENT_FIRE ) {
                audio.loop( AudioStream.LOOP_CONTINUOUSLY );
                currentState = STATE_RUNNING;
            }
        } else if( currentState == STATE_RUNNING ) {
            if( event == EVENT_CLOSE ) {
                audio.stop();
                audio.close();
                currentState = STATE_CLOSED;
            }

            if( event == EVENT_DONE ) {
                audio.stop();
                currentState = STATE_WAITING;
            }
        }
    }
}
```

## THE QUICKRESTART CLASS

The QuickRestart class is similar to the last sound event update, allowing the sound to be opened and closed only once, instead of every time the sound is played. This class does not need the extra while loop to pull out events because the sound is restarted, which doesn't cause any queue issues.

```
package javagames.completegame.admin;

import javagames.sound.AudioStream;
import javagames.sound.SoundEvent;

public class QuickRestart extends SoundEvent {
    public static final String STATE_CLOSED = "closed";
    public static final String STATE_WAITING = "waiting";
    public static final String STATE_RUNNING = "running";

    public static final String EVENT_FIRE = "fire";
    public static final String EVENT_DONE = "done";
    public static final String EVENT_OPEN = "open";
    public static final String EVENT_CLOSE = "close";

    private String currentState;

    public QuickRestart( AudioStream stream ) {
        super( stream );
        currentState = STATE_CLOSED;
    }

    public void open() {
        put( EVENT_OPEN );
    }

    public void close() {
        put( EVENT_CLOSE );
    }

    public void fire() {
        put( EVENT_FIRE );
    }

    protected void processEvent( String event ) throws InterruptedException {
        System.out.println( "Quick Restart Got: " + event );
        System.out.println( "Current State: " + currentState );
        if( currentState == STATE_CLOSED ) {
            if( event == EVENT_OPEN ) {
                audio.open();
                currentState = STATE_WAITING;
            }
        } else if ( currentState == STATE_WAITING ) {
            if( event == EVENT_CLOSE ) {
                audio.close();
                currentState = STATE_CLOSED;
            }
            if( event == EVENT_FIRE ) {
                audio.start();
                currentState = STATE_RUNNING;
            }
        } else if ( currentState == STATE_RUNNING ) {
            if( event == EVENT_FIRE ) {
                audio.restart();
            }
            if( event == EVENT_CLOSE ) {
                audio.stop();
                audio.close();
                currentState = STATE_CLOSED;
            }
            if( event == EVENT_DONE ) {
                currentState = STATE_WAITING;
            }
        }
        System.out.println( "New State: " + currentState );
    }

    @Override
    protected void onAudioFinished() {
        put( EVENT_DONE );
    }
}
```

## THE HIGHSCOREMGR CLASS

HighScoreMgr is responsible for saving and loading the top ten high scores in a data file. If the file is not found when the game is started, then a default file is written. The file, spacerocks.dat has the following format:

```
<hs>
<player name="Dad" score="220600"/>
<player name=" score="51700"/>
<player name="BOB3ar" score="50000"/>
<player name="U" score="45000"/>
<player name="Lilly" score="42900"/>
<player name="Awe" score="33240"/>
<player name="Woowo" score="31000"/>
<player name="Loopy" score="27600"/>
<player name="Coco" score="26700"/>
<player name="AAA" score="14200"/>
</hs>
```

This file is saved in the user's home directory. This also uses the Score class presented previously to sort the scores from highest to lowest.

```
package javagames.completegame.admin;

import java.io.*;
import java.text.*;
import java.util.*;

import javagames.completegame.state.GameState;
import javagames.completegame.state.Score;
import javagames.util.XMLUtility;

import javax.swing.JOptionPane;
import org.w3c.dom.*;

public class HighScoreMgr {
	private static final String HIGH_SCORE_FILE_NAME = "spacerocks.dat";
	private static final String[] DEFAULT_SCORES = {
		{"B03ar", "50000"},
		{"Lilly", "42900"},
		{"Tiger", "40000"},
		{"Coco", "36000"},
		{"Loopy", "30100"},
		{"Woowoo", "27800"},
		{"Orange Foot", "23400"},
		{"Groovy", "18300"},
		{"Guitar God", "11100"},
		{"Daddy", "7800"}
	};

	private Vector<Score> scores = new Vector<Score>();
	private NumberFormat format = null;

	public HighScoreMgr() {
		format = new DecimalFormat();
		format.setMaximumFractionDigits( 0 );
		format.setMinimumFractionDigits( 0 );
		format.setGroupingUsed( true );
		format.setParseIntegerOnly( true );
	}
}
```
