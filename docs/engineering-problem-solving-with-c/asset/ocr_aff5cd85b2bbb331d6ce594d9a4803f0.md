determine the payoff of each move. This function will be used in Steps 5 and 6. Step 7 reports the final scores. This will also be done in a function. We will now develop the refinement in pseudocode:

# Refinement in Pseudocode:

```
main():
    setup(player*, player*)
    play_game(player1*, player2*)
    report(player1*, player2*)
end main

play_game(player* player1, player* player2):
    input number of iterations.
    p1move = player1->play()
    p2move = player2->play()
    player1->accumulate(payoff(p1move, p2move))
    player2->accumulate(payoff(p2move, p1move))
    for(count =1, count < iterations, count++)
        p1save = p1move
        p1move = player1->play(p2move)
        p2move = player2->play(p1save)
        player1->accumulate(payoff(p1move, p2move))
        player2->accumulate(payoff(p2move, p1move))
    end play_game

payoff(p1move, p2move):
    if(p1move)
        if(p2move)
            return 3
        else
            return 0
    else
        if(p2move)
            return 5
        else
            return 1
    end payoff

report(player* player1, player* player2):
    if(player1->score > player2->score)
        output player 1 wins
    else if(player1->score < player2->score)
        output player 2 wins
    else
        output tie
    end report
```

Our main function calls three functions to implement the game. Each function has formal parameters of type player*. Since the Player class uses the keyword virtual in its class declaration, the dynamic objects referenced by the formal parameters will call the