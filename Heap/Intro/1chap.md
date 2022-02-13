# Definition and Classification of Heap

## Priority Queues
Before introducing a Heap, let's first talk about a Priority Queue.

* a priority queue is an abstract data type similar to a regular queue or stack data structure in which each element additionally has a "priority" associated with it. In a priority queue, an element with high priority is served before an element with low priority.

* In daily life, we would assign different priorities to tasks, start working on the task with the highest priority and then proceed to the task with the second highest priority. This is an example of a Priority Queue.

A common misconception is that a Heap is the same as a Priority Queue, which is not true. A priority queue is an abstract data type, while a Heap is a data structure. Therefore, a Heap is not a Priority Queue, but a way to implement a Priority Queue.

There are multiple ways to implement a Priority Queue, such as array and linked list. 
However, these implementations only guarantee O(1)O(1) time complexity for either insertion or deletion, while the other operation will have a time complexity of O(N)O(N). On the other hand, implementing the priority queue with Heap will allow both insertion and deletion to have a time complexity of O(\log N)O(logN). So, what is a Heap?

In this chapter, we will learn to:

* Understand the Heap data structure.
* Understand Max Heap and Min Heap.
* Understand the insertion and deletion of a Heap.
* Implement a Heap.


## Definition of Heap
According to Wikipedia, a Heap is a special type of binary tree. A heap is a binary tree that meets the following criteria:

Is a complete binary tree;
The value of each node must be no greater than (or no less than) the value of its child nodes.
A Heap has the following properties:

Insertion of an element into the Heap has a time complexity of O(\log N)O(logN);
Deletion of an element from the Heap has a time complexity of O(\log N)O(logN);
The maximum/minimum value in the Heap can be obtained with O(1)O(1) time complexity.


## Classification of Heap
* There are two kinds of heaps: Max Heap and Min Heap.

* Max Heap: Each node in the Heap has a value no less than its child nodes. Therefore, the top element (root node) has the largest value in the Heap.

* Min Heap: Each node in the Heap has a value no larger than its child nodes. Therefore, the top element (root node) has the smallest value in the Heap.
  
![Min Heap/ Max Heap](../../Images/1_1_min_max_heap_diagram_new.png)
