# Heap data structure
> Heap is a data structure that can fundamentally change the performance of fairly common algorithms in Computer Science.

> In this lesson we discuss the key operations of the Heap data stucture along with their performance. We then implement the data stucture using TypeScript / JavaScript.

The heap data structure is called a heap because it satisfies the heap property: if P is a parent node of C, then the key (the value) of node P is less than the key of node C.

* Its nice to have a mental model of a heap as a `complete binary tree`.
* Here we have a graph of nodes `a,b,c,d,e`
* This tree would satisfy the heap property if `A` is less than its children `B` and `C` Similarly `B` is less than its children `D` and `E`.
* Note that if the heap property is satified for direct children it is also automatically satisfied for any indirect children. e.g. A < D and A < E.
* Essentially this implies that the *smallest* item in the tree, has to be the root node.

```
           A
         ↙   ↘
       B       C
     ↙   ↘
    D     E

A < B
A < C
B < D
B < E

A < D
A < E
```

Note that a given set of keys can be arranged in multiple ways to satisfy the heap property. E.g.

* Given 4,4,5,6,9
* we can have the following two trees, Both are perfectly valid.
* The only position that is guaranteed to be the same is that the root node will be the item with the smallest key.
```
4,4,5,6,9

Example Tree
           4
         ↙   ↘
       5       4
     ↙   ↘
    6     9

Example Tree
           4
         ↙   ↘
       4       5
     ↙   ↘
    9     6
```


Even though its nice to have a mental model of a heap as a `complete binary tree`, they are normally implemented as an array. An array provides very low memory overhead and the left and right nodes can be calculated quite easily.

* Consider the simple array of indexes 0-13.
* It can be *conceptualized* as a tree with indexes corresponding to items of the array. When we are done with the left and right nodes at a level, we start a new level, and consider the indexes as the left and right of items of the previous level. We stop whenever we run out of items in the array.
* Given a node at index `n` lets, try and figure out a formula to find the index for its left child node. Always good to right down a few examples we can use to test our forumula.
* The key realization for the formula is that an item at index n will essentially have n spaces on its left and one more to arrive at its left node.
* So we arrive at `2n+1`. Our examples are all satisfied by this equation.
* The right is simply one plus the left, so its `2n+2`.

```
[] = 0,1,2,3,4,5,6,7,8,9,10,11,12,13

                0
           ╱       ╲
         ↙            ↘
       1                2
     ↙   ↘           ↙    ↘
   3       4        5       6
 ↙  ↘    ↙  ↘    ↙  ↘    ↙
7    8   9   10  11  12  13

left(0) = 1
left(1) = 3
left(3) = 7

    n -> n items on the right
  + 1

left(n) = n + n + 1 = 2n + 1
left(0) = 2(0) + 1 = 1
left(1) = 2(1) + 1 = 3
left(3) = 2(3) + 1 = 7

right(n) = 2n + 2
```

We start off by creating a generic class for a Heap for items of type T.
Each data structure has its strenghts. The raison d'etre of the heap data structure is its O(logn) `insert` and `extract` operations.

Lets add a `size` method, it is simply the length of the underlying array.

Another useful method to have is `peek` which instead of removing only looks at the value.

Worth mentioning is the fact that a heap can easily be changed into a `max` heap by simply changing the logic in the `comparison` function.

In future lessons we will see a few use cases where this O(logn) insertion and extract can greatly improve efficiency of simple programming challanges. Basically whenever you see an algorithm requiring repeated minimium (or maximum) computations, consider using a heap.

