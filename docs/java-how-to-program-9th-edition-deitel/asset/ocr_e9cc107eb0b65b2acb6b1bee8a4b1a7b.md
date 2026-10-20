```
// Fig. 31.18: BlackjackGameJFrame.java
// Blackjack game that uses the Blackjack Web Service.
package com.deitel.blackjackclient;

import com.deitel.blackjack.Blackjack;
import com.deitel.blackjack.BlackjackService;
import java.awt.Color;
import java.util.ArrayList;
import javax.swing.ImageIcon;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.xml.ws.BindingProvider;

public class BlackjackGameJFrame extends javax.swing.JFrame
{
    private String playerCards;
    private String dealerCards;
    private ArrayList<JLabel> cardboxes; // list of card image JLabels
    private int currentPlayerCard; // player's current card number
    private int currentDealerCard; // blackjackProxy's current card number
    private BlackjackService blackjackService; // used to obtain proxy
    private Blackjack blackjackProxy; // used to access the web service

    // enumeration of game states
    private enum GameStatus
    {
        PUSH, // game ends in a tie
        LOSE, // player loses
        WIN, // player wins
        BLACKJACK // player has blackjack
    } // end enum GameStatus

    // no-argument constructor
    public BlackjackGameJFrame()
    {
        initComponents();

        // due to a bug in NetBeans, we must change the JFrame's background
        // color here rather than in the designer
        getContentPane().setBackground( new Color( 0, 180, 0 ) );

        // initialize the blackjack proxy
        try
        {
            // create the objects for accessing the Blackjack web service
            blackjackService = new BlackjackService();
            blackjackProxy = blackjackService.getBlackjackPort();

            // enable session tracking
            ( (BindingProvider) blackjackProxy ).getRequestContext().put(
                BindingProvider.SESSION_MAINTAIN_PROPERTY, true );
        } // end try
```