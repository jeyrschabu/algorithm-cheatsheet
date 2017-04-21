Strings
==========

// determine if s2 is a rotation of s1 using a call to "isSubString(String s1, String s2)  

```java
boolean isRotation(String s1, String s2) {
	if (s1 == null || s2 == null || s1.length() == 0 || s2.length() == 0) return false;
	if (s1.length() == s2.length()) {
	    return isSubString(s1+s1, s2);
	}
	return false;
}
```



