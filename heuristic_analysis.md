# Heuristic Analysis

## Raw Metrics
| Algo          | problem | expansions | goal tests | time  | plan size |
| ----          | ------- | ---------- | ---------- | ----- | --------- |
| rec-Best      | 1       | 4229       | 423        | 2.90  | 6         |
| greedy-best   | 1       | 7          | 9          | 0.005 | 6         |
| a*-h1         | 1       | 55         | 57         | 0.041 | 6         |
| a*-ignore-pre | 1       | 41         | 43         | 0.107 | 6         |
| a*-levelsum   | 1       | 11         | 13         | 0.610 | 6         |
| rec-Best      | 2       | n/a        | n/a        |  n/a  | n/a       |
| greedy-best   | 2       | 998        | 1000       | 2.65  | 21        |
| a*-h1         | 2       | 4853       | 4855       | 14.32 | 9         |
| a*-ignore-pre | 2       | 1450       | 145        | 85.95 | 9         |
| a*-levelsum   | 2       | 86         | 88         | 58.94 | 9         |
| rec-Best      | 3       | n/a        | n/a        |  n/a  | n/a       |
| greedy-best   | 3       | 5578       | 5580       | 18.0  | 22        |
| a*-h1         | 3       | 18223      | 18225      | 59.6  | 12        |
| a*-ignore-pre | 3       | 5040       | 5042       | 640.3 | 12        |
| a*-levelsum   | 3       | 325        | 327        | 307.8 | 12        |

## Optimality Analysis

#### Recursive Best First Search

Produced an optimal plan, though searched a lot to find it.  For p2 and p3
it never even finished, I eventually aborted.

#### Greedy Best First Search

Found optimal plan for P1 almost immediately.  Since it's also using the h_1
heuristic (not a real heuristic) I think it's mostly coincidental that there
was an easy to find solution early in the search space.  P1 is fairly small.

For P2, it produced a distinctly unoptimal plan (exactly as expected since the
  heuristic is returning the same value for any node, it has no way to determine
  best-ness of a state).

#### A* (constant heuristic)

h1 as a heuristic means that all nodes score the same, but for P1 it
found an optimal plan pretty quick.  P2 it also found an optimal path (9 steps),
but had to expand a lot of nodes to find it (no good way to prioritize with a constant
  heuristic).  P3, same result, optimal plan but very broad search.

A good algorithm doesn't work well with a crummy heuristic, but on problems
this simple it performs pretty quick :).


#### A* (ignore_preconditions)

This is the first search with a real heuristic.  On problem 1 it produced an equally
optimal plan to the constant heuristic in 80% of the expansion space, though
it took longer in clock time (as it requires computation time to calculate
  the heuristic value).

For problem 2 it found the same length plan as h1, but only expanded 1450 nodes
(much better search space).  It seems the tradeoff here is for a very high branching
factor, the expensive heuristics will be worth it.  For problems with only a few
possible paths, the simpler but faster to calculate heuristics would ultimately be better.

#### A* (level sum)

Took even longer in clock time than ignore_preconditions, so the heuristic
is more expensive to calculate, but it trimmed the search space immensely
(for p1 it only expanded 11 nodes, preconditions ignoring expanded 41).

For problem 2 it also found an optimal solution (as expected) and took a
while to calculate it (58 seconds), but it only expanded 86 nodes. In fact,
even though the level sum is a more expensive heuristic to calculate, because
it is able to search so much more optimally it still ran in less wall clock time
than the ignore-preconditions heuristic on the same problem.

Problem 3 demonstrated the same difference, much lower search space and significantly
less clock time.
