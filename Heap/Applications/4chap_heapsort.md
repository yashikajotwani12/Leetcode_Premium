# Heap Sort

### Heap Sort sorts a group of unordered elements using the Heap data structure.

## The sorting algorithm using a Min Heap is as follows:

## Heapify all elements into a Min Heap.
* Record and delete the top element.
* Put the top element into an array T that stores all sorted elements. 
* Now, the Heap will remain a Min Heap.
* Repeat steps 2 and 3 until the Heap is empty.
*  The array T will contain all elements sorted in ascending order.
  
## The sorting algorithm using a Max Heap is as follows:

## Heapify all elements into a Max Heap.
* Record and delete the top element.
* Put the top element into an array T that stores all sorted elements. 
* Now, the Heap will remain a Max Heap.
* Repeat steps 2 and 3 until the Heap is empty.
*  The array T will contain all elements sorted in descending order.
  
## Complexity Analysis:

### Let NN be the total number of elements.

* Time complexity: O(N \log N)O(NlogN)
* Space complexity: O(N)O(N)

### Heap Sort Video
Using a heap to obtain a sorted array involves converting the unsorted array into a heap, then popping the elements from the heap one at a time and adding them to the new sorted array. The following video will walk through this process step by step for a Min Heap to obtain an array sorted in ascending order. The process for a Max Heap would be the same, except that the sorted array would be in descending order.

