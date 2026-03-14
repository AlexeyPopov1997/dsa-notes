## Two pointer
Start the pointers at the edges of the input. Move them towards each other until they meet.

```c#
void Function(int[] arr)
{
    int left = 0;
    int right = arr.Length - 1;

    while (left < right)
    {
        // Do some logic here depending on the problem

        // Decide how to move pointers:
        // 1. left++
        // 2. right--
        // 3. both

        // Example structure:
        if (/* condition */)
        {
            left++;
        }
        else if (/* another condition */)
        {
            right--;
        }
        else
        {
            left++;
            right--;
        }
    }
}
```

### Time Complexity
Two-pointer algorithms usually run in `O(n)` time because each pointer moves across the array **at most once**.

### Common Problem Patterns
Two pointers are commonly used for:
* **two sum in a sorted array**
* **checking palindromes**
* **removing duplicates**
* **partitioning arrays**
* **container with most water**

## Sliding window
It’s a two-pointer technique where:
* right expands the window
* left shrinks it when a condition is violated

```c#
void Function(int[] arr)
{
    int left = 0;

    for (int right = 0; right < arr.Length; right++)
    {
        // add arr[right] to window

        while (/* window is invalid */)
        {
            // remove arr[left] from window
            left++;
        }

        // update answer using current window
    }
}
```

### Time Complexity
Even though this contains a nested loop, the complexity is still `O(n)` because each element enters and leaves the window **at most once**.

### Common Problem Patterns
Sliding window is commonly used for:
* **longest substring without repeating characters**
* **maximum sum subarray of size k**
* **minimum window substring**
* **counting valid subarrays**
* **frequency-based substring problems**


## Prefix sum
Precompute cumulative sums so you can answer range sum queries in `O(1)`.

Useful when you need fast subarray sums or counting subarrays with a given sum.

```c#
int[] BuildPrefix(int[] arr)
{
    int[] prefix = new int[arr.Length + 1];
    prefix[0] = 0;

    for (int i = 1; i <= arr.Length; i++)
    {
        prefix[i] = prefix[i - 1] + arr[i - 1];
    }

    return prefix;
}
```

### Time Complexity
| Operation        | Time   |
|------------------|--------|
| Time Complexity  | `O(n)` |
| Query range sum  | `O(1)` |

### Common Problem Patterns
Prefix sums are useful for:
* **range sum queries**
* **counting subarrays with a given sum**
* **difference between ranges**
* **cumulative statistics**