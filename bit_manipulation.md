Bit Manipulation
==========
```
function isPowerOfTwoBit(x) {
	return (x != 0 && (x & (x - 1)) == 0);
}
function isPowerOfTwo(x) {
	if (x == 0) return false;
	while (x % 2 == 0) x /=2;
	return x == 1;
}
function countOnes(x) {
	var count = 0;
	while (x !== 0) {
		x = x & (x - 1);
		count++;
	}
	return count;
}
function subsets(n) {
	var total = n.length;
	var possibility = 1 << total;
	var ans = [];
	for (var k = 0; k < possibility; k++) ans[k] = '';
	for (var i = 0 ; i < possibility; i++) 
		for (var j = 0; j < total; j++)
			if ((i & (1 << j) ) !== 0)
				ans[i] += (n[j]);
	return ans;
}
```



