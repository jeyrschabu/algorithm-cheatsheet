Insertion Algorithm
========================

Implementations:

[INSERTIONSORT]

```
//Stable
//O(1) extra space
//O(n2) comparisons and swaps
//Adaptive: O(n) time when nearly sorted
//Very low overhead
for i = 2:n,
    for (k = i; k > 1 and a[k] < a[k-1]; k--) 
        swap a[k,k-1]
    → invariant: a[1..i] is sorted
end
```
[/INSERTIONSORT]