# Linear Search
```go
// LinearSearch performs a linear search for the target value in the slice.
// If the target value is found, the function returns the index at which the target value is found.
// If the target value is not found, the function returns -1.
func LinearSearch(slice []int, target int) int {
    for i, v := range slice {
        if v == target {
            return i
        }
    }
    return -1
}
```

# Sentinel Linear Search
```go
// SentinelLinearSearch performs a linear search for the target value in the slice using a sentinel loop.
// If the target value is found, the function returns the index at which the target value is found.
// If the target value is not found, the function returns -1.
func SentinelLinearSearch(slice []int, target int) int {
    n := len(slice)
    last := slice[n-1]
    slice[n-1] = target

    i := 0
    for slice[i] != target {
        i++
    }

    slice[n-1] = last
    if i < n-1 || slice[n-1] == target {
        return i
    }
    return -1
}
```

# Binary Search
```go
// BinarySearch performs a binary search for the target value in the slice.
// The slice must be sorted in ascending order.
// If the target value is found, the function returns the index at which the target value is found.
// If the target value is not found, the function returns -1.
func BinarySearch(slice []int, target int) int {
    low := 0
    high := len(slice) - 1

    for low <= high {
        mid := low + (high-low)/2
        if slice[mid] == target {
            return mid
        } else if slice[mid] < target {
            low = mid + 1
        } else {
            high = mid - 1
        }
    }
    return -1
}
```
