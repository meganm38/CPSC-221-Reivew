
# UBC CPSC 221 Basic Algorithms and Data Structures: Review

# Table of Content
- [Asymptotic Analysis](#asymptotic-analysis)
- [Correctness](#correctness)
- [Data Structures](#data-structures)
  - [Linked List](#linked-list)
  - [Stack](#stack)
  - [Queue](#queue)
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

#### Code
```c++
    void mergesort(vector<int> & A) {
        mergesort(A, 0, A.size() - 1);
    }
    
    void mergesort(vector<int> &A, int lo, int hi) {
        if (lo >= hi) return;
        int mid = (lo + hi) / 2;
        mergesort(A, lo, mid);
        mergesort(A, mid + 1, hi);
        merge(A, low, mid, hi);
    }
```

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

#### Visualization
![#](https://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif)

#### Merge Sort Vs. Quicksort
- Quicksort is likely faster in practice, but merge sort is faster on paper.
- Merge Sort divides the set into the smallest possible groups immediately then reconstructs the incrementally as it sorts the groupings.
- Quicksort continually partitions the data set by a pivot, until the set is recursively sorted.


# <a id="data-structures"></a>Data Structures
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
- **Sentinel linked lists** Sentinel node is a special node that doesn't count as content at the front of the list. Reduces special cases.
- **Circularly linked list** is simple linked list whose **tail**, the last node, references the **head**, the first node.

#### Time Complexity for Singly Linked Lists without Tail Pointer
- Search: `O(n)`
- Insertion in the middle: `O(n)`
- Insertation at front: `O(1)`
- Insertation at back: `O(1)`
- Deletion at front: `O(1)`
- Deletion at back: `O(n)`

#### Linked Lists Manipulation ``O(n)``
- Insert at back iteratively ``O(n)``
    ```c++
    void insertAtBack(Node*& head, int new) {
        if (head == nullptr) {
            head = new Node(new, nullptr);
            return;
        }
        Node* curr = head;
        while(curr->next != nullptr) {
            curr = curr->next;
        }
        curr->next = new Node(new, nullptr);
    }
    ``` 
- Print in reverse order recursivly(odd locations only) ``O(n)``
    ```c++
    void printReverseOdds(Node* curr) {
        if (curr == nullptr) {
            return;
        }
        if (curr->next != nullptr) {
            printReverseOdds(curr->next->next);
        }
        cout << curr->data << endl;
    }
    ``` 
- Reverse the list recursivly without copying``O(n)``
   ```c++
    Node* reverse(Node* curr) {
        if (curr == nullptr || curr->next == nullptr) {
            return curr;
        }
        Node* result = reverse(curr->next);
        curr->next->next = curr;
        curr->next = nullptr;
        return result;
    }
    ```
- Reverse doubly linked list iteratively ``O(n)``
   ```c++
    Node* reverse(Node* curr) {
        Node* result = nullptr;
        while (curr != nullptr) {
            Node* nextNode = curr->next;
            curr->next = curr->prev;
            curr->prev = nextNode;
            result = curr;
            curr = curr->prev;
        }
        return result;
    }
    ```
    
### <a id="stack"></a> Stack
#### Definition
FILO: last in first out

#### Linked list implementation ``O(1) push and pop``
Have the head be the only place for insertion and removal.
  ```c++
  class Stack {
      Stack();
      bool empty() const;
      void push(const int integer);
      int pop();
      
      private:
        struct Node{
          int data;
          Node* next;
        };
        Node* top;
  }
  ```
  
   ```c++
  void Stack::push(int integer) {
      Node* node = new Node(integer);
      node.next = top;
      top = node;
      }
  }
  
  int Stack::pop() {
      assert(!empty());
      int result = top->data;
      Node* newTop = top->next;
      delete top;
      top = newTop;
      return result;
  }
  
  bool Stack::empty() {
      return top == nullptr;
  }
  
  void ~Stack() {
      while (!empty()) {
          pop();
      }
  }
  ```
#### Array based implementation ``O(1) push and pop``
Resize array: Upon insertion (push), if the array is full, create a larger space and copy the data into it.
- Constant additions to array size: k = n/c copy events, ``O(n^2)`` operations of n pushes, ``O(n)`` operations per push.
- Double the array size: k = lg(n) copy events, ``O(n)``operations of n pushes, ``O(1)`` operations per push.
- Remember to deallocate old array memeory by calling delete[] array;

### <a id="queue"></a> Queue
#### Definition
FIFO: first in first out
Made with a singly linked list that has head and tail pointers. Dequeue from head, enqueue from tail.

#### Linked list implementation ``O(1) push and pop``
```c++
    class Queue {
        public:
        Queue();
        bool empty() const;
        void enqueue(const int integer);
        int dequeue();
        
        private:
        struct Node {
           int data;
           Node* next;
        };
        Node* front;
        Node* back;
    }   
```

```c++
  void Queue::enqueue(int integer) {
      Node* node = new Node(integer);
      if (empty()) {
          front = back = node;
      } else {
          back->next = node;
          back = node;
      }
  }
```

```c++
  void int Queue::dequeue() {
      assert(!empty());
      int value = front->data;
      Node* temp = front->next;
      delete front;
      front = temp;
      return value;
  }
```
#### Array based implementation ``O(1) push (average per push) and pop``
Use a circular array and resize array if is full.

```c++
class Queue {
  public：
      Queue();
      bool empty();
      void enqueue (const int integer)
      int dequeue();
    
  private:
      int size; //capacity of queue
      int front, back;
      void resize();
      bool full() const;     
      int* Q;
};
```

```c++
  void Queue::enqueue(int integer) {
      if(full) {
        resize();
      }
      Q[back] = integer;
      back++;
      back = back % size;
  }
```

```c++
  int Queue::dequeue() {
      assert(!empty());
      int value = Q[front];
      front ++;
      front = front % size;
      return value;
   }
```
```c++
  bool full() {
      return back = front - 1 || (front == 0 && back = size - 1);
  } 
```

```c++
   void Queue::resize() {
      int* newQ = new int[size * 2];
      if (front < back) {
      int index = 0;
        for (int i = front; i < back; i++) {
            newQ[index++] = Q[i];
        }
       } else {
         for (int i = front; i < size; i++）{
            newQ[index++] = Q[i];
         }
         for (int i = 0; i < back; i++) {
            newQ[index++] = Q[i];
         }
      }
      delete[] Q;
      Q = newQ;
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
