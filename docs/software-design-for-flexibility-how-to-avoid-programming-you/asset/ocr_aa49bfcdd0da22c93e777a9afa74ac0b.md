The delegate procedure node-at gets the node at a given address. If this is a Black turn, it translates the address and applies the node view.

```
(define (node-at address)
(define (get-node address)
(list-ref list-ref nodes (address-x address)
    (address-y address)))
(if (white-move?)
  (get-node address)
  (graph-node-view (get-node (invert-address address))
    rotate-180-view)))
```

The inverse of node-at is the delegate procedure address-of. Each node has an edge, labeled with address, with its address as the value. As with node-at, if this is a Black move the returned address must be translated.

```
(define (address-of node)
(let ((address node 'edge-value 'address'))
  (if (white-move?)
    address
    (invert-address address))))
```

The delegate procedure next-turn advances the board after a move is made:

```
(define (next-turn) (loop (+ 1)))
```

Connecting the squares to their neighbors does address arithmetic to handle (literal) edge cases, creating a labeled edge between each square and each of its neighbors. It also creates the address edge for each node.

```
(define (connect-up-square address board)
(let ((node board 'node-at address))
  (node 'connect! address address))
  (for-each (lambda label x-delta y-delta)
    (let ((x (+ (address-x address) x-delta))
      (y (+ (address-y address) y-delta)))
      (if (and (<= x chess-board-last-index)
                (<= 0 y chess-board-last-index))
          (node 'connect! label
            (board 'node-at)))))
```