QuickSort Algorithm
========================

Implementations:

```java
//O(n log n)
void quickSort(int a[], int left, int right) {
      int index = partition(a, left, right);
      if (left < index - 1) {
            quickSort(a, left, index - 1);
      }

      if (index < right) {
            quickSort(a, index, right);
      }
}

int partition(int numbers[], int left, int right) {
    int i = left, j = right;
    int tmp;
    int pivot = numbers[(left + right) / 2];
    while (i <= j) {
        while (numbers[i] < pivot) {
            i++;
        }

        while (numbers[j] > pivot) {
            j--;
        }

        if (i <= j) {
            tmp = numbers[i];
            arr[i] = numbers[j];
            arr[j] = tmp;
            i++;
            j--;
        }
    }

    return i;
}
```