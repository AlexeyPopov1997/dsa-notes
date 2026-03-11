#  Linked lists
A linked list is a data structure that is similar to an array. It also stores data in an ordered manner, but it is implemented using node objects. Each node will have a "next" pointer, which points to the node representing the next element in the sequence.
```c#
public class Node {
    int value;
    Node next;

    public Node (int value) {
        this.value = value;
    }
}
```

## Advantages and disadvantages compared to arrays
The main advantage of a linked list is that you can add and remove elements at any position in `O(1)`. The caveat is that you need to have a reference to a node at the position in which you want to perform the addition/removal, otherwise the operation is `O(n)`, because you will need to iterate starting from the headuntil you get to the desired position. However, this is still much better than a normal (dynamic) array, which requires `O(n)` for adding and removing from an arbitrary position.

The main disadvantage of a linked list is that there is no random access. If you have a large linked list and want to access the 150,000th element, then there usually isn't a better way than to start at the head and iterate 150,000 times. So while an array has `O(1)` indexing, a linked list could require `O(n)` to access an element at a given position.

## Mechanics of a linked list
### Assignment (=)
When you assign a pointer to an existing linked list node, the pointer refers to the object in memory. Let's say you have a node head:
```c#
Node ref = head;
head = head.next;
head = null;
```

### Chaining .next
If you have multiple `.next`, for example `head.next.next`, everything before the final `.next` refers to one node. For example, given a linked list `1 -> 2 -> 3`, if you have head pointing at the first node, and you do `head.next.next`, you are actually referring to `2.next`, because `head.next` is the `2`.

### Traversal
The final node's `next` pointer is `null`. Therefore, after doing `head = head.next` at the final node, `head` becomes `null` and the while loop ends.
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

Moving to `head.next` is the equivalent of iterating to the next element in an array. Traversal can also be done recursively:
```c#
public int GetSum(Node head) {
    if (head == null)
        return 0;

    return head.value + GetSum(head.next);
}
```

## Types of linked lists
### Singly linked list
This is the most common type of linked list and the one that is given in the code above. In a singly linked list, each node only has a pointer to the next **node**. This means you can only move forward in the list when iterating. The pointer used to reference the next node is usually called `next`.
```c#
public class Node {
    int value;
    Node next;

    public Node (int value) {
        this.value = value;
    }
}

// Let prevNode be the node at position i - 1
public void AddNode(Node prevNode, Node nodeToAdd) {
    nodeToAdd.next = prevNode.next;
    prevNode.next = nodeToAdd;
}

// Let prevNode be the node at position i - 1
public void DeleteNode(Node prevNode) {
    prevNode.next = prevNode.next.next;
}
```

As mentioned before, when you have a reference to the node at `i - 1`, then insertion and deletion is `O(1)`. However, without that reference, you need to obtain the reference by iterating from the head, which for an **arbitrary** position is `O(n)`.

### Doubly linked list
A doubly linked list is like a singly linked list, but each node also contains a pointer to the previous node. This pointer is usually called `prev`, and it allows iteration in both directions.
```c#
public class Node {
    int value;
    Node next;
    Node prev;

    public Node (int value) {
        this.value = value;
    }
}

public void AddNode(Node node, Node nodeToAdd) {
    Node prevNode = node.prev;
    nodeToAdd.next = node;
    nodeToAdd.prev = prevNode;
    prevNode.next = nodeToAdd;
    node.prev = nodeToAdd;
}

public void DeleteNode(ListNode node) {
    ListNode prevNode = node.prev;
    ListNode nextNode = node.next;
    prevNode.next = nextNode;
    nextNode.prev = prevNode;
}
```
