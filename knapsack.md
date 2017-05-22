```java
int knapsack(int values[], int weights[], int n, int capacity) {
    int m[][] = new int[100][100];
    
    for (int i = 0; i < values.length; i++) {
        m[0][i] = 0;
    }
    
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j <= capacity; j++) {
            if (weights[i -  1] <= j) {
                m[i][j] = Math.max(m[i-1][j],values[i-1]+m[i-1][j-weights[i-1]]);
            } else {
                m[i][j] = m[i - 1][j];
            }
        }
    }
    
    return m[n][capacity];
}
```