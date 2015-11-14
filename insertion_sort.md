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
void insertionSort(int [] numbers) {
    for(int i = 1; i < numbers.length; i++) {
        int val = numbers[i];
        int j = i - 1;
        while(j >= 0 && numbers[j] > val){
            numbers[j + 1] = numbers[j];
            j--;
        }
        numbers[j + 1] = val;
    }
}
```
[/INSERTIONSORT]