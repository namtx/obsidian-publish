[Wikipedia-Strongly connected components](https://en.wikipedia.org/wiki/Tarjan%27s_strongly_connected_components_algorithm)

##### Basic idea
1. DFS begins from an arbitrary start node
2. the collection of search tree is a [[spanning forest]] of the graph
3. The first node discovered by DFS is the root of [[Strongly connected components]]

##### Stack invariant
- Nodes are placed on [[stack]] in the order which they are visited
- when the DFS search recursively visits a node `v` and its desedants, those nodes are not neccessarily popped from the stack when recursive call returns.
- the node remains on the stack after it has been visited if and only if there exists a path in the input graph from it to some node earlier on the stack.
- In other words, it means that in the #dfs a node would be only removed from the stack after all its connected paths has been traversed.
- when the #dfs will backtrack it would remove the node on a single path and return to the root in order to start a new path.
- At the end of the call that visits `v` and its descendants, we know whether `v` itself has a path to any node ealier on the stack. If so, the call returns, leaving `v` on the stack to resever the invariant. If not, then `v`  must be the root of its [[Strongly connected components]], which consists of `v` together with any nodes later on stack than `v`.
- the connected component root at `v` is then popped from the stack and returned, again preserving the invariant.

##### Bookeeping
- Each node `v` is assigned a unique integer `v.index`, which numbers the nodes consecutively in the order in which they are discovered.
- It also maintains a value `v.lowlink` that presents the smallest indx of any node on the stack know to be reachable from `v` through `v`'s #dfs subtree, including `v` itself.
- therefore `v` must be left the stack if `v.lowlink < v.index`, whereares `v` must be removed as the root of [[Strongly connected components]] if `v.lowlink == v.index`.
- The value `v.lowlink` is computed during the #dfs from `v`, as this finds the node are reachable from `v`.

<iframe width="560" height="315" src="https://www.youtube.com/embed/wUgWX0nc4NY?start=458" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>