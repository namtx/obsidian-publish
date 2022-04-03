
### What is a Priority Queue
A priority queue is a Abstract Data Type (ADT) that operaates similar to a normal queu except that **each element has a certain priority**. The priority of the elements in the priority queue determine the order in which elements are removed from the PQ

**NOTE:** Priority queues only supports **comparable data**, meaning the data inserted into the priority queue must be able to be ordered in some way either from least to greatest or greatest to least. This is so that we are able to assign relative priorities to each element.

### What is a Heap?

A heal is a tree based DS that satisfies the **heap invariant** (heap property):
If A is a parent node of B then B is ordered with respect to B for a nodes A, B in the heap.


### Complexity
- Construction: `O(n)`
- Polling: `O(log(n))`
- Peeking: `O(1)`
- Adding: `O(log(n))`

### Turning Min PQ into Max PQ
_Problem_: Often the standard of most programming language only provides a min PQ which sorts by smallest elemens first, but sometimes we need a Max PQ.

_Solution_: negate the comparator

### Insertion
The Priority Queue (PQ) is an **Abstract Data Type (ADT)**, hence heaps are not the only way to implent PQs.

There are many types of heaps we could use to implement a priority queue including:
- Binary Heap
- Fibonacci Heap
- Binomial Heap
- Pairing Heap

#### Binary Heap
is a `Binary Tree` that supports the `heap invariants`

Binary Heap representation:

![[Binary heap representation.png]]

Let `i` be the parent node index
Left children index: `2i + 1`
Right children index: `2i + 2`

Insertion steps:
- Add the being inserted element to the last index
- Bubble up that element to keep the Heap invariant by swapping it with its parent.

```java
package dev.namtx.ds;  
  
import java.util.ArrayList;  
import java.util.List;  
  
public class BinaryHeap {  
	List<Integer> heap;  
 
	public BinaryHeap() {  
		this.heap = new ArrayList<>();  
	}  
 
	public static void main(String[] args) {  
		BinaryHeap binaryHeap = new BinaryHeap();  
		binaryHeap.insert(1);  
		binaryHeap.insert(2);  
		binaryHeap.insert(3);  
		binaryHeap.insert(0);  
	}  
 
	public void insert(int n) {  
		heap.add(n);  
		int i = heap.size() - 1;  
		while (i > 0 && heap.get(i) < heap.get(parent(i))) {  
			swap(i, parent(i));  
			i = parent(i);  
		}
	}
	
	private int parent(int i) {  
		return (i - 1) / 2;  
	}  
 
	private void swap(int i, int j) {  
		int temp = heap.get(i);  
		heap.set(i, heap.get(j));  
		heap.set(j, temp);  
	}
}
```

### Removal

#### Pool
- Swap the first node with the last
- remove the last
- Bubble down the root to keep `Heap invariant`, by swapping the root with its smallest child.

```java
public int poll() {  
	int result = heap.get(0);  
	heap.set(0, heap.get(heap.size() - 1));  
	heap.remove(heap.size() - 1);  
	heapify(0);  
	return result;  
}

private void heapify(int i) {  
	int left = left(i);  
	int right = right(i);  
	int largest = i;  
	if (left < heap.size() && heap.get(left) < heap.get(largest)) {  
		largest = left;  
	}  
	if (right < heap.size() && heap.get(right) < heap.get(largest)) {  
		largest = right;  
	}  
	if (largest != i) {  
		swap(i, largest);  
		heapify(largest);  
	}  
}  

private int left(int i) {  
	return 2 * i + 1;  
}  
  
private int right(int i) {  
	return 2 * i + 2;  
}
```

#### Remove
- Find that element, which takes `O(n)`
- Swap it with the last node
- Remove the last node
- Bubble down the swapped node to keep `Heap invariant`

```java
private void remove(int n) {
    int i = 0;
    while (i < heap.size()) {
 	   if (heap.get(i) == n) {
 		   heap.set(i, heap.get(heap.size() - 1));
 		   heap.remove(heap.size() - 1);
 		   heapify(i);
 		   return;
 	   }
 	   i++;
    }
}
```

### References
- https://www.youtube.com/watch?v=wptevk0bshY