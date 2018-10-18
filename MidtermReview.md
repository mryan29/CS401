# Ch1: Intro
## 1.1 Stable Matching
Given set of preferences among applicants and employers, asssign applicants to employers s.t. for every employer E and every applicant A who is not scheduled to work for E, at lease one of the following things is true:
1. E prefers every one of its accepted applicants to A
2. A prefers their current situation over any other matches

If so, the outcome is **stable**

Gale-Shapley Algorithm:
1. Initially, everyone is unmatched. Proposer chooses applicant who ranks highest on preferences and proposes to her.
2. Next man chooses their highest ranking woman to whom he has not yet proposed, and proposes to her. If she is also free, they become engaged. If not, she determines which of the two men rank higher on her preference list and those two become engaged while the other becomes free.
3. Continue untill no one is free.

```
Initially all m E M and w E W are free
While there is a man m who is free and hasn’t proposed to every woman
  Choose such a man m
  Let w be the highest-ranked woman in m’s preference list to whom m has not yet proposed 
  If ~ is free then
    (m, w) become engaged
  Else 
    w is currently engaged to m’
    If w prefers m’ to m then 
      m remains free
    Else w prefers m to m’ 
      (m,w) become engaged 
      m' becomes free
    Endif 
  Endif
Endwhile
Return the set S of engaged pairs
```

Observations:
1. w remains engaged from pt at which she receives first propsal, and sequence of partners to which she is engaged gets better and better (in terms of her preference list)
2. Sequence of women to whom m proposes gets worse and worse (in terms of his preference list)
3. G-S algorithm terminates after at most n<super>2</super> iterations of the While loop
4. If m is free at some pt in the algorithm, then there is a woman to whome he has not yet proposed.
5. The set S returned at termination is a perfect matching.

## 1.2
Representative problems:
1. Interval Scheduling
  a. n requests with each request i specifying start time s<sub>i</sub> and finish time f<sub>i</sub>
  b. s<sub>i</sub> < f<sub>i</sub>
  c. Two requests i and j are compatible if the requested intervals don't overlap
  d. Solved by greedy algorithms
  e. want to maximize # of requests accomodated simultaneously
2. Weighted Interval Scheduling
  a. each request has associated weight/value
  b. want to find compatible subset of intervals of maximum total value
  c. use dynamic programming
3. bipartite matching
...


# 2. Algorithm Analysis
## Big O - asymptotically upper bound
f(N) is O(g(N)) iff there is a constant c>0 and N0 >= 0 s.t., eventually always

0 <= f(N) <= c⋅g(N) for all N >= N0

### Properties
Reflexivity. f is O(f).

Constants. If f is O(g) and c > 0, then c⋅f is O(g).

Products. If f1 is O(g1) and f2 is O(g2), then f1⋅f2 is O(g1⋅g2).

Sums. If f1 is O(g1) and f2 is O(g2), then f1 + f2 is O(max {g1, g2}).

Transitivity. If f is O(g) and g is O(h), then f is O(h)

### Common 
• Polynomials:

a<sub>0</sub> + a<sub>1</sub>n + ⋯ + a<sub>d</sub>n<sup>d</sup> is O(n<sup>d</sup>)

• Logarithms:

log<sub>a</sub>n = O(log<sub>b</sub>n) for all constants a, b > 0

• Logarithms: log grows slower than every polynomial

For all k > 0, log n = O(n<sup>k</sup>)

• n log n = O(n<sup>1.01</sup>)

## &Omega; - asymptotically lower bound
f(N) is &Omega;(g(N)) iff there is a constant c>0 and N0 >= 0 s.t., for infinitely

0 <= c⋅g(N) <= f(N) for all N >= N0

## &Theta; - asymptotically tight bound
f(N) is &Theta;(g(N)) iff there are c0>0, c1>0 and N0 >= 0 s.t., eventually always

c0⋅g(N) <= f(N) <= c1⋅g(N) for all N >= N0

