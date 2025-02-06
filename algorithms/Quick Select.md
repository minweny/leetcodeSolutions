The Quickselect algorithm is an efficient way to find the *k*-th smallest element in an unordered list. It is related to the Quicksort algorithm, but it only partially sorts the list, making it more efficient when you're only interested in the *k*-th smallest element.

Here's how Quickselect works:

1. **Choose a pivot**: Similar to Quicksort, pick a pivot element from the list.
2. **Partition the list**: Rearrange the elements such that all elements smaller than the pivot are to the left, and all elements greater than the pivot are to the right. This step is identical to what happens in the Quicksort partition step.
3. **Recurse**:
   - If the pivot is the *k*-th smallest element, return it.
   - If the pivot's position is greater than *k*, recurse into the left side (the portion of the list less than the pivot).
   - If the pivot's position is less than *k*, recurse into the right side (the portion of the list greater than the pivot).

The time complexity on average is **O(n)**, though in the worst case, it could be **O(n²)** if a bad pivot is chosen repeatedly (like in Quicksort).

Here’s a simple Python implementation of the Quickselect algorithm:

```python
def quickselect(arr, left, right, k):
    """
    Select the k-th smallest element in the unordered list arr.
    :param arr: The input array.
    :param left: The left index of the array.
    :param right: The right index of the array.
    :param k: The index of the k-th smallest element.
    :return: The k-th smallest element.
    """
    if left == right:
        return arr[left]
    
    pivot_index = partition(arr, left, right)
    
    if k == pivot_index:
        return arr[k]
    elif k < pivot_index:
        return quickselect(arr, left, pivot_index - 1, k)
    else:
        return quickselect(arr, pivot_index + 1, right, k)

def partition(arr, left, right):
    """
    Partition the array around a pivot.
    :param arr: The input array.
    :param left: The left index of the array.
    :param right: The right index of the array.
    :return: The pivot index after partitioning.
    """
    pivot = arr[right]
    i = left - 1
    for j in range(left, right):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    
    arr[i + 1], arr[right] = arr[right], arr[i + 1]
    return i + 1

# Example usage:
arr = [3, 2, 1, 5, 4, 6]
k = 3  # Looking for the 3rd smallest element
result = quickselect(arr, 0, len(arr) - 1, k - 1)  # Adjusted index for 0-based indexing
print(f"The {k}th smallest element is: {result}")
```

### Explanation:
1. `quickselect(arr, left, right, k)` is the main function, which calls the `partition` function and recursively narrows down the search space.
2. `partition(arr, left, right)` rearranges the elements around a pivot and returns the index of the pivot after partitioning.
3. The recursion continues until the pivot is the *k*-th element in the array.

Let me know if you need further clarifications!