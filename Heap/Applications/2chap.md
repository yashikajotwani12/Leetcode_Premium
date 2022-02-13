## Constructing a Heap
 means initializing an instance of a Heap. All methods of Heap need to be performed on an instance. Therefore, we need to initialize an instance before applying the methods. When creating a Heap, we can simultaneously perform the heapify operation. Heapify means converting a group of data into a Heap.

* Time complexity: O(N)O(N).
* Space complexity: O(N)O(N).

## Inserting an Element

Insertion means inserting a new element into the Heap. Note that, after the new element is inserted, properties of the Heap are still maintained.

* Time complexity: O(\log N)O(logN)
* Space complexity: O(1)O(1)

## Getting the Top Element of the Heap

The top element of a Max heap is the maximum value in the Heap, while the top element of a Min Heap is the smallest value in the Heap. The top element of the Heap is the most important element in the Heap.

* Time complexity: O(1)O(1).
* Space complexity: O(1)O(1).

## Deleting the top element

Note that, after deleting the top element, the properties of the Heap will still hold. Therefore, the new top element in the Heap will be the maximum (for Max Heap) or minimum (for Min Heap) of the current Heap.

* Time complexity: O(\log N)O(logN).
* Space complexity: O(1)O(1).

## Getting the Length of a Heap

The length of the Heap can be used to determine the size of the current heap, and it can also be used to determine if the current Heap is empty. If there are no elements in the current Heap, the length of the Heap is zero.

* Time complexity: O(1)O(1)
* Space complexity: O(1)O(1)
  
![TC and SC](../../Images/Screenshot%202022-02-13%20103739.png)