# Array Data Structure

## Leet Code Questions

---

[TOC]



#### Remove Duplicates from Sorted Array

20-11-2020

###### constraints
~~~
Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length. 

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
~~~
###### Code Solution
```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int c = 0;
        for (int j = 1; i < nums.length; j++) {
            if (nums[j] != nums[c]) {
                c++;
                nums[c] = nums[j];
            } 
        }
    return c + 1;
    }
}
```
######  Explanation of Solution
__I felt as if this question wasn't very well explained.__
However, the problem requires a fast runner and slow runner. The slow runner only changes index when the current index `nums[c]` is not equal to the faster runner index `nums[j]`.

---

#### Best Time to Sell and Buy Stock II	

20-11-2020

###### constraints

```
say you have an array prices for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
```

###### Code Solution

```Java
class Solution {
    public int maxProfit(int[] prices) {
        // return 0 profit if only 1 day
        if (prices.length == 1) return 0;
        // initial profit and price
        int profit = 0;
        int price = -1;
        
        for (int i = 0; i < prices.length-1; i++) {
            // buy, only if todays price is less than the tomorrows
            if (price == -1) {
                if (prices[i] < prices[i+1]) {
                    price = prices[i];
                }
            } else { //sell, if the tomorrows price is less and the buying 												price is less than the selling price.
                if (prices[i] > prices[i+1] && prices[i] >= price) {
                    profit = profit + (prices[i]-price);
                    price = -1;
                }
            }
        }
        // check on the last day to sell.
        if (prices[prices.length-1] >= price && price != -1) {
            profit = profit + (prices[prices.length-1]-price);
            }
        return profit;
    }
}
```

###### Explanation of Solution

It boils down to breaking down the process into two steps; 1 buy, and 2 sell.

1. Buy - Only buy if todays price is worth less than tomorrows price
2. Sell - Only sell if tomorrows price is less and the buying price is less than the selling price.

On the last day it is also important to sell the stock if it can be sold for more than it was bought for.

---

#### Rotate Array

21-11-2020

###### Constraints

```
Given an array, rotate the array to the right by k steps, where k is non-negative. In-place with O(1) memory.
```

