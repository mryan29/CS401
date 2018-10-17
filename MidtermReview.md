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


