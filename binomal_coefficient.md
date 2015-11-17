Binomial Coefficient
====================

NOTES:

```
public static long binomialCoefficient(int n, int k) {
    int max = (n+1);
    long table[][] = new long[max][max];
    //initialize the table
    for (int i=0; i<=n; i++) table[i][0]=1;
    for (int j=1; j<=n; j++) table[j][j]=1;
    for (int i = 1; i<=n; i++)
        for(int j=1; j < i; j++)
            table[i][j] = table[i - 1][j-1] + table[i - 1][j];
    return table[n][k];
}
```