#  Linked lists
A **linked list** is a data structure that stores elements in sequence using nodes.
Each node contains a value and a pointer to the **next node** in the list.

Unlike arrays, nodes are **not stored contiguously in memory**.
```c#
public class Node {
    int value;
    Node next;

    public Node (int value) {
        this.value = value;
    }
}
```

## Arrays vs Linked Lists
| Operation                          | Array  | Linked List |
|------------------------------------|--------|-------------|
| Access element                     | `O(1`  | `O(n)`      |
| Insert/delete (arbitrary position) | `O(n)` | `O(1)`*     |

*-`O(1)` only if we already have a reference to the node before the insertion/deletion point. Otherwise we must traverse the list (`O(n)`).

The main trade-off:
* **Arrays** → fast random access
* **Linked lists** → fast insertion and deletion

## Traversal
The final node's `next` pointer is `null`. Traversal continues until the pointer becomes `null`.

### Iterative traversal
```c#
public int GetSum(Node head) {
    int sum = 0;

    while (head != null) {
        sum += head.value;
        head = head.next;
    }

    return sum;
}
```

### Recursive traversal
```c#
public int GetSum(Node head) {
    if (head == null)
        return 0;

    return head.value + GetSum(head.next);
}
```

### Using a dummy pointer
Sometimes we want to traverse the list **without losing the reference to `head`**.
```c#
public int GetSum(Node head) {
    int sum = 0;
    Node curr = head;

    while (curr != null) {
        sum += curr.value;
        curr = curr.next;
    }

    return sum;
}
```

## Types of Linked Lists
### Singly Linked List
Each node only stores a pointer to the **next node**, so traversal is only possible **forward**.
```c#
public class Node {
    int value;
    Node next;

    public Node(int value) {
        this.value = value;
    }
}
```

#### Insert node
If we know the node at position `i - 1`, insertion is `O(1)`.
```c#
public void AddNode(Node prevNode, Node nodeToAdd) {
    nodeToAdd.next = prevNode.next;
    prevNode.next = nodeToAdd;
}
```

#### Delete node
```c#
public void DeleteNode(Node prevNode) {
    prevNode.next = prevNode.next.next;
}
```

### Doubly Linked List
Each node stores pointers to both the next and previous nodes.

This allows traversal in **both directions**.
```c#
public class Node {
    int value;
    Node next;
    Node prev;

    public Node(int value) {
        this.value = value;
    }
}
```

#### Insert node
```c#
public void AddNode(Node node, Node nodeToAdd) {
    Node prevNode = node.prev;

    nodeToAdd.next = node;
    nodeToAdd.prev = prevNode;

    prevNode.next = nodeToAdd;
    node.prev = nodeToAdd;
}
```

#### Delete node
```c#
public void DeleteNode(Node node) {
    Node prevNode = node.prev;
    Node nextNode = node.next;

    prevNode.next = nextNode;
    nextNode.prev = prevNode;
}
```

### Linked Lists with Sentinel Nodes
**Sentinel nodes** are dummy nodes placed at the start and end of the list.

Even when the list is empty, `head` and `tail` still exist.
```shell
head <-> firstNode <-> ... <-> lastNode <-> tail
```

The real nodes are between `head` and `tail`.
```c#
Node head = new Node(-1);
Node tail = new Node(-1);

head.next = tail;
tail.prev = head;
```
This simplifies insertion and deletion because we never need to handle special cases for empty lists.

#### Add to end
```c#
public void AddToEnd(Node nodeToAdd) {
    nodeToAdd.next = tail;
    nodeToAdd.prev = tail.prev;

    tail.prev.next = nodeToAdd;
    tail.prev = nodeToAdd;
}
```

#### Remove from end
```c#
public void RemoveFromEnd() {
    if (head.next == tail)
        return;

    Node nodeToRemove = tail.prev;

    nodeToRemove.prev.next = tail;
    tail.prev = nodeToRemove.prev;
}
```

## Common Techniques
### Fast and Slow Pointers
This technique uses two pointers moving at **different speeds**.

Typically:
* `slow` moves 1 step
* `fast` moves 2 steps

A common use case is **finding the middle of a linked list**.
```c#
public int GetMiddle(Node head) {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow.value;
}
```

### Reversing a Linked List
To reverse a singly linked list we use three pointers:
* `prev` – previous node
* `curr` – current node
* `nextNode` – temporarily stores the next node

For each node:
1. Save the next node
2. Reverse the pointer
3. Move `prev` and `curr` forward
```c#
public Node ReverseLinkedList(Node head) {
    Node prev = null;
    Node curr = head;

    while (curr != null) {
        Node nextNode = curr.next;
        curr.next = prev;

        prev = curr;
        curr = nextNode;
    }

    return prev;
}
```
Time complexity: `O(n)`
Space complexity: `O(1)`

## Common Problem Patterns
Linked lists often appear in problems involving:
* **reversing a list**
* **finding the middle node**
* **cycle detection**
* **merging two lists**
* **removing the N-th node from the end**
* **reordering nodes**