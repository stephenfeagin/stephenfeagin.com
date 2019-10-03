---
title: "Selection Sort: C"
author: ""
type: ""
date: 2019-10-03T10:20:17-04:00
subtitle: ""
image: ""
tags: [learning, algorithms, C]
draft: true
---

Next up in my ["learning in public" push](/2019/09/learning-and-working-in-public) is 
[selection sort](https://en.wikipedia.org/wiki/Selection_sort), and an implementation in C. Like 
[insertion sort](/2019/09/insertion-sort-c), selection sort sorts
the array in place, starting with a sorted beginning portion and an unsorted end. We iterate through
the unsorted portion, and find the smallest value. We then swap that element with the first element
in the unsorted portion. From there, the unsorted portion begins one index later, and we repeat the
process until the entire array is sorted.

## Pseudocode

```
A = Array(...)
N = A.length
for i from 0 to N - 1:  // We can do N-1 because a one-element array is sorted by definition
    minValueIndex = i  // index of the smallest element we've seen so far
    for j from i+1 to N:
        if array[j] < array[minValueIndex]:
            minValueIndex = j
    swap(A, i, j)  // In array A, swap the values at indices i and j
```

### Example

- Start with `A = [2 1 4 3]`
- The entire array is unsorted at this point
- The sorted portion has 0 elements, the unsorted portion has 4 elements
- The first index of the unsorted portion is 0
- Search through the unsorted portion for its smallest value
  - At `i=0`, 2 is the smallest value
  - At `i=1`, `1 < 2` so 1 is the smallest value
  - At `i=2`, `1 < 4` so 1 is still the smallest value
  - At `i=3`, `1 < 3` so 1 is still the smallest value
- We then swap that smallest value with the element at the first index of the unsorted portion
(`i=0`, which is 2)
- After one iteration, we now have `[1 2 4 3]`
- The sorted portion has one element, index 0, and the unsorted portion has 3 elements
- The first index of the unsorted portion is `i=1`
- We repeat our search through the unsorted portion, and find that the first value, 2, is the
smallest element
- At this point, we can either swap it with itself or check whether the first element is the
smallest, and if so, just move on
- We still have `[1 2 4 3]`
- The array hasn't changed, but the starting index of the unsorted portion is now `i=2`
- Third iteration: we start at `i=2`, find that the smallest value in the unsorted portion is 3, and
swap that with the value at `i=2`
- We now have `[1 2 3 4]`
- The length of the unosrted portion is now 1, containing only index `i=3`, so is sorted by
definition

## Efficiency

- **Worst-case**
  - *O(n<sup>2</sup>)*
- **Best-case**
  - *&Omega;(n<sup>2</sup>)*

In both cases, selecting the minimum value requires scanning all of the unsorted elements (let's
call that *N'*), which requires *N' - 1* comparisons. In each iteration, the length of the unsorted
portion decreases by one. This can be written as:

<div>
\[(n-1) + (n - 2) \ldots + 1 = \sum_{i=1}^{n-1}i\]
</div>

This series can be re-written as:[^1]

[^1]: The sum of an arithmetic series can be found by multiplying the number of terms in the series (in this case, *n-1* because we need to iterate through the array *n-1* times) by the sum of the first term and the last term and dividing by 2. See [arithmetic progression](https://en.wikipedia.org/wiki/Arithmetic_progression). Another win for learning in public, because I had definitely forgotten how to solve arithmetic series.

<div>
\[\sum_{i=1}^{n-1}i = (n - 1)\frac{(n - 1) + 1}{2} = \frac{1}{2}(n^2 - n)\]
</div>

The *n<sup>2</sup>* term means that the efficiency is *O(n<sup>2</sup>)*, regardless of initial
ordering.

## Implementation

`selectionSort()` takes two parameters: an integer `n`, which is the length of the array, and the
integer array itself.

```c
void selectionSort(int n, int arr[])
{
    // Iterate from the beginning of the unsorted portion through n
    for (int i = 0; i < n-1; i++)
    {
        // Find the smallest value and its index in the unsorted portion
        int minIndex = i;  // the index of the minimum value, not the minimum index
        int minVal = arr[minIndex];
        for (int j = i+1; j < n; j++)
        {
            if (arr[j] < minVal)
            {
                minIndex = j;
                minVal = arr[j];
            }
        }

        // Copy the first unsorted value
        int elementI = arr[i];

        // Re-assign arr[i] to be minValue, and arr[minIndex] to be elementI
        arr[i] = minVal;
        arr[minIndex] = elementI;
    }
}
```


<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

