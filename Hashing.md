# Hashing

## Hash Function
A **hash function** converts a **key** into an **integer within a fixed range**.

Properties:
* **Deterministic** — the same key always produces the same number
* Used to compute an **index in an array**.

## Hash Map (Hash Table / Dictionary)
A **hash map** stores **key → value pairs**.

How it works:
1. The key goes through a **hash function**
2. The result is used as **an array index**
3. The value is stored there

Characteristics:
* **Unordered**
* Keys are usually **immutable**

Disadvantages:
* **Overhead** can make them slower for very small inputs
* They **use more memory**
* **Resizing is expensive** because all keys must be rehashed
* Hashing strings takes `O(m)` where m is the string length

```c#
// Declaration
Dictionary<TKey, TValue> map = [];

// Initialize with some key-value pairs
Dictionary<int, int> map = new() {
   {1, 2},
   {5, 3},
   {7, 2}
};

// Checking if a key exists: use ContainsKey()
bool exists = map.ContainsKey(1); // true
bool exists = map.ContainsKey(9); // false

// Accessing a value by key
int value = map[5]; // 3

// Safer way to access a value
if (map.TryGetValue(5, out int value))
    Console.WriteLine(value);

// Adding or updating a key
map[5] = 6;   // updates existing key
map[9] = 15;  // inserts new key-value pair

// Removing a key
map.Remove(9);

// Get size
int size = map.Count; // 3

// Iterate over keys
foreach (int key in map.Keys)
    Console.WriteLine(key);

// Iterate over values
foreach (int value in map.Values)
    Console.WriteLine(value);

// Iterate over key-value pairs (most common way)
foreach (var pair in map)
    Console.WriteLine($"Key: {pair.Key}, Value: {pair.Value}");
```

Use **Dictionary** when you need to:
* **count occurrences**
* store a **mapping**
* store an **index**
* **group elements**

## Set
A **set** is similar to a hash map but stores only keys.

Operations (average `O(1)`):
* add
* remove
* check if element exists

Important: **Sets do not track frequency**.

Adding the same element multiple times still stores it only once.

```c#
// Declaration: HashSet stores unique elements (no duplicates)
HashSet<int> set = [];

// Initialize with some values
set = [1, 5, 7];

// Adding elements
set.Add(3);  // adds element if it doesn't exist
set.Add(5);  // does nothing because 5 already exists

// Checking if an element exists
bool exists = set.Contains(1); // true
bool exists = set.Contains(9); // false

// Removing an element
set.Remove(7);

// Get size
int size = set.Count;

// Iterate over elements
foreach (int value in set)
    Console.WriteLine(value);

// Clear the set (remove all elements)
set.Clear();

// Check if set is empty
bool isEmpty = set.Count == 0;
```

Use **HashSet** when you need to:
* check **whether an element exists**
* **remove duplicates**
* keep track of **visited elements**
