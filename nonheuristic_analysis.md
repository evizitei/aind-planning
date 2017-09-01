# Heuristic Analysis

## Raw Metrics
| Algo       | problem | expansions | goal tests | time  |
| ----       | ------- | ---------- | ---------- | ----- |
| BFS        | 1       | 43         | 56         | 0.03  |
| BF-Tree    | 1       | 1458       | 1459       | 1.24  |
| DF-Graph   | 1       | 21         | 22         | 0.02  |
| DF-Limited | 1       | 101        | 271        | 0.02  |
| UCS        | 1       | 55         | 57         | 0.04  |
| BFS        | 2       | 3343       | 4609       | 18.16 |
| BF-Tree    | 2       |        |        |   |
| BFS        | 3       | 14663      | 18098      | 138.1 |

## Optimality Analysis

#### Breadth-first search

BFS does produce an optimal plan, though it can evaluate many irrelevant plans to arrive there.  This is
absolutely expected because BFS looks through *every* plan
of a given number of steps before broadening.  Producing
the optimal path comes at the expense of an exponentially
large search space as the input grows.

#### Breadth-first tree search

In this case, BFS tree search is strictly worse than BFS.
The problem is that BFS maintains an explored set and
doesn't bother evaluating states it has already arrived at
before.  BFS-tree does not care if a state has been seen before,
so although it does arrive at the same optimal plan (
 optimal number of steps ) it evaluates *all plans of less than
 that number of steps, even those with many repeated pointless
 steps*.

#### Depth-limited search

Produces an incredibly inefficient plan.  This is expected
because it has a high cutoff (50) and it allows repeated states.
Therefore the first goal state it arrives at which is less than
50 steps it will consider successful, and it will explore the
'deepest' part of that space first. Given how many repeated
states are possible in this state space, it's perfectly likely
that you'll end up with a plan that is very close to the length
of the cutoff, even if there are much shorter plans avaialable
(a great example is problem 1 where a 6 step plan is available,
  and depth-limited search manages to produce a 50-step plan).

#### Uniform Cost Search

Since our 'cost' in this case is 1 per action, uniform cost should naturally
be more expensive than breadth first search to produce the same result
(since it spends time calculating the 'cost' which is equivalent to the number
of steps, and therefore the same as just using a FIFO queue in order but probably
wastes time trying to maintain a priority queue).
