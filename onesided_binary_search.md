```java
int oneSidedBinarySearch(int numbers[], int key) {
    int index = 0, exp = 0;
    while (true) {
        try {
            if (numbers[index] == key) {
                return index;
            } else if (numbers[index] < key) {
                index = (int) Math.pow(2, exp);
                exp++;
            } else {
                break;
            }
        } catch(Exception e) {
            break;
        }
    }
    
    int low = index/2 - 1;
    int high = index - 1;
    
    while (low <= high) {
        try {
            int mid = (low + high)/2;
            if (numbers[mid] == key) {
                return mid;
            }

            if (numbers[mid] < key) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        } catch(Exception e) {
            high = index - 1;
        }
    }

    return -1;
}
```
