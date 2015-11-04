Min Heap Algorithm
========================

Implementations:
[MINHEAP]
```
class MinHeap {
    int[] heap;
    int maxSize;
    int parent(int position) { return position / 2; }
    int left(int position) { return position * 2; }
    int right(int position) { return position * 2 + 1}
    boolean isLeaf(int position) {
        return (position >= heap.length/2 && position <= heap.length)
    }
}
```
[/MINHEAP]
