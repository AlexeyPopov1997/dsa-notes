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
