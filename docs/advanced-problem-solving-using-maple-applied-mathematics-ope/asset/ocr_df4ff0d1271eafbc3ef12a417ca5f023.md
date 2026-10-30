It’s time for Maple.

```
> Labels := Vector[row]([Susan, Steve, Sarah, Tom, Claire, Fred, David, Claudia, Bob, Jenn]) :
Kite := Matrix([[0.1806, 0.2022, 0.1751, 0.1088], [0.1389, 0.1553, 0.1375, 0.1131], [0.1250, 0.1042, 0.1375, 0.1131], [0.1111, 0.0194, 0.1144, 0.1009], [0.1111, 0.0194, 0.1144, 0.1009], [0.0833, 0.0000, 0.0938, 0.0975], [0.0833, 0.0000, 0.0938, 0.0975], [0.0833, 0.3177, 0.1042, 0.1088], [0.0556, 0.1818, 0.0241, 0.0885], [0.0278, 0.0000, 0.0052, 0.0707]]) :
w := [0.47986, 0.26215, 0.155397, 0.102592) :
> Results := <Labels, f_normal(SAW(Kite, w), 3)>;
```

| Susan | Steve | Sarah | Tom | Claire | Fred | David | Claudia | Bob | Jenn |
| 0.901 | 0.722 | 0.643 | 0.504 | 0.504 | 0.393 | 0.393 | 0.675 | 0.399 | 0.143 |
| 1.0 | 0.801 | 0.714 | 0.560 | 0.560 | 0.436 | 0.436 | 0.749 | 0.443 | 0.158 |

The results are easier to parse when we sort the array. The program MatrixSort is in the PSMv2 package with syntax MatrixSort(Matrix, (row/col), <options>). The options are sortby=‘row’/‘column’ and order=‘ascending’/‘descending’ with defaults ‘row’ and ‘ascending’.

```
> MatrixSort(Results, 3, order = 'descending');
```

| Susan | Steve | Claudia | Sarah | Claire | Tom | Bob | David | Fred | Jenn |
| 0.901 | 0.722 | 0.675 | 0.643 | 0.504 | 0.504 | 0.399 | 0.393 | 0.393 | 0.143 |
| 1.0 | 0.801 | 0.749 | 0.714 | 0.560 | 0.560 | 0.443 | 0.436 | 0.436 | 0.158 |

We see the resulting rank order for "overall centrality" is
Susan > Steve > Claudia > Sarah > Claire > Bob > David > Fred > Jenn
Tom

# SENSITIVITY ANALYSIS.

We can apply sensitivity analysis to the weights to determine how changes impact the final rankings. We recommend using an algorithmic method to modify the weights. For example, if we reverse the weights for TC (total centrality) and BTW (betweenness), the rankings change to

| Susan | Claudia | Steve | Sarah | Bob | Claire | Tom | David | Fred | Jenn |
| 0.822 | 0.792 | 0.661 | 0.563 | 0.457 | 0.384 | 0.384 | 0.293 | 0.293 | 0.109 |
| 1.0 | 0.964 | 0.804 | 0.686 | 0.556 | 0.467 | 0.467 | 0.356 | 0.356 | 0.133 |

Susan is still the "top node," but Claudia and Steve have swapped for second; Bob is now above Claire, rather than tied.