Min Heap Algorithm
========================

Implementations:
[MINHEAP]
```
class MinHeap {
    int[] heap;
    int maxSize;
    int counter = 0;
    static final int FRONT = 1; 
    MinHeap(int maxSize) {
        this.maxSize = maxSize;
        heap = new heap[maxSize + 1];
        heap[0] = Integer.MIN_VALUE;
    }
    int parent(int position) { return position / 2; }
    int left(int position) { return position * 2; }
    int right(int position) { return position * 2 + 1}
    boolean isLeaf(int position) {
        return (position >= counter/2 && position <= counter)
    }
    void insert(int element) {
        heap[++counter] = element;
        int i = counter;
        while (heap[i] < heap[parent(i)]) {
            swap(i, parent(i));
            current = parent(current);
        }
    }
    int remove() {
        int popped = heap[FRONT];
        heap[FRONT] = heap[counter--];
        minify(FRONT);
        return popped;
    }
    void minify(int position) {
        if (!isLeaf(pos)) {
            if (heap[pos]) > heap[left(pos)] || heap[pos] < heap[right(pos)]) { 
                if (heap[left(pos)] < heap[right(pos)]) {
                    swap(pos, left(pos));
                    minify(left(pos));
                } else {
                    swap(pos, right(pos));
                    minify(right(pos));
                }
            }
        }
    }
}
```
[/MINHEAP]
