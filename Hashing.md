# Hashing
## Hashing
A **hash function** converts a **key** into an **integer within a fixed range**.

The result of the hash function is typically used as an **index in an array**.

### Properties
* **Deterministic** — the same key always produces the same value
* Efficient to compute
* Distributes keys across the available indices

## Hash Map (Hash Table / Dictionary)
A **hash map** stores **key** → **value pairs**.

### How it works
1. The key is passed through a **hash function**
2. The hash determines an **index in an array**
3. The value is stored at that location

### Characteristics
* **Unordered**
* Keys are usually **immutable**
* Average-case operations are `O(1)`

### Disadvantages
* **Higher memory usage**
* **Overhead** can make them slower for very small inputs
* **Resizing is expensive** because keys must be rehashed
* Hashing strings takes `O(m)` time where `m` is the string length

```c#
// Declaration
Dictionary<TKey, TValue> map = [];

// Initialize with key-value pairs
Dictionary<int, int> map = new() {
   {1, 2},
   {5, 3},
   {7, 2}
};

// Check if a key exists
bool exists = map.ContainsKey(1); // true
bool exists = map.ContainsKey(9); // false

// Access value by key
int value = map[5]; // 3

// Safer access
if (map.TryGetValue(5, out int value))
    Console.WriteLine(value);

// Add or update
map[5] = 6;   // update
map[9] = 15;  // insert

// Remove key
map.Remove(9);

// Size
int size = map.Count;

// Iterate keys
foreach (int key in map.Keys)
    Console.WriteLine(key);

// Iterate values
foreach (int value in map.Values)
    Console.WriteLine(value);

// Iterate key-value pairs
foreach (var pair in map)
    Console.WriteLine($"Key: {pair.Key}, Value: {pair.Value}");
```

### Hash Map Operations
| Operation | Description                     | Average Time  |
|-----------|---------------------------------|---------------|
| Insert    | Add or update a key-value pair  | `O(1)`        |
| Lookup    | Access value by key             | `O(1)`*       |
| Delete    | Remove a key                    | `O(1)`*       |

Worst-case time complexity can degrade to `O(n)` if many collisions occur.

### Common Use Cases
Use a **hash map** when you need to:
* **count occurrences**
* store a **mapping**
* store an **index**
* **group elements**
* perform **fast lookups**

## Set
A **set** is similar to a hash map but stores **only keys**.

Each element can appear **at most once**.

Adding the same element multiple times still stores it only once.

```c#
// Declaration
HashSet<int> set = [];

// Initialize with values
set = [1, 5, 7];

// Add elements
set.Add(3);  // added
set.Add(5);  // ignored (already exists)

// Check existence
bool exists = set.Contains(1); // true
bool exists = set.Contains(9); // false

// Remove element
set.Remove(7);

// Size
int size = set.Count;

// Iterate elements
foreach (int value in set)
    Console.WriteLine(value);

// Clear set
set.Clear();

// Check if empty
bool isEmpty = set.Count == 0;
```

### Set Operations
| Operation | Description         | Average Time  |
|-----------|---------------------|---------------|
| Add       | Insert element      | `O(1)`        |
| Remove    | Delete element      | `O(1)`*       |
| Contains  | Check existence     | `O(1)`*       |

### Common Use Cases
Use a `HashSet` when you need to:
* check **whether an element exists**
* **remove duplicates**
* keep track of **visited elements**
* perform **fast membership checks**

Important: **sets do not track frequency**.
If you need counts, use a **hash map** instead.