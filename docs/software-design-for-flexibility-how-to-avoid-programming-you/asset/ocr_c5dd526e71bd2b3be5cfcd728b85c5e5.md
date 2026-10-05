# 4.5.5 Chess moves

Now that we have a chessboard, populated with pieces, we need a way to move those pieces around. If a piece is in a particular square at a particular turn, the node representing that square has an edge, with the turn as its label, whose value is the piece. The following delegate procedures in make-chess-board-internal on page 218 are relevant here:

```
(define (piece-at address)
  (piece-in (node-at address)))

(define (node-in node)
  (and (has-edge? turn)
       (node 'edge-value turn)))

(define (set-piece-at address piece)
  ((node-at address) connect! (+ turn 1) piece))
```

We use piece-at to obtain a piece that we expect to move, given its address. Of course, it is always a good idea to check for obvious errors.

```
(define (get-piece-to-move board from)
  (let ((my-piece (board 'piece-at from))
    (if (not my-piece)
      (error "No piece in this square:" from)
      (if (not (eq? (board 'color) (piece-color my-piece))
          (error "Can move only one's own pieces:"
            my-piece))))
  my-piece)
```

To actually make a move we pick the piece and set it down in the target square. However, this move is allowed only if the target square is empty or if it is occupied by an opponent piece to be captured.

```
(define (simple-move board from to)
  (let ((my-piece (get-piece-to-move board from))
    (let ((captured (board 'piece-at to)))
      (if (not (no-piece-or-opponent?) captured my-piece)
        (error "Can't capture piece of same color:"
          captured))))

  ; The move looks good; make it so:
  (board 'set-piece-at my-piece))
```