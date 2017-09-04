# Heuristic Analysis

## Raw Metrics
| Algo          | problem | expansions | goal tests | time  | plan size |
| ----          | ------- | ---------- | ---------- | ----- | --------- |
| rec-Best      | 1       | 4229       | 423        | 2.90  | 6         |
| greedy-best   | 1       | 7          | 9          | 0.005 | 6         |
| a*-h1         | 1       | 55         | 57         | 0.041 | 6         |
| a*-ignore-pre | 1       | 55         | 57         | 0.041 | 6         |

## Optimality Analysis

#### Recursive Best First Search

Produced an optimal plan, though searched a lot to find it.  

#### Greedy Best First Search

Found optimal plan for P1 almost immediately.  Since it's also using the h_1
heuristic (not a real heuristic) I think it's mostly coincidental that there
was an easy to find solution early in the search space.  P1 is fairly small.

#### A* (constant heuristic)

h1 as a heuristic means that all nodes score the same, but for P1 it
found an optimal plan pretty quick.

#### A* (ignore_preconditions)

First search with a real heuristic.  On problem 1 it produced an equally
optimal plan to the constant heuristic in 80% of the expansion space, though
it took longer in clock time (as it requires computation time to calculate
  the heuristic value).

#### A* (level sum)

Took even longer in clock time than ignore_preconditions, so the heuristic
is more expensive to calculate, but it trimmed the search space immensely
(for p1 it only expanded 11 nodes, preconditions ignoring expanded 41).
