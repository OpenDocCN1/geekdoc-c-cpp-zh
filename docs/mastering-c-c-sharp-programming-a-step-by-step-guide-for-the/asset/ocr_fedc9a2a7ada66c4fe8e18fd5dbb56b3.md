|  |  |  |
|---|---|---|
| Min | Not applicable for either ordered or unordered sequences |  |
| OrderBy | Sequence is reordered | New ordered section |
| OrderByDescending | Sequence is reordered | New ordered section |
| Range sequences* | Not applicable for either ordered or unordered |  |
| Repeat sequences* | Not applicable for either ordered or unordered |  |
| Reverse | Reverses | Doesn't do anything |
| Select | Ordered Results | Unordered Results |
| Select (Indexed) | Ordered Results | Unordered Results |
| SelectMany | Ordered Results | Unordered Results |
| SelectMany(Index) | Ordered Results | Unordered Results |
| SequenceEqual | Ordered Comparison | Unordered Comparison |
| Single sequences | Not applicable for either ordered or unordered |  |
| SingleOrDefault | Not applicable for either ordered or unordered sequences |  |
| Skip | Skips the first n elements | Skips any n elements |
| SkipWhile | Ordered Results | Nondeterministic |

Performs on a current arbitrary order

Nondeterministic where the operation is noncommutative or nonassociative for both ordered and unordered sequences