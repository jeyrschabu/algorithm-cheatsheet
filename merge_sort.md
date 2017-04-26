Merge Algorithm
========================

Implementations:

```java
void mergesort(int [] numbers, int low, int high) {
    if (low < high) {
        int middle = (low + high)/2;
        mergesort(numbers, low, middle);
        mergesort(numbers, middle + 1, high);
        merge(numbers, low, middle, high);
    }
}

void merge(int [] numbers, int low, int middle, int high) {
    int [] helper = new int[numbers.length];
    // Copy both parts into the helper array
    for (int i = low; i <= high; i++) {
      helper[i] = numbers[i];
    }
    
    int i = low;
    int j = middle + 1;
    int k = low;
    // Copy the smallest values from either the left or the right side back
    // to the original array
    while (i <= middle && j <= high) {
      if (helper[i] <= helper[j]) {
        numbers[k] = helper[i];
        i++;
      } else {
        numbers[k] = helper[j];
        j++;
      }
      k++;
    }
    // Copy the rest of the left side of the array into the target array
    while (i <= middle) {
      numbers[k] = helper[i];
      k++;
      i++;
    }
  }
```