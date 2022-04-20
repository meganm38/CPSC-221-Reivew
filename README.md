
# CPSC221 Review

# Table of Content
- [Asymptotic Analysis](#asymptotic-analysis)
- [Correctness](#correctness)
- [Data Structures](#data-structures)
  - [Array](#array)
  - [Linked List](#linked-list)
  - [Hash Table or Hash Map](#hash)
  - [Binary Tree](#binary-tree)
- [Algorithms](#algorithms)
    - [Sorting Algorithms](#sorting-algorithms)
        - [Selection Sort](#selection-sort)
        - [Insertion Sort](#insertion-sort)
        - [Merge Sort](#merge-sort)
        - [Quick Sort](#quick-sort)
  - [Search Algorithms](#search-algorithms)
    - [Breadth First Search](#breadth-first-search)
    - [Depth First Search](#depth-first-search)
- [C++ Review](#c++review)

# <a id="asymptotic-analysis"></a>Asymptotic Analysis

#### Complexities
The following are the Asymptotic rates of growth from best to worst:
- constant - ``O(1)`` 
- logarithmic – ``O(log n)`` 
- linear – ``O(n)``
- log-linear – ``O(n log n)`` 
- superlinear - ``O(n^(1+c))``
- polynomial – `O(n^c)` 
- exponential – `O(c^n)`
- factorial  – `O(n!)` 

#### Big-O notation
Big-O refers to the upper bound of time or space complexity of an algorithm, meaning it worst case runtime scenario. An easy way to think of it is that runtime could be better than Big-O but it will never be worse.
#### Big-Ω (Big-Omega) notation
Big-Omega refers to the lower bound of time or space complexity of an algorithm, meaning it is the best runtime scenario. Or runtime could worse than Big-Omega, but it will never be better.
#### Big-θ (Big-Theta) notation
Big-Theta refers to the tight bound of time or space complexity of an algorithm. Another way to think of it is the intersection of Big-O and Big-Omega, or more simply runtime is guaranteed to be a given complexity, such as `n log n`.
#### Comparing Functions
If <img src="https://render.githubusercontent.com/render/math?math=\lim_{n \to \infty} f(n)/g(n)">
- Goes to 0: f(n) is faster/smaller/better.
- Goes to infinity: g(n) is faster/smaller/better.
- Goes to constant, they are Big-Omega of each other.
#### Log rules
- Product:	``ln(xy)=ln(x)+ln(y)``
- Quotient:	``ln(x/y)=ln(x)−ln(y)``
- Log of power:	``ln(x^y)=yln(x)``

# <a id="correctness"></a>Correctness
#### Loop invariant
- The loop invariant holds just before the loop guard (the start of some iteration i)
- It states: for any iteration i in {...}, ...
- Try to draw invariant to understand it
#### Formal proof by induction in three parts
- Setup: How do we refer to loop iterations? -> **induction variable**. What property does the loop establish? -> **loop invariant**
- Showing the invariant holds: At first? -> **base case**. Then, does each iteration “restore” the invariant for the next? -> **inductive case**. Consider an arbitrary time we reach the guard i < n, assume the invariant holds **induction hypothesis** and show just before the next iteration i + 1, the invariant holds.
- Termination: The loop stops eventually. Finite number of steps.


## <a id="sorting-algorithms"></a>Sorting Algorithms

### <a id="selection-sort"></a>Selection Sort
#### Definition
- A comparison based sorting algorithm.
  - Starts with the cursor on the left, iterating left to right
  - Start from the index to the end of array, looking for the smallest item
    - If the left is smaller than the item to the right it continues iterating
    - If the left is bigger than the item to the right, the item on the right becomes the known smallest number
    - Once it has checked all items, it moves the known smallest to the index and advances the index to the right and starts over
  - As the algorithm processes the data set, it builds a fully sorted left side of the data until the entire data set is sorted
- Changes the array in place.

#### Code
```c++
void selectionSort(vector<int> & arry) {
   for (int i = 0; i < arr.size(); ++i) {
       int min = findMin(arr, i);
       swap(A[i], A[min]);
   }
}

int findMin(vector<int> & arr, int a) {
    int m = a;
    for (int i = a + 1; i < arr.size(); i++) {
        if (arr[i] < arr[m]) {
            m = i;
        }
    }
    return m;
}
```

#### Time Complexity
- Best Case Sort: `O(n^2)`
- Average Case Sort: `O(n^2)`
- Worst Case Sort: `O(n^2)`

#### Space Complexity
- Worst Case: `O(1)`

#### Visualization
![#](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)


### <a id="insertion-sort"></a>Insertion Sort
#### Definition
- A comparison based sorting algorithm.
  - Iterates left to right comparing the current cursor to the previous item.
  - Saves cursor in a temp variable. If the cursor is smaller than the item on the left it replaces its value with the smaller value on the left. The cursor moves towards left and compares the temp again to the left hand side until the item on the left is larger at which time the cursor replaces its current value with temp.
  - As the algorithm processes the data set, the left side becomes increasingly sorted until it is fully sorted.
- Changes the array in place.

#### Code
```c++
void insertionSort(vector<int> & arr) {
    for (int i = 1; i < n; i++) {
        putInPlace(arr, i);    
    }
}

void putInPlace(vector<int> & arr, int i) {
    int temp = arr[i];
    int j = i;
    while (j > 0 && arr[j-1] > temp) {
        arr[j] = arr[j-1];
        j--;
    }
    arr[j] = temp;
}
```
#### What you need to know
- Inefficient for large data sets, but can be faster for than other algorithms for small ones.
- Although it has an `O(n^2)` time complexity, in practice it is slightly less since its comparison scheme only requires checking place if it is smaller than its neighbor.

#### Time Complexity
- Best Case: `O(n)` (already sorted array)
- Average Case: `O(n^2)`
- Worst Case: `O(n^2)`

#### Space Complexity
- Worst Case: `O(n)`

#### Visualization
![#](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)


### <a id="merge-sort"></a>Merge Sort
#### Definition
- A divide and conquer algorithm.
  - Recursively divides entire array by half into subsets until the subset is one, the base case.
  - Once the base case is reached results are returned and sorted ascending left to right.
  - Recursive calls are returned and the sorts double in size until the entire array is sorted.

#### What you need to know
- This is one of the fundamental sorting algorithms.
- Know that it divides all the data into as small possible sets then compares them.

#### Time Complexity
- Worst Case: `O(n log n)`
- Average Case: `O(n log n)`
- Best Case: `O(n)`

#### Space Complexity
- Worst Case: `O(1)`

#### Visualization
![#](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Merge_sort_algorithm_diagram.svg/400px-Merge_sort_algorithm_diagram.svg.png)


### <a id="quick-sort"></a>Quicksort
#### Definition
- A divide and conquer algorithm
  - Partitions entire data set in half by selecting a random pivot element and putting all smaller elements to the left of the element and larger ones to the right.
  - It repeats this process on the left side until it is comparing only two elements at which point the left side is sorted.
  - When the left side is finished sorting it performs the same operation on the right side.
- Computer architecture favors the quicksort process.
- Changes the array in place.

#### What you need to know
- While it has the same Big O as (or worse in some cases) many other sorting algorithms it is often faster in practice than many other sorting algorithms, such as merge sort.

#### Time Complexity
- Worst Case: `O(n^2)`
- Average Case: `O(n log n)`
- Best Case: `O(n log n)`

#### Space Complexity
- Worst Case: `O(log n)`

#### Visualization
![#](https://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif)

#### Merge Sort Vs. Quicksort
- Quicksort is likely faster in practice, but merge sort is faster on paper.
- Merge Sort divides the set into the smallest possible groups immediately then reconstructs the incrementally as it sorts the groupings.
- Quicksort continually partitions the data set by a pivot, until the set is recursively sorted.


# <a id="data-structures"></a>Data Structures
### <a id="array"></a> Array
#### Definition
- Stores data elements based on an sequential, most commonly 0 based, index.
- Based on [tuples](http://en.wikipedia.org/wiki/Tuple) from set theory.
- They are one of the oldest, most commonly used data structures.

#### What you need to know
- Optimal for indexing; bad at searching, inserting, and deleting (except at the end).
- **Linear arrays**, or one dimensional arrays, are the most basic.
  - Are static in size, meaning that they are declared with a fixed size.
- **Dynamic arrays** are like one dimensional arrays, but have reserved space for additional elements.
  - If a dynamic array is full, it copies its contents to a larger array.
- **Multi dimensional arrays** nested arrays that allow for multiple dimensions such as an array of arrays providing a 2 dimensional spacial representation via x, y coordinates.

#### Time Complexity
- Indexing:         Linear array: `O(1)`,      Dynamic array: `O(1)`
- Search:           Linear array: `O(n)`,      Dynamic array: `O(n)`
- Optimized Search: Linear array: `O(log n)`,  Dynamic array: `O(log n)`
- Insertion:        Linear array: n/a,         Dynamic array: `O(n)`


### <a id="linked-list"></a> Linked List
#### Definition
- Stores data with **nodes** that point to other nodes.
  - Nodes, at its most basic it has one datum and one reference (another node).
  - A linked list _chains_ nodes together by pointing one node's reference towards another node.
#### Code snippet
```c++
class LinkedList {

    struct Node {
        int data; 
        Node* next; //the location of the next node
        Node* prev; //doubly linked list
        Node(int ndata, Node* nx = nullptr) : data(ndata), next(nx){}
    }

    Node* head;
    Node* back; //optional tail pointer
    int length;
    
    public:
        LinkedList();
}

// Initialize
Node* head = new Node(5, null);
head->next = new Node(3, null);

```
#### What you need to know
- Designed to optimize insertion and deletion, slow at indexing and searching.
    - Insertion in a singly linked list requires only updating the next node reference of the preceding position.
        ```c++
        Node* b = new Node(3, a->next);
        a->next = b;
        ```
    - Likewise, we can remove a node by updating the pointer of the preceding node, but remember to delete the removed node. 
        ```c++
        a->next = b->next;
        delete b;
        b = nullptr;
        ```
- **Doubly linked list** has nodes that also reference the previous node.
- **Circularly linked list** is simple linked list whose **tail**, the last node, references the **head**, the first node.
- **Stack**, commonly implemented with linked lists but can be made from arrays too.
  - Stacks are **last in, first out** (LIFO) data structures.
  - Made with a linked list by having the head be the only place for insertion and removal.
- **Queues**, too can be implemented with a linked list or an array.
  - Queues are a **first in, first out** (FIFO) data structure.
  - Made with a doubly linked list that only removes from head and adds to tail.

#### Time Complexity for Singly Linked Lists without Tail Pointer
- Search: `O(n)`
- Insertion in the middle: `O(n)`
- Insertation at front: `O(1)`
- Insertation at back: `O(1)`
- Deletion at front: `O(1)`
- Deletion at back: `O(n)`

#### Linked Lists Manipulation
- Print in reverse order (odd locations only)
    ```c++
    void printReverseOdds(Node* curr) {
        if (curr == nullptr) {
            return;
        }
        if (curr->next != nullptr) {
            printReverseOdds(curr->next->next);
        }
    }
    ```

### <a id="hash"></a> Hash Table or Hash Map
#### Definition
- Stores data with key value pairs.
- **Hash functions** accept a key and return an output unique only to that specific key.
  - This is known as **hashing**, which is the concept that an input and an output have a one-to-one correspondence to map information.
  - Hash functions return a unique address in memory for that data.

#### What you need to know
- Designed to optimize searching, insertion, and deletion.
- **Hash collisions** are when a hash function returns the same output for two distinct inputs.
  - All hash functions have this problem.
  - This is often accommodated for by having the hash tables be very large.
- Hashes are important for associative arrays and database indexing.

#### Time Complexity
- Indexing:         Hash Tables: `O(1)`
- Search:           Hash Tables: `O(1)`
- Insertion:        Hash Tables: `O(1)`


### <a id="binary-tree"></a> Binary Tree
#### Definition
- Is a tree like data structure where every node has at most two children.
  - There is one left and right child node.

#### What you need to know
- Designed to optimize searching and sorting.
- A **degenerate tree** is an unbalanced tree, which if entirely one-sided, is essentially a linked list.
- They are comparably simple to implement than other data structures.
- Used to make **binary search trees**.
  - A binary tree that uses comparable keys to assign which direction a child is.
  - Left child has a key smaller than its parent node.
  - Right child has a key greater than its parent node.
  - There can be no duplicate node.
  - Because of the above it is more likely to be used as a data structure than a binary tree.

#### Time Complexity
- Indexing:  Binary Search Tree: `O(log n)`
- Search:    Binary Search Tree: `O(log n)`
- Insertion: Binary Search Tree: `O(log n)`


# <a id="algorithms"></a> Algorithms
## <a id="search-algorithms"></a>Search Algorithms
### <a id="breadth-first-search"></a>Breadth First Search
#### Definition
- An algorithm that searches a tree (or graph) by searching levels of the tree first, starting at the root.
  - It finds every node on the same level, most often moving left to right.
  - While doing this it tracks the children nodes of the nodes on the current level.
  - When finished examining a level it moves to the left most node on the next level.
  - The bottom-right most node is evaluated last (the node that is deepest and is farthest right of it's level).

#### What you need to know
- Optimal for searching a tree that is wider than it is deep.
- Uses a queue to store information about the tree while it traverses a tree.
  - Because it uses a queue it is more memory intensive than **depth first search**.
  - The queue uses more memory because it needs to stores pointers

#### Time Complexity
- Search: Breadth First Search: O(V + E)
- E is number of edges
- V is number of vertices

### <a id="depth-first-search"></a>Depth First Search
#### Definition
- An algorithm that searches a tree (or graph) by searching depth of the tree first, starting at the root.
  - It traverses left down a tree until it cannot go further.
  - Once it reaches the end of a branch it traverses back up trying the right child of nodes on that branch, and if possible left from the right children.
  - When finished examining a branch it moves to the node right of the root then tries to go left on all it's children until it reaches the bottom.
  - The right most node is evaluated last (the node that is right of all it's ancestors).

#### What you need to know
- Optimal for searching a tree that is deeper than it is wide.
- Uses a stack to push nodes onto.
  - Because a stack is LIFO it does not need to keep track of the nodes pointers and is therefore less memory intensive than breadth first search.
  - Once it cannot go further left it begins evaluating the stack.

#### Time Complexity
- Search: Depth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices


#### Breadth First Search Vs. Depth First Search
- The simple answer to this question is that it depends on the size and shape of the tree.
  - For wide, shallow trees use Breadth First Search
  - For deep, narrow trees use Depth First Search

#### Nuances
  - Because BFS uses queues to store information about the nodes and its children, it could use more memory than is available on your computer. (But you probably won't have to worry about this.)
  - If using a DFS on a tree that is very deep you might go unnecessarily deep in the search. See [xkcd](http://xkcd.com/761/) for more information.
  - Breadth First Search tends to be a looping algorithm.
  - Depth First Search tends to be a recursive algorithm.

### <a id="c++review"></a> C++ Review
#### Pointers
``*`` means: pointer
``&`` means: reference type
``* operator`` means: dereference
``& operator`` means: address-of
