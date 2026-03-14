# Stacks and Queues
## Stacks
A **stack** is an ordered collection of elements where elements are added and removed from the **same end**. Stacks follow the **LIFO (last in, first out)** principle: the most recently added element is the first one removed.

The defining property of a stack is that all operations occur at one end, commonly called the **top**. A stack is an **abstract data type**, meaning the concept is independent of its implementation. In practice, stacks are commonly implemented using **dynamic arrays** or **linked lists**.

Stacks are closely related to recursion, because most programming languages implement function calls using a **call stack**. Each function call is pushed onto the stack, and the function at the top is the currently active one. When a function returns, it is popped from the stack and execution continues with the previous call.
```c#
// Declaration
Stack<int> stack = new();

// Push elements
stack.Push(1);
stack.Push(2);
stack.Push(3);

// Pop elements
stack.Pop(); // 3
stack.Pop(); // 2

// Check element at top
stack.Peek(); // 1

// Check if not empty
bool notEmpty = stack.Count > 0;

// Get size
int size = stack.Count; // 1
```

### Stack operations
| Operation | Description         | Time        |
|-----------|---------------------|-------------|
| Push      | Add element to top  | `O(1)`      |
| Pop       | Remove top element  | `O(1)`*     |
| Peek      | Read top element    | `O(1)`*     |
| Size      | Number of elements  | `O(1)`*     |

### Common problem patterns
Stacks are commonly used in problems involving:
* **Matching parentheses**
* **Expression evaluation**
* **Backtracking**
* **Depth-first search (DFS)**
* **Undo / redo commands**

## Queues
A **queue** follows the **FIFO (first in, first out)** principle. Unlike a stack, elements are **added and removed from opposite ends**.

Adding an element is called **enqueue**, and removing one is called **dequeue**. Elements are typically **added at the back** of the queue and **removed from the front**.

Queues are commonly implemented using a **linked list** or a **circular buffer**.
```c#
// Declaration
Queue<int> queue = new();

// Initialize with values
Queue<int> queue = new([1, 2, 3]);

// Enqueue elements
queue.Enqueue(4);
queue.Enqueue(5);

// Dequeue elements
queue.Dequeue(); // 1
queue.Dequeue(); // 2

// Check element at front
queue.Peek(); // 3

// Check if not empty
bool notEmpty = queue.Count > 0;

// Get size
int size = queue.Count; // 3
```

### Queue operations
| Operation | Description                | Time        |
|-----------|----------------------------|-------------|
| Enqueue   | Add element to back        | `O(1)`      |
| Dequeue   | Remove element from front  | `O(1)`*     |
| Peek      | Read front element         | `O(1)`*     |
| Size      | Number of elements         | `O(1)`*     |

### Common problem patterns
Queues are commonly used in:
* **Breadth-first search (BFS)**
* **Task scheduling**
* **Producer–consumer systems**
* **Rate limiting**
* **Level-order traversal in trees**

## Deque
A **deque** (double-ended queue, pronounced "deck") allows elements to be **added and removed from both ends**.

A standard queue allows:
* enqueue at the back
* dequeue from the front

A deque supports operations on **both the front and the back**.

## Monotonic Stack / Queue
A **monotonic stack** or **monotonic queue** maintains its elements in either **increasing** or **decreasing order**. Before inserting a new element, elements that would violate the ordering property are removed.

For example, consider a **monotonically increasing stack**:
```c#
stack = [1, 5, 8, 15, 23]
```

If we want to push `14`, we remove elements greater than it:
```bash
pop 23
pop 15
push 14
```

Result:
```c#
stack = [1, 5, 8, 14]
```

```c#
int[] nums = [1, 2, 3, 4, 5];
var stack = new Stack<int>();

foreach (var num in nums)
{
    while (stack.Count > 0 && stack.Peek() >= num)
        stack.Pop();

    // Logic depending on the problem
    stack.Push(num);
}
```

Even though this code contains a nested loop, the time complexity is still `O(n)`. Each element can be pushed and popped **at most once**, so the total number of operations across all iterations is linear.

This pattern is frequently used when solving problems involving **nearest elements**.

### When to think about a monotonic stack
Consider using a monotonic stack when a problem asks for:
* the **next greater element**
* the **previous smaller element**
* the **nearest element** satisfying some condition
* maintaining **minimum or maximum values in a dynamic window**