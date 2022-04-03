### Algorithm
1.  Create a set mstSet that keeps track of vertices already included in #mst.
2. Assign a key value to all vertices in the input graph. Initialize all key values to `INFINITE`. Assign the key value as 0 for the first vertex so that it is picked first.
3. while `mstSet` doesn't include all vertices
	- Pick a vertex `u` which is not there in `mstSet` and has minumum key value
	- Include `u` to `mstSet`
	- Update key value of all adjacent vertices of `u`. To update the key values, interate through all adjacent vertices. For every adjacent vertex `v`, if weight of edge `u-v` is less the the previous keyu value of `v`, update the key value as weight of `u-v`

### Example
![[mst 1.png]]