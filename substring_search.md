```java

    /**
     * Worst Case: O(m*n)
     * Uses back up everytime there is a mismatch
     */

    int substringSearchBruteForce(String pattern, String txt) {
        int m = pattern.length();
        int n = txt.length();
        
        for (int i= 0; i <= n - m; i++) {
            int j;
            for (j = 0; j < m; j++) {
                if (txt.charAt(i+j) != pattern.charAt(j)) {
                    break;
                }
            }

            if (j == m) {
                return i;
            }
        }

        return n;
    }

    int substringSearch(String pattern, String txt) {
        int i,m = pattern.length();
        int j,n = txt.length();
        
        for (i= 0, j=0 ; i < n && j < m; i++) {
            if (txt.charAt(i) == pattern.charAt(j)) {
                j++;
            } else {//backup
                i-=j;
                j=0;
            }
        }

        if (j == m) {
            return i -m ;
        }

        return n;
    }
```