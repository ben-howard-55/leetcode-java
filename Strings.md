# String Data Structures

## LeetCode Questions

### Reverse String

9-01-2021

#### constraints

~~~
Write a function that reverses a string. The input string is given as an array of characters char[].

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
~~~

#### Code Solution

```Java
class Solution {
	public void reverseString(char[] s) {
        int length = s.length;
        
        if (length > 1) {
            char temp;
            int l = length-1;
        
            for (int i = 0; i < length/2; i++) {
                temp = s[i];
                s[i] = s[l-i];
                s[l-i] = temp;
            }
        }
    }
}
```

####  Explanation of Solution

Just a simple solution that is self explanatory.

---

### Reverse Integer

09-01-2021

#### Contraints

```
Given a 32-bit signed integer, reverse digits of an integer.
Note: Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For this problem, assume that your function returns 0 when the reversed integer overflows.
```

#### Code Solution

```java
class Solution {
		public int reverse(int x) {
        int rev = 0;
        int pop;
        while (x != 0) {
            pop = x % 10;
            x /= 10;
            if (rev > Integer.MAX_VALUE/10 || 
                (rev == Integer.MAX_VALUE / 10 && pop > 7)) return 0;
            if (rev < Integer.MIN_VALUE/10 || 
                (rev == Integer.MIN_VALUE/10 && pop < -8)) return 0;
            
            rev = rev * 10 + pop;
        }
        return rev;
    }
```

#### Explanation of Solution

The `pop` is finding the last digit of the int `x`. And then `1` is divided by 10, truncating `x` and returning x with 1 less digit. Checks are then in place to check if the adding of the pop value to the `rev` would make the number larger than the largest possible int.

If not then the current `rev` is multiplied by 10 and pop is added to it. Repeat until `x` is 0.

---

### Find First Unique Character

10-01-2021

#### Constraints

```
Given a string, find the first non-repeating character in it and return its index. If it doesn't exist, return -1.
```

#### Code Solution

```java
class Solution {
    public int firstUniqChar(String s) {
        int length = s.length();
        
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        
        char ch;
        for (int i = 0; i < length; i++) {
            ch = s.charAt(i);
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }
        
        for (int i = 0; i < length; i++) {
            if (map.get(s.charAt(i)) == 1) return i;
        }
        
        return -1;
    }
}
```

#### Explanation of Solution

Run through the String and grab each `charAt(i);`, add it to the HashMap as the Key and  as default place 0 as the value and add 1. If a value already exists as the key, then add 1 to the current value. This is the functionality of `map.getOrDefault(ch, 0) + 1;`. 

Then each char in the string must be looked at in the map to see if a char key has a value of only 1. If so `return i;`. Else `return -1;` 

---

### Implement Strstr

16-01-2021

#### constraints

~~~
Write an efficient algorithm to implement strstr function in Java which returns the index of first occurrence of a string in another string.
~~~

#### Code Solution

```Java
class Solution {
    public int strStr(String haystack, String needle) {
        int n = needle.length();
        int h = haystack.length();
        
        if (n == 0) return 0;
        
        if (needle.equals(haystack)) return 0;
        
        if (n > h) return -1;
        
        for (int i = 0; i < h - n + 1; i++) {
            for (int j = 0; j < n; j++) {
                if (needle.charAt(j) != haystack.charAt(i+j)) {
                    break;
                } 
                if (n-1 == j) {
                    return i;
                }
            }
        } 
    		return -1;
    }
}
```

####  Explanation of Solution

The initial checks are just for outliers that could occur. The rest is quite simple:

Simply iterate through the haystack string and check if the char is the same as the char at the first index of the needle. If not break and check the next. 

Else check if the last index of the needle is the char selected and if so return the index.

Keep iterating until either the inner for loop breaks or it `returns i`.

Move on to the next char in the haystack. `return -1` if no match found.

---