###### Code Solutions

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int length = nums.length;
        if (k >= length) {
            k = k % length;
        }
        
        int temp;
        for (int i = 0; i < k; i++) {
            for (int j = 0; j < length; j++) {
               temp = nums[length-1];
               nums[length-1] = nums[j];
               nums[j] = temp;
            }
        }
    }
}
```

###### Explanation of Solution

simply swap the elements from the end of the array to the index position, do this for the entire array length and then the array will be fully rotated. Do this k times, and the problem is solved.

*To reduce the amount of iterations needed, get the remainder of k by the length, if k >= length. This reduces unneeded iterations.*

**I initially ran into a time problem, this is due to not instantiating a length var**

---

#### Contains Duplicates

22-11-2020

###### constraints

```
Find a duplicate in an array of integers. If one or more duplicates exist, return true. If all elements are distinct return false.
```

###### Code Solutions

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        int length = nums.length;
        int temp;
        for (int i = 0; i < length-1; i++) {
            temp = nums[i];
            for (int j = i+1; j < length; j++) {
                if (temp == nums[j]) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

###### Explanation of Solution

**This naive linear search, is generally not what is wanted as is too slow.**

*Instead, you could do one of two things:*

###### Solution using Sort

1. Using some a merge algorithm, such as merge sort.
$$
   O(n\log(n))
$$

   ```java
   // first sort array using Arrays.sort()
   Arrays.sort(nums);
   // then look for two consecutive integers
   for (int i = 0; i < nums.length-1; i++) {
     if (nums[i] == nums[i+1]) return true;
   }
   return false;
   ```

###### Solution using HashMap

2. Using a HashSet.
   $$
   O(n)
   $$

   ```java
   // create the hash set
   Set<Integer> set = new HashSet<>(nums.length);
   	for (int x: nums) {
       // if the set already contains then a duplicate exists return true
   		if (set.contains(x)) return true;
       	// add element to the set
   			set.add(x);
   		}
      return false;
   ```

---

#### Single Number

23-11-2020

```
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one. Implement a solution with a linear runtime complexity.
```

###### Code Solution

$$
O(n+n)=O(n)
$$

```java
class Solution {
    public int singleNumber(int[] nums) {
    // hash map that takes an integer key and integer value.
    HashMap<Integer, Integer> hashTable = new HashMap<>();
        
      	// iterate through the entie array O(n)
        for (int x : nums) {
          	// if integer is not in the hashmap then add the value as 1,
          	// else get the current value and add 1.
            hashTable.put(x, hashTable.getorDefault(x, 0) + 1);
        }
      
      	// iterate through the entire array O(n)
        for (int x : nums) {
          	// if the key returns the value 1, then return the key.
            if (hashTable.get(x) == 1) {
                return x;
            }
        }
        return 0;
    }
}
```

###### Explanation of Solution 

###### Solution using HashMap

Using a HashMap allows for constant time operations of `put()`, `getorDefault()`, and `get()`. Meaning two iterations through the array, gives you a linear time operation.

###### Solution Using Math

$$
2\times (a+b+c) - (a+a+b+b+c)=c
$$

Go through each element and find each unique one, times the sum by 2.

Then remove original array from the sum. What is left is the solution.

###### Solution Using Bit Manipulation

- If we take XOR of zero and some bit, it will return that bit

  `a^0=a` > a ⊕ 0 = a

- If we take XOR of two same bits, it will return 0

  `a^a=0` a ⊕ a = 0

- XOR is a commutative and assosciative

  a ⊕ b ⊕ a = (a ⊕ a) ⊕ b = 0 ⊕ b = b

So we can XOR all bits together to find the unique number.

```java
int a = 0;
for (int x: nums) {
  a ^= x;
}
return a;
```

#### Intersection of Two Arrays II

###### Constraints

Given two arrays, find the intersection of the two. The order does not matter and an element should appear how every many times they appear in both arrays.

###### Code Solution

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> hashMap = new HashMap<>();
        List<Integer> list = new ArrayList<Integer>();
        
        for (int x: nums1) {
            hashMap.put(x, hashMap.getOrDefault(x, 0) + 1);
        }
        
        for (int x : nums2) {
            if (hashMap.containsKey(x) && hashMap.get(x) > 0) {
                list.add(x);
                hashMap.put(x, hashMap.get(x) - 1);
            }
        }
        
        return listToArray(list);
    }
    
    private int[] listToArray(List<Integer> list) {
        int[] array = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            array[i] = list.get(i);
        }
        return array;
    }
}
```

###### Explanation Of Solution (HashMap)

First HashMap uses the int as a key to point to the value of number of times appeared. Each time the same element is in the second array, it subtracts one from the value and adds the key value to the list. Then the list is changed to an array and then returned.

#### Plus One

25-11-2020

###### Constraints

```
Given a non-empty array of decimal digits representing a non-negative integer, increment one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contains a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.
```

###### Code Solution

```java
class Solution {
    public int[] plusOne(int[] digits) {
       
        int carry = 1;
        for (int i = digits.length-1; i >= 0; i--) {
            if (digits[i] == 9) {
                digits[i] = 0;
                carry = 1;
            } else {
                digits[i] += carry;
                carry = 0;
                break;
            }
        }
        
        if (carry == 1) {
        int[] temp = new int[digits.length+1];
            temp[0] = 1;
            return temp;
        }
        return digits;
    }
 }
```

###### Explanation of Solution

Not the most elegant solution. However, the problem should be broken down into its components.

####

#### Two Sum

28-11-2020

###### Constraints

```
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.
```

###### Code Solution

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
      
        int complement;
        for (int i = 0; i < nums.length; i++) {
            complement = target - nums[i];
            if (map.containsKey(complement) {
                return new int[] { map.get(complement, i) };
                map.put(nums[i], i);
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```

###### Explanation of Solution

Due to the fact that the order does not matter, it can be done in one pass. For each element find its complement and check to see if the elements complement already exists inside of the hash map. Return if it does.





