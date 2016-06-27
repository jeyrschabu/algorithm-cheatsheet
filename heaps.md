Heap Algorithms
========================
[MAXHEAP]
```
void maxHeapify(int arr, int i, int size) {
    int leftIndex = 2 * i;
    int rightIndex = 2 * i + 1;
    int largestIndex = i;
    if (leftIndex < size && arr[leftIndex] > arr[i])
        largestIndex = leftIndex;
    if (rightIndex < size && arr[rightIndex] > arr[i])
        largestIndex = rightIndex;
    if (largestIndex != i) {
        swap(arr[i], arr[largestIndex]);
        maxHeapify(arr, largestIndex, size);
    }
}
void swap(int i, int j, int arr[]) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
void buildMaxHeap(int [] arr) {
    for (int i = arr.length/2; i > 0; i--) 
        maxHeapify(arr, i, arr.length);
}
```
[/MAXHEAP]

[MINHEAP]
```
void minHeapify(int arr[], int i, int size) {
    int leftIndex = 2 * i;
    int rightIndex = 2 * i + 1;
    int smallestIndex = i;
    if (leftIndex < size && arr[leftIndex] < arr[i])
        smallestIndex = leftIndex;
    if (rightIndex < size && arr[rightIndex] < arr[i])
        smallestIndex = rightIndex;
    if (largest != i) {
        swap(arr[i], arr[smallestIndex]);
        minHeapify(arr, smallestIndex, size);
    }
}
void buildMinHeap(int [] arr) {
    for (int i = arr.length/2; i >0; i--) 
        maxHeapify(arr, i, arr.length);
}
```
[/MINHEAP]

[HEAPSORT]
O(nlgn)
```
void heapSort(int arr[]) {
    int size = arr.length;
    buildMaxHeap(arr);
    for (int i = arr.length - 1; i >= 1; i--){
        swap(0, i, arr);
        maxHeapify(arr, 0, size--);
    }
}
```
[/HEAPSORT]

We can construct a priority queue using a heap

```
int max(int arr[]) {
    return arr[0]; //largest element in a max priority queue
}
int extractMax(int arr[]) { //O(logN)
    int max = arr[0];
    arr[0] = arr[arr.length - 1];
    maxHeapify(arr, 0, arr.length);
    return max;
}
int findKthLargestNumber(int [] arr, int k) {
    buildMaxHeap(arr);
    for (int i = 0; i < k; i++) {
        extractMax(arr); 
    }
    return max(arr);
}
```