### Proof
Let f and g be two functions that:

&nbsp;&nbsp;&nbsp;&nbsp;lim n&rarr;∞ &nbsp;&nbsp;f(n)/g(n)

exists and is equal to some number c > 0. Then f(n) = &Theta;(g(n))

## Properties
1. If f = O(g) and g = O(h), then f = O(h).
2. If f = &Omega;(g) and g = &Omega;(h), then f = &Omega;(h).
3. If f = &Theta;(g) and g = &Theta;(h), then f = &Theta;(h).
4. If f = O(h) and g = O(h), then f+g = O(h).
5. If g = O(f), then f + g = &Theta;(f).


## Common Run Times
### Linear O(n)
1. Computing maximum
2. Merging two sorted lists

### O(n log n) Time
1. Mergesort
2. Determining largest gaps of an unsorted list of times

### Quadratic
1. Nested loops
2. Finding closest pair of points in list of (x,y) coordinates using brute force

### Cubic
1. Nested Loops

# 3. Graphs
## Basic Overview



## BFS


## DFS
explores G by going as deeply as possible and only retreating when necessary

## Representing graphs



# 4. Greedy Algorithms
## Interval Scheduling
Possible rules for selecting which to schedule:
1. which starts the earliest s(i)
2. which requires the smallest interval of time f(i) - s(i)
3. which has the fewest number of noncompatible requests/conflicts
4. which finishes first f(i) --> optimal

To prove:
- |A| = |O| aka show A contains the same number of intervals as O and is therefore the optimal solution
- for each r>=1, the r<sup>th</sup> accepted request in A's schedule finishes no later than the r<sup>th</sup> request in the optimal schedule
- proof by induction:
  - r=1 clearly true bc we pick request i w/ minimum finish time
  - let r>1, for all r<= k, we have f(i<sub>r</sub>) <= f(j<sub>r</sub>)
  - induction hypothesis: the statement is true for r-1 and we will try to prove it for r
> study this more

## Interval Partitioning
goal: schedule all requests using as few resources as possible
i.e. schedule all courses using as few classrooms as possible
- number of required resources >= depth of the set of intervals

## Minimize Lateness
- resource available to begin at time s with deadline d<sub>i</sub>, requiring contiguous time interval of length t<sub>i</sub>, allowing certain requests run late
- algo must determine start/finish time for each interval
- late: request misses deadline f(i) > d<sub>i</sub>, where lateness is l<sub>i</sub> = f(i) - d<sub>i</sub> and l<sub>i</sub> = 0 if not late
- goal: schedule all requests, nonoverlapping, minimize maximum lateness L = max<sub>i</sub> l <sub>i</sub>, single machine

possible approaches:
1. schedule by increasing length
2. schedule by minimal slack time d<sub>i</sub> - t<sub>i</sub>
3. schedule by increasing order of deadlines d<sub>i</sub> --> optimal

## Optimal Caching
- issue: deciding which pieces of data to have close at hand (access quickly) of the large amount of data it takes a long time to access
- parameters:
  - set U of n pieces of data in main memor
  - cache can hold k < n pieces of data
  - cache initially holds some set of k items
  - sequence of data items D = d<sub>1</sub>,...,d<sub>m</sub> drawn from U is sequence of memory references to process
  - must decide at all times which k items to keep in the cache, which to evict jf already full (cache miss) - eviction schedule
- solution:
  - Farthest-in-Future Algorithm:
  ```
  When di needs to be brought into the cache,
    evict the item that is needed the farthest into the future
  ```
- terms:
  - reduced schedule: S<sub>bar</sub> brings in at most as many items as the schedule S
  - locality of reference: programs keep accessing things they have been accessing
  - optimal: incures no more misses than any other schedule

## 4.4 Shortest Paths in a Graph
problem: given nodes u and v, what is the shortest u-v path? or given start node s, shortest path from s to each other node?

