# Sep6 - Graphs

# Undirected graphs G=(V,E)
**Notaion**: G=(V,E)
- V = nodes (vertices)
- E = edges btwn pairs of nodes
- captures pairwise relationship btwn objects
- graph size parameters: n = |V|, m = |E|
- no self loop or multi-edges
- geometric property is mathematically irrelevant, only convenient

## Terms
- **path**: sequence of vertices st each vertexis connected to the next vertex w an edge
- **cycle**: path of a length >2 that has same start and end
- **tree**: connected graph with no cycls
- **degree of a vertex**: number of edges that touch the vertex
- **connected**: graph is connected if there is a path between every two vertices
- **connected component**: *maximal* set of connected vertices

## Properties
### Degree Sum
**Claim**: in any undirected graph, the number of edges is equal to (1/2) Summation vertex v of deg(v)

**Pf**: Summation vertex v of deg(v) counts every edge of the graph exactly twice, from each end of the edge

### Odd Degree Vertices
**Claim**: In any undirected graph, the number of odd degree vertices is even

**Pf**: In previous claim, we showed sum of all vertex degrees is even. So, there must be even number of odd degree vertices, ecause sum of odd number of odd numbers is odd.

### Number of edges
Let G=(V,E) be a graph w/ n = |V| vertices and m = |E| edges.

**Claim**: 0 <= m <= (n over 2) = (n(n-1))/2 = O(n^2)

**Pf**: Since every edgeconnects 2 distinct vertices and no two edges connect the same pair of vertices, it has at most (n over 2) edges.

### Degree 1 vertices
**Claim**: If G has no cycle, then vertex degree <= 1 (Every tree has a leaf)

**Pf**: (by contradiction)
- Suppose every vertex has degree >=2.
- Start from vertex v1 and follow path v1, ...,vi . When at vi, we choose next vertex to be diff from vi-1. We can do so bc deg(vi)>=2.
- First time we see a repeated vertex, we get a cycle.
- We always get a repeated vertex bc G hsa finitely many vertices.

### Trees and Induction
**Claim**: Every tree w n vertices has n-1 edges.

**Pf**: (by induction)
- Base case: n = 1, the tree has no edge
- Inductive Step: Let T be a tree with n vertices.
- So, T has a vertex v of degree 1.
- Remove v and the neighboring edge, and let T' be the new graph.
- We claim T' is a tree: it has no cycle, and it must be connected.
- So, T' has n-2 edges and T has n-1 edges.

## Algorithms
### Graph Traversal
Walk (via edges) from a fixed starting vertex s to all vertices reachable from s.
- Breadth first search (BFS): Order nodes in successive layers based on distance from s
- Depth first search (DFS): More natural approach for exploring a maze

#### BFS
Completely explore the vertices in order of their distance from s.

Three states of vertices:
- undiscovered
- discovered
- fully-explored

Naturally implemented using queue which will always have list of Discovered vertices.

##### BFS Algorithm
**Initialization**: mark all vertices undiscovered

```
BFS(s)
  mark s **discovered**
  queue = {s}
  while queue not empty
    u = remove_first(queue)
    for each edge {u,x}
      if (x is undiscovered)
        mark x **discovered**
        append x on queue
    mark u **fully-explored**
```

Using a queue &rarr; FIFO.

##### Properties of BFS
- BFS(s) visits a vertex v iff there is a path from s to v
- edges into then-undiscovered vertices define a tree - the "breadth first spanning tree" of G
- level i in the tree are exactly all vertices v st the shortest path (in G) from the root s to v is of length i

- **Claim**: all nontree edges join vertices on same or adjacent levels of the tree
- **Lemma*: all vertices at level i of BFS(s) have shortest path distance i to s
  - claim: if L(v) = i, then shortest path <= i
  - claim: if shortest path = i, then L(v) <= i


## Graph representation
**Adjacency matrix**: n-by-n matrix with A<sub>uv</sub> = 1 if (u,v) is an edge.
- Space proportional to **n<sup>2<sup>**
- Checking if (u,v) is an edge takes **&theta; (1)** time
- Identifying all edges takes **&theta; (n<sup>2</sup>)** time

_BFS Analysis_

`while queue not empty` O(n) times: at most once per vertex

`for each edge {u,x}` O(n) times: check eevry vertex x

Overall: O(n<sup>2</sup>) time

**Adjacency List**: Node indexed array of lists
- Space proportional to **m+n**
- Checking if (u,v) is an edge takes **O(deg(u))** time
- Identifying all edges take **&theta;(m+n)** time

_BFS Analysis_

`while queue not empty` O(n) times: at most once per vertex

`for each edge {u,x}` O(deg(u)) times: at most twice per edge

Overall: O(n+m) time

## Why Trees?
Trees are simpler than graphs and many statements can be proved on trees by induction.

To solve graph problems:
- find nice tree in graph i.e. one such that nontree edges have some simplifying structure
- solve problem on the tree
- use solution on tree to find good solution on graph


## BFS Application: connected component
Given vertices u,v, is there a path from u to v in G?

&nbsp; Idea: Create array A st for all u in same connected component, A[u] is same

...




















