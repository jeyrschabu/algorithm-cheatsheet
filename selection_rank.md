Selection Rank Algorithm
========================
- Application:
    - find the ith largest or smallest numbers
NOTES:
1. pick a random element in the array and use it as a pivot. Partition elements around pivot while keeping track of 
the number of elements on each side. (elements on left are smaller and elements on right are larger) 
2. if there is exactly i elements on the left, then you just return the biggest element on the left
3. if the left side is bigger than i, repeat the algorithm on the left side of the array
4. if the left side is smaller than i, repeat the algorithm on the right


Implementations:

[RANK]

```
// O(n)
int rank(int[] array, int left, int right, int rank) {
    int random = random(left, right);
    int pivot = array[random];
    int leftEnd = partition(array, left, right, pivot); //partition
    int leftSize = leftEnd - left + 1;
    if (leftSize == rank + 1) return Math.max(array[left], array[leftEnd]);
    else if (rank < leftSide) return rank(array, left, leftEnd, rank);
    else return rank(array, leftEnd + 1, right, rank - leftSize);
}
```
[/RANK]

[PARTITION]
```
int partition(int[] array, int left, int right, int pivot) {
    while (true) {
        while (left <= right && array[left] <= pivot) left++;
        while (left <= right && array[right] > pivot) right--;
        if (left > right) return left -1;
        swap(array, left, right)
    }
}
```
[/PARTITION]