parameters:
- given directed graph G = (V,E) w/ start node s (or undirected graph w/ two directed edges (u,v) and (v,u))
- assume s has a path to every other node in G
- each edge e has length l<sub>e</sub> >=0, and length of P denoted l(P)= sum of lengths of all edges in P

solution:
- Dijkstra's Algorithm (G,l)
  ```
  Let S be the set of explored nodes
    For each u∈S, we store a distsnce d(u) 
  Initially S = {s} and d(s) = 0
  While S != V
    Select a node v !∈ S with at least one edge from S for which
      d’(v) = min<sub>e=(u,v):u∈S</sub> d(u) + l<sub>e</sub> is as small as possible 
    Add v to S and define d(v)=d’(v)
  EndWhile
  ```
  
proof:
- show paths P<sub>u</sub> are shortest paths
- allow set S where for each u ∈ S, the path P<sub>u</sub> is a shortest s-u path
- induction
- base case: |S| = 1
- induction hypothesis: suppose the claim holds when |S| = k for some k>=1
- suppose S grows to size k+1 by adding node v, with (u,v) as our final edge on our s-v path P<sub>v</sub>
- by induction hypothesis, P<sub>u</sub> is shortest s-u path for each u ∈ S
> include more proof

run time: O(m log n)

## 4.5 Minimum Spanning Tree
Problem:
- given set of locations V = {v<sub>1</sub>1,...,v<sub>n</sub>}
- connect all nodes, minimize cost 
- cost c(v<sub>i</sub>,v<sub>j</sub>) = c<sub>e</sub> for each edge e = (v<sub>i</sub>,v<sub>j</sub>)

Parameters:
- assume G connected
- T = minimum cost solution, so (V,T) is a tree (minimum spanning tree)

Solution:
1. Kruskal's Algorithm
  a. start w/o any edegs
  b. successively insert edges from E in order of increasing cost, so long as e does not create a cycle when added
  c. if it would create a cycle, discard e and continue
2. Prim's Algorithm (Using Djikstra)
  a. start w/ root node s
  b. add node that can be attached as cheaply as possibly to partial tree
3. Backwards Kruskal's (Reverse-Delete Algorithm)
  a. start with full graph
  b. beginning w/ most expensive edge e, delete it as long as would not disconnect current graph
  
> Proof

# 5. Divide and Conquer
break input into parts, solve parts recursively, combine into overall solution

## 5.1 Mergesort

## 5.3 Counting Inversions
used in: rankings
- given: n numbers
- want a measure for how far the list is from being in ascending order
- solution: count number of inversions
- inversions: two indices i<j form an inversion if a<sub>i</sub> > a<sub>j</sub> aka if they're out of order

solution:
```
Merge-and-Count(A,B)

Maintain a Current pointer into each list, initialized to point to the front elements
Maintain a variable Count for the number of inversions, initialized to 0
While both lists are nonempty:
  Let ai and bj the elements pointed to by the Current pointer 
  Append the smaller of these two to the output list
  If b<sub>j</sub> is the smaller element then
    Increment Count by the number of elements remaining in A
  Endif
  Advance the Current pointer in the list from which the smaller element was selected. 
EndWhile
Once one list is empty, append the remainder of the other list to the output
Return Count and the merged list
```
run time: O(n)

Then extended to:
```
Sort-and-Count (L)

If the list has one element then
  there are no inversions 
Else
  Divide the list into two halves:
    A contains the first [rt/2] elements
    B contains the remaining [n/2J elements
  (rA, A) = Sort-and-Count (A) 
  (rB, B) = Sort-and-Count (B) 
  (r, L) = Merge-and-Count (A, B)
Endif
Return r=rA+rB+r, and the sorted list L
```
run time: O(n log n)


# Topics:
- analysis of run time
- graphs
- greedy algos
- divide and conquer

> Data Structures in Ch 2
> Actual algorithms
> Sort run times/complexities by worse/better
> What is (<sup>n</sup> <sub>2</sub>) where n is over 2
> study proofs by induction
> what is a minimum spanning tree


