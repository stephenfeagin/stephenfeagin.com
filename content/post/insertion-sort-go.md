---
title: "Insertion Sort: Go"
author: ""
type: ""
date: 2019-10-11T10:39:44-04:00
subtitle: ""
image: ""
tags: [learning, algorithms, go]
---

This post shows an implementation of insertion sort written in Go. Insertion sort builds a sorted
array at the beginning of the original array, iterating through the unsorted portion to add another
element to the sorted portion with each pass. For a more detailed walkthrough, see my
[original post](/insertion-sort-c) with an implementation in C.

```go
func insertionSort(arr []int) {
    arrLen := len(arr)
    for i := 1; i < arrLen; i++ {
        key := arr[i]
        j := i - 1
        for j >= 0 && arr[j] > key {
            arr[j+1] = arr[j]
            j--
        }
        arr[j+1] = key
    }
}
```
