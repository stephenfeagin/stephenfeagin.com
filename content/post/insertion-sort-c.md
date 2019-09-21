---
title: "Insertion Sort: C"
author: ""
type: ""
date: 2019-09-21T15:17:11-04:00
subtitle: ""
image: ""
tags: [learning, algorithms, C]
draft: false
---

In my first post in my ["learning in public" push](/2019/09/learning-and-working-in-public), I'm
going to be talking about the insertion sort algorithm and an implemention in C. The general idea of
insertion sort is to build a sorted array in place, at the beginning of the original array, shifting
the unsorted elements toward the end of the array as necessary. It relies on the fact that an array
of length 1 is sorted by definition.

I'm going to show and walk through some pseudocode, touch on the efficiency of the algorithm, and
then show an implementation in C.

## Pseudocode

NB: I use zero-indexed arrays and half-open array slicing in this pseudocode.

```
A = Array(...)
N = A.length
for i from 1 to N:
    A[0:i] is sorted
    key = array[i]
    j = i - 1  // index of last element in the sorted portion
    while j >= 0 and A[j] > key:
        A[j + 1] = A[j]
        j = j - 1
    A[j + 1] = key
```

### Example

- Start with `A = [3 1 2]`
- First iteration: `i = 1`
  - `A[0:i] --> A[0:1] --> [3]` is sorted by definition
  - `key = A[i] --> A[1] --> 1`
  - `j = i - 1 --> 0`
  - Loop condition: `0 >= 0 and 3 > 1 --> TRUE`
    - `A[j + 1] = A[j] --> A[1] = 3, A = [3 3 2]`
    - `j = j - 1 --> -1`
  - Loop condition: `FALSE` (`j < 0`)
  - `A[j + 1] = key --> A[0] = 1, A = [1 3 2]`
- `A = [1 3 2]`
- Second iteration: `i = 2`
  - `A[0:i] --> A[0:2] --> [1 3]` is already sorted
  - `key = A[i] --> A[2] --> 2`
  - `j = i - 1 --> 1`
  - Loop condition: `1 >= 0 and 3 > 2 --> TRUE`
    - `A[j + 1] = A[j] --> A[2] = 3, A = [1 3 3]`
    - `j = j - 1 -- > 0`
  - Loop condition: `FALSE` (`!(1 > 2)`)
  - `A[j + 1] = key --> A[1] = 2, A = [1 2 3]`
- `A = [1 2 3]`
- `i == N` so no third iteration

## Efficiency

- **Worst-case**
  - Array is reverse sorted
  - *O(n<sup>2</sup>)*
- **Best-case**
  - Array is already sorted
  - *&Omega;(n)*

## Implementation

`insertionSort()` takes as input an integer, `n`, the length of the array, and an array of integers,
`arr`. It sorts the array in place, so it doesn't return anything.

{{< highlight c >}}
void insertionSort(int n, int arr[])
{
    for (int i = 1; i < n; i++)
    {
        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
{{< /highlight >}}
