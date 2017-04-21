Arrays
======

```java
void mergeSortedArrays(int[] a, int[] b, int lastA, int lastB) {
	int indexA = lastA -1;
	int indexB = lastB -1;
	int indexMerged = lastA - lastB -1;
	while (indexA >= 0 && indexB >= 0) {
		if (a[indexA] > b[indexB]) {
			a[indexMerged] = a[indexA];
			indexMerged--;
			indexA--;
		} else {
			a[indexMerged] = b[indexB];
			indexMerged--;
			indexB--;
		}
	}
	
	while (indexB >=0) {
		a[indexMerged] = b[indexB];
		indexMerged--;
		indexB--;
	}
}
```



