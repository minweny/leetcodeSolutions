### In-Place Quicksort

Here's a more efficient, **in-place** version of Quicksort that uses the same divide-and-conquer principle but avoids creating additional lists:

```python
def quicksort(arr, low, high):
    """
    In-place Quicksort algorithm.
    :param arr: The input array.
    :param low: The starting index of the subarray.
    :param high: The ending index of the subarray.
    """
    if low < high:
        # Partition the array and get the pivot index
        pi = partition(arr, low, high)
        
        # Recursively sort the left and right subarrays
        quicksort(arr, low, pi - 1)
        quicksort(arr, pi + 1, high)

def partition(arr, low, high):
    """
    Partition the array into two parts based on a pivot.
    :param arr: The input array.
    :param low: The starting index of the subarray.
    :param high: The ending index of the subarray.
    :return: The index of the pivot element.
    """
    pivot = arr[high]  # Pivot is the last element
    i = low - 1         # Pointer for the smaller element
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]  # Swap if element is smaller than or equal to pivot
    arr[i + 1], arr[high] = arr[high], arr[i + 1]  # Swap the pivot into the correct position
    return i + 1

# Example usage:
arr = [3, 6, 8, 10, 1, 2, 1]
quicksort(arr, 0, len(arr) - 1)
print(f"Sorted array: {arr}")
```

### Explanation:

- **In-place partitioning**: The key difference in this version is the partitioning process, which works **in place** (i.e., no new arrays are created). The array is modified during the partitioning process by swapping elements around the pivot.
- **Low and high**: We pass the `low` and `high` indices to the recursive calls to sort the subarrays in place.
- **Pivot selection**: In this implementation, the pivot is always selected as the **last element** (`arr[high]`), but you could adjust this to use other pivot selection strategies.

### Key points:

- **Space complexity** is reduced to **O(log n)**, as it only uses a small amount of extra space for the recursive stack (since it's done in place).
- **Time complexity** remains **O(n log n)** on average, with a worst case of **O(n²)** if the pivot selection is poor.

### Conclusion:

For interviews, this **in-place** version is much more efficient and ideal to use because:

1. **Lower space complexity**: It doesn't create new arrays at each recursion.
2. **Optimal performance**: It's faster in terms of memory usage and is a more classic and expected implementation.

This is the type of solution that interviewers usually look for when asking about sorting algorithms.