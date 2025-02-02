## Buy and Sell I stocks 

It looks like you're interested in a coding question related to buying and selling stocks in Java. Here's a more detailed example that includes a method to find the best time to buy and sell a stock to maximize profit. This is a common interview question.

```java
public class StockTrading {

    // Method to find the maximum profit
    public static int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for (int price : prices) {
            if (price < minPrice) {
                minPrice = price;
            } else if (price - minPrice > maxProfit) {
                maxProfit = price - minPrice;
            }
        }

        return maxProfit;
    }

    public static void main(String[] args) {
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Maximum profit: " + maxProfit(prices));
    }
}
```

### Explanation:
1. **maxProfit Method**: This method takes an array of stock prices where each element represents the price of the stock on a given day.
2. **minPrice**: Keeps track of the minimum price encountered so far.
3. **maxProfit**: Keeps track of the maximum profit that can be achieved.
4. **Loop**: Iterates through the prices array. For each price, it updates `minPrice` if the current price is lower. Otherwise, it calculates the profit by subtracting `minPrice` from the current price and updates `maxProfit` if the calculated profit is higher.

### Example:
For the input array `[7, 1, 5, 3, 6, 4]`, the maximum profit is `5` (buy at price `1` and sell at price `6`).

Feel free to ask if you have any questions or need further assistance!

## Buy and Sell II stocks 

Got it! The "Buy and Sell Stock II" problem typically involves finding the maximum profit you can achieve by making as many transactions as you like (i.e., buy one and sell one share of the stock multiple times). Here's a Java solution for this problem:

```java
public class StockTradingII {

    // Method to find the maximum profit with multiple transactions
    public static int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int maxProfit = 0;

        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                maxProfit += prices[i] - prices[i - 1];
            }
        }

        return maxProfit;
    }

    public static void main(String[] args) {
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Maximum profit: " + maxProfit(prices));
    }
}
```

### Explanation:
1. **maxProfit Method**: This method takes an array of stock prices where each element represents the price of the stock on a given day.
2. **Loop**: Iterates through the prices array starting from the second day. If the price on the current day is higher than the price on the previous day, it adds the difference to `maxProfit`.
3. **maxProfit**: Keeps track of the total profit that can be achieved by making multiple transactions.

### Example:
For the input array `[7, 1, 5, 3, 6, 4]`, the maximum profit is `7` (buy at price `1` and sell at price `5`, then buy at price `3` and sell at price `6`).

Feel free to ask if you have any questions or need further assistance!


## Buy and Sell III stocks 

The "Buy and Sell Stock III" problem involves finding the maximum profit you can achieve with at most two transactions. Here's a Java solution for this problem:

```java
public class StockTradingIII {

    // Method to find the maximum profit with at most two transactions
    public static int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int n = prices.length;
        int[] leftProfits = new int[n];  // Max profit if sold up to day i
        int[] rightProfits = new int[n]; // Max profit if bought from day i

        // Calculate leftProfits
        int minPrice = prices[0];
        for (int i = 1; i < n; i++) {
            leftProfits[i] = Math.max(leftProfits[i - 1], prices[i] - minPrice);
            minPrice = Math.min(minPrice, prices[i]);
        }

        // Calculate rightProfits
        int maxPrice = prices[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            rightProfits[i] = Math.max(rightProfits[i + 1], maxPrice - prices[i]);
            maxPrice = Math.max(maxPrice, prices[i]);
        }

        // Calculate the maximum profit by combining left and right profits
        int maxProfit = 0;
        for (int i = 0; i < n; i++) {
            maxProfit = Math.max(maxProfit, leftProfits[i] + rightProfits[i]);
        }

        return maxProfit;
    }

    public static void main(String[] args) {
        int[] prices = {3, 3, 5, 0, 0, 3, 1, 4};
        System maxProfit(prices));
    }
}
```

### Explanation:
1. **maxProfit Method**: This method takes an array of stock prices where each element represents the price of the stock on a given day.
2. **leftProfits**: An array where `leftProfits[i]` represents the maximum profit achievable by making one transaction up to day `i`.
3. **rightProfits**: An array where `rightProfits[i]` represents the maximum profit achievable by making one transaction from day `i` to the end.
4. **Loop**: The first loop calculates `leftProfits` by iterating from the start to the end of the prices array. The second loop calculates `rightProfits` by iterating from the end to the start of the prices array.
5. **Combining Profits**: The final loop combines the maximum profits from `leftProfits` and `rightProfits` to find the overall maximum profit with at most two transactions.

### Example:
For the input array `[3, 3, 5, 0, 0, 3, 1, 4]`, the maximum profit is `6` (buy at price `0` and sell at price `3`, then buy at price `1` and sell at price `4`).

Feel free to ask if you have any questions or need further assistance!

## Buy and Sell IV stocks 

The "Buy and Sell Stock IV" problem involves finding the maximum profit you can achieve with at most `k` transactions. Here's a Java solution for this problem:

```java
public class StockTradingIV {

    // Method to find the maximum profit with at most k transactions
    public static int maxProfit(int k, int[] prices) {
        if (prices == null || prices.length == 0 || k == 0) {
            return 0;
        }

        int n = prices.length;
        if (k >= n / 2) {
            // If k is large enough, it's the same as an unlimited number of transactions
            int maxProfit = 0;
            for (int i = 1; i < n; i++) {
                if (prices[i] > prices[i - 1]) {
                    maxProfit += prices[i] - prices[i - 1];
                }
            }
            return maxProfit;
        }

        int[][] dp = new int[k + 1][n];
        for (int i = 1; i <= k; i++) {
            int maxDiff = -prices[0];
            for (int j = 1; j < n; j++) {
                dp[i][j] = Math.max(dp[i][j - 1], prices[j] + maxDiff);
                maxDiff = Math.max(maxDiff, dp[i - 1][j] - prices[j]);
            }
        }

        return dp[k][n - 1];
    }

    public static void main(String[] args) {
        int k = 2;
        int[] prices = {3, 2, 6, 5, 0, 3};
        System.out.println("Maximum profit: " + maxProfit(k, prices));
    }
}
```

### Explanation:
1. **maxProfit Method**: This method takes an integer `k` (the maximum number of transactions) and an array of stock prices where each element represents the price of the stock on a given day.
2. **Edge Cases**: If the prices array is empty or `k` is 0, the maximum profit is 0.
3. **Unlimited Transactions**: If `k` is large enough (greater than or equal to half the number of days), it is equivalent to an unlimited number of transactions. In this case, the solution is similar to the "Buy and Sell Stock II" problem.
4. **Dynamic Programming**: The `dp` array is used to store the maximum profit for up to `k` transactions up to day `j`. The `maxDiff` variable keeps track of the maximum difference between the profit of the previous transaction and the current price.

### Example:
For the input `k = 2` and prices `[3, 2, 6, 5, 0, 3]`, the maximum profit is `7` (buy at price `2` and sell at price `6`, then buy at price `0` and sell at price `3`).

Feel free to ask if you have any questions or need further assistance!

## Find Duplicate in Array in Java

Sure! Finding duplicates in an array is a common problem. Here's a simple Java solution to find duplicates in an array using a `HashSet`:

```java
import java.util.HashSet;
import java.util.Set;

public class FindDuplicates {

    // Method to find duplicates in an array
    public static Set<Integer> findDuplicates(int[] nums) {
        Set<Integer> duplicates = new HashSet<>();
        Set<Integer> seen = new HashSet<>();

        for (int num : nums) {
            if (!seen.add(num)) {
                duplicates.add(num);
            }
        }

        return duplicates;
    }

    public static void main(String[] args) {
        int[] nums = {4, 3, 2, 7, 8, 2, 3, 1};
        Set<Integer> duplicates = findDuplicates(nums);
        System.out.println("Duplicates: " + duplicates);
    }
}
```

### Explanation:
1. **findDuplicates Method**: This method takes an array of integers and returns a set of duplicates.
2. **Sets**: Two sets are used: `seen` to keep track of numbers that have been encountered, and `duplicates` to store numbers that appear more than once.
3. **Loop**: Iterates through the array. If a number is already in the `seen` set, it is added to the `duplicates` set. Otherwise, it is added to the `seen` set.

### Example:
For the input array `[4, 3, 2, 7, 8, 2, 3, 1]`, the output will be `Duplicates: [2, 3]`.

Feel free to ask if you have any questions or need further assistance!

## Intersection and Union of arrays in java

Sure! Here are Java methods to find the intersection and union of two arrays.

### Intersection of Two Arrays
The intersection of two arrays contains only the elements that are present in both arrays.

```java
import java.util.HashSet;
import java.util.Set;

public class ArrayOperations {

    // Method to find the intersection of two arrays
    public static Set<Integer> intersection(int[] nums1, int[] nums2) {
        Set<Integer> set1 = new HashSet<>();
        Set<Integer> intersection = new HashSet<>();

        for (int num : nums1) {
            set1.add(num);
        }

        for (int num : nums2) {
            if (set1.contains(num)) {
                intersection.add(num);
            }
        }

        return intersection;
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 2, 1};
        int[] nums2 = {2, 2};
        Set<Integer> intersection = intersection(nums1, nums2);
        System.out.println("Intersection: " + intersection);
    }
}
```

### Union of Two Arrays
The union of two arrays contains all the unique elements from both arrays.

```java
import java.util.HashSet;
import java.util.Set;

public class ArrayOperations {

    // Method to find the union of two arrays
    public static Set<Integer> union(int[] nums1, int[] nums2) {
        Set<Integer> union = new HashSet<>();

        for (int num : nums1) {
            union.add(num);
        }

        for (int num : nums2) {
            union.add(num);
        }

        return union;
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 2, 1};
        int[] nums2 = {2, 3};
        Set<Integer> union = union(nums1, nums2);
        System.out.println("Union: " + union);
    }
}
```

### Explanation:
1. **Intersection Method**:
   - **Sets**: Use a `HashSet` to store elements of the first array and another `HashSet` to store the intersection.
   - **Loop**: Add elements of the first array to `set1`. Then, for each element in the second array, check if it is in `set1`. If it is, add it to the `intersection` set.

2. **Union Method**:
   - **Sets**: Use a single `HashSet` to store the union of elements.
   - **Loop**: Add elements of both arrays to the `union` set.

### Example:
For the input arrays `nums1 = {1, 2, 2, 1}` and `nums2 = {2, 2}`:
- **Intersection**: `{2}`
- **Union**: `{1, 2}`

For the input arrays `nums1 = {1, 2, 2, 1}` and `nums2 = {2, 3}`:
- **Intersection**: `{2}`
- **Union**: `{1, 2, 3}`

Feel free to ask if you have any questions or need further assistance!


## Roman to Integer in Java

Sure! Converting a Roman numeral to an integer is a common problem. Here's a Java solution for this:

```java
import java.util.HashMap;
import java.util.Map;

public class RomanToInteger {

    // Method to convert Roman numeral to integer
    public static int romanToInt(String s) {
        Map<Character, Integer> romanMap = new HashMap<>();
        romanMap.put('I', 1);
        romanMap.put('V', 5);
        romanMap.put('X', 10);
        romanMap.put('L', 50);
        romanMap.put('C', 100);
        romanMap.put('D', 500);
        romanMap.put('M', 1000);

        int result = 0;
        int prevValue = 0;

        for (int i = s.length() - 1; i >= 0; i--) {
            int currentValue = romanMap.get(s.charAt(i));
            if (currentValue < prevValue) {
                result -= currentValue;
            } else {
                result += currentValue;
            }
            prevValue = currentValue;
        }

        return result;
    }

    public static void main(String[] args) {
        String roman = "MCMXCIV";
        System.out.println("Integer value: " + romanToInt(roman));
    }
}
```

### Explanation:
1. **romanToInt Method**: This method takes a Roman numeral string and converts it to an integer.
2. **Map**: A `HashMap` is used to store the integer values of Roman numeral characters.
3. **Loop**: Iterates through the string from right to left. If the current value is less than the previous value, it subtracts the current value from the result. Otherwise, it adds the current value to the result.
4. **prevValue**: Keeps track of the value of the previous character to handle the subtraction rule in Roman numerals.

### Example:
For the input Roman numeral `"MCMXCIV"`, the output will be `1994`.

Feel free to ask if you have any questions or need further assistance!

## Integer to Roman in Java

Sure! Converting an integer to a Roman numeral is another common problem. Here's a Java solution for this:

```java
public class IntegerToRoman {

    // Method to convert integer to Roman numeral
    public static String intToRoman(int num) {
        String[] thousands = {"", "M", "MM", "MMM"};
        String[] hundreds = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String[] tens = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String[] units = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};

        return thousands[num / 1000] +
               hundreds[(num % 1000) / 100] +
               tens[(num % 100) / 10] +
               units[num % 10];
    }

    public static void main(String[] args) {
        int num = 1994;
        System.out.println("Roman numeral: " + intToRoman(num));
    }
}
```

### Explanation:
1. **intToRoman Method**: This method takes an integer and converts it to a Roman numeral.
2. **Arrays**: Four arrays are used to store the Roman numeral representations for thousands, hundreds, tens, and units.
3. **Concatenation**: The method constructs the Roman numeral by concatenating the appropriate strings from each array based on the value of the input number.

### Example:
For the input integer `1994`, the output will be `"MCMXCIV"`.

Feel free to ask if you have any questions or need further assistance!

## Combinational Sum in Java

Sure! The "Combination Sum" problem involves finding all unique combinations in an array where the numbers sum up to a target value. Here's a Java solution for this problem using backtracking:

```java
import java.util.ArrayList;
import java.util.List;

public class CombinationSum {

    // Method to find all unique combinations that sum up to the target
    public static List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), candidates, target, 0);
        return result;
    }

    // Helper method for backtracking
    private static void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] candidates, int remain, int start) {
        if (remain < 0) {
            return; // If remain is less than 0, no valid combination
        } else if (remain == 0) {
            result.add(new ArrayList<>(tempList)); // Found a valid combination
        } else {
            for (int i = start; i < candidates.length; i++) {
                tempList.add(candidates[i]);
                backtrack(result, tempList, candidates, remain - candidates[i], i); // Not i + 1 because we can reuse same elements
                tempList.remove(tempList.size() - 1); // Remove last element to backtrack
            }
        }
    }

    public static void main(String[] args) {
        int[] candidates = {2, 3, 6, 7};
        int target = 7;
        List<List<Integer>> combinations = combinationSum(candidates, target);
        System.out.println("Combinations: " + combinations);
    }
}
```

### Explanation:
1. **combinationSum Method**: This method takes an array of candidate numbers and a target sum, and returns a list of lists containing all unique combinations that sum up to the target.
2. **backtrack Method**: This helper method uses backtracking to find all valid combinations.
   - **Base Cases**: If `remain` (remaining sum) is less than 0, it returns as no valid combination can be found. If `remain` is 0, it adds the current combination (`tempList`) to the result.
   - **Loop**: Iterates through the candidates starting from the current index (`start`). It adds the current candidate to `tempList`, recursively calls `backtrack` with the updated remaining sum, and then removes the last element to backtrack.

### Example:
For the input array `[2, 3, 6, 7]` and target `7`, the output will be `[[2, 2, 3], [7]]`.

Feel free to ask if you have any questions or need further assistance!

## Subarray sum equals K

The "Subarray Sum Equals K" problem is a common problem in computer science, particularly in the context of arrays and hashing. The goal is to find the number of continuous subarrays whose sum equals a given value \( K \).

### Problem Explanation

Given an array of integers and an integer \( K \), you need to find the total number of continuous subarrays whose sum equals \( K \).

### Approach

A common and efficient approach to solve this problem is to use a hash map (or dictionary) to store the cumulative sum up to each index. This allows us to quickly find the number of subarrays that sum to \( K \).

### Java Implementation

Here's a Java implementation of the solution:

```java
import java.util.HashMap;

public class SubarraySumEqualsK {

    public static int subarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, 1); // Initialize with sum 0 having one count

        int count = 0;
        int sum = 0;

        for (int num : nums) {
            sum += num;

            if (map.containsKey(sum - k)) {
                count += map.get(sum - k);
            }

            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }

        return count;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 1};
        int k = 2;

        int result = subarraySum(nums, k);
        System.out.println("Number of subarrays with sum " + k + " = " + result);
    }
}
```

### Explanation of the Code

1. **HashMap Initialization**: We use a `HashMap` to store the cumulative sum and its frequency. We initialize it with `(0, 1)` to handle the case where a subarray starts from the beginning of the array.
2. **Iterate Through the Array**: We iterate through the array, updating the cumulative sum.
3. **Check for Subarray Sum**: For each element, we check if `(sum - k)` exists in the map. If it does, it means there is a subarray ending at the current index with sum \( K \).
4. **Update the Map**: We update the map with the current cumulative sum.

### Example

For the array `[1, 1, 1]` and \( K = 2 \):
- The subarrays `[1, 1]` (starting at index 0) and `[1, 1]` (starting at index 1) both sum to 2.
- The output will be `2`.

Feel free to ask if you have any questions or need further clarification!



## Kaden algo in Java

Sure! Kadane's Algorithm is used to find the maximum sum of a contiguous subarray in an array of integers. Here's a Java implementation of Kadane's Algorithm:

```java
public class KadanesAlgorithm {

    // Method to find the maximum sum of a contiguous subarray
    public static int maxSubArray(int[] nums) {
        int maxSoFar = nums[0];
        int maxEndingHere = nums[0];

        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }

        return maxSoFar;
    }

    public static void main(String[] args) {
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum sum of contiguous subarray: " + maxSubArray(nums));
    }
}
```

### Explanation:
1. **maxSubArray Method**: This method takes an array of integers and returns the maximum sum of a contiguous subarray.
2. **maxSoFar**: Keeps track of the maximum sum encountered so far.
3. ****: Keeps track of the maximum sum of the subarray ending at the current position.
4. **Loop**: Iterates through the array starting from the second element. For each element, it updates `maxEndingHere` to be the maximum of the current element and the sum of `maxEndingHere` and the current element. It then updates `maxSoFar` to be the maximum of `maxSoFar` and `maxEndingHere`.

### Example:
For the input array `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`, the maximum sum of a contiguous subarray is `6` (subarray `[4, -1, 2, 1]`).

Feel free to ask if you have any questions or need further assistance!

## Print all Subset of array

Sure! Printing all subsets (or power set) of an array can be done using backtracking. Here's a Java solution for this:

```java
import java.util.ArrayList;
import java.util.List;

public class Subsets {

    // Method to find all subsets of an array
    public static List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), nums, 0);
        return result;
    }

    // Helper method for backtracking
    private static void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] nums, int start) {
        result.add(new ArrayList<>(tempList));
        for (int i = start; i < nums.length; i++) {
            tempList.add(nums[i]);
            backtrack(result, tempList, nums, i + 1);
            tempList.remove(tempList.size() - 1);
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        List<List<Integer>> subsets = subsets(nums);
        System.out.println("Subsets: " + subsets);
    }
}
```

### Explanation:
1. **subsets Method**: This method takes an array of integers and returns a list of lists containing all subsets of the array.
2. **backtrack Method**: This helper method uses backtracking to generate all subsets.
   - **Base Case**: Adds the current combination (`tempList`) to the result.
   - **Loop**: Iterates through the array starting from the current index (`start`). It adds the current element to `tempList`, recursively calls `backtrack` with the next index, and then removes the last element to backtrack.

### Example:
For the input array `[1, 2, 3]`, the output will be:
```
Subsets: [[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
```

Feel free to ask if you have any questions or need further assistance!

## Merge Sort in Java using Space


Sure! Merge Sort is a divide-and-conquer algorithm that sorts an array by dividing it into two halves, sorting each half, and then merging the sorted halves. Here's a Java implementation of Merge Sort:

```java
import java.util.Arrays;

public class MergeSort {

    // Method to sort an array using Merge Sort
    public static void mergeSort(int[] array) {
        if (array.length < 2) {
            return;
        }

        int mid = array.length / 2;
        int[] left = Arrays.copyOfRange(array, 0, mid);
        int[] right = Arrays.copyOfRange(array, mid, array.length);

        mergeSort(left);
        mergeSort(right);

        merge(array, left, right);
    }

    // Method to merge two sorted arrays
    private static void merge(int[] array, int[] left, int[] right) {
        int i = 0, j = 0, k = 0;

        while (i < left.length && j < right.length) {
            if (left[i] <= right[j]) {
                array[k++] = left[i++];
            } else {
                array[k++] = right[j++];
            }
        }

        while (i < left.length) {
            array[k++] = left[i++];
        }

        while (j < right.length) {
            array[k++] = right[j++];
        }
    }

    public static void main(String[] args) {
        int[] array = {38, 27, 43, 3, 9, 82, 10};
        System.out.println("Original array: " + Arrays.toString(array));
        mergeSort(array);
        System.out.println("Sorted array: " + Arrays.toString(array));
    }
}
```

### Explanation:
1. **mergeSort Method**: This method takes an array and sorts it using the Merge Sort algorithm.
   - **Base Case**: If the array has less than two elements, it is already sorted.
   - **Divide**: The array is divided into two halves.
   - **Recursion**: The `mergeSort` method is called recursively on each half.
   - **Merge**: The `merge` method is used to merge the two sorted halves.

2. **merge Method**: This method merges two sorted arrays into a single sorted array.
   - **Pointers**: Three pointers (`i`, `j`, `k`) are used to keep track of the current index in the left array, right array, and merged array, respectively.
   - **Comparison**: Elements from the left and right arrays are compared and added to the merged array in sorted order.
   - **Remaining Elements**: Any remaining elements in the left or right array are added to the merged array.

### Example:
For the input array `[38, 27, 43, 3, 9, 82, 10]`, the output will be:
```
Original array: [38, 27, 43, 3, 9, 82, 10]
Sorted array: [3, 9, 10, 27, 38, 43, 82]
```

Feel free to ask if you have any questions or need further assistance!

## Merge sort without using extra space 

Implementing Merge Sort without using extra space is quite challenging because the standard Merge Sort algorithm inherently requires additional space for the temporary arrays used during the merge process. However, it is possible to perform an in-place merge sort with some modifications. Here's an approach to achieve this:

### In-Place Merge Sort

1. **Divide**: Divide the array into two halves.
2. **Sort**: Recursively sort each half.
3. **Merge**: Merge the two sorted halves in place.

Here's a Java implementation of in-place merge sort:

```java
public class InPlaceMergeSort {

    // Method to sort an array using in-place merge sort
    public static void mergeSort(int[] array, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;

            // Sort first and second halves
            mergeSort(array, left, mid);
            mergeSort(array, mid + 1, right);

            // Merge the sorted halves
            merge(array, left, mid, right);
        }
    }

    // Method to merge two sorted halves in place
    private static void merge(int[] array, int left, int mid, int right) {
        int start2 = mid + 1;

        // If the direct merge is already sorted
        if (array[mid] <= array[start2]) {
            return;
        }

        // Two pointers to maintain start of both arrays to merge
        while (left <= mid && start2 <= right) {
            // If element 1 is in right place
            if (array[left] <= array[start2]) {
                left++;
            } else {
                int value = array[start2];
                int index = start2;

                // Shift all the elements between element 1 and element 2 right by 1
                while (index != left) {
                    array[index] = array[index - 1];
                    index--;
                }
                array[left] = value;

                // Update all the pointers
                left++;
                mid++;
                start2++;
            }
        }
    }

    public static void main(String[] args) {
        int[] array = {38, 27, 43, 3, 9, 82, 10};
        System.out.println("Original array: " + java.util.Arrays.toString(array));
        mergeSort(array, 0, array.length - 1);
        System.out.println("Sorted array: " + java.util.Arrays.toString(array));
    }
}
```

### Explanation:
1. **mergeSort Method**: This method takes an array and sorts it using the in-place merge sort algorithm.
   - **Base Case**: If the left index is less than the right index, the array is divided into two halves.
   - **Recursion**: The `mergeSort` method is called recursively on each half.
   - **Merge**: The `merge` method is used to merge the two sorted halves in place.

2. **merge Method**: This method merges two sorted halves of the array in place.
   - **Direct Merge Check**: If the two halves are already sorted, no merging is needed.
   - **Pointers**: Two pointers are used to keep track of the current index in each half.
   - **Shifting Elements**: If an element in the second half is smaller than an element in the first half, the elements in the first half are shifted to the right to make space for the smaller element.

### Example:
For the input array `[38, 27, 43, 3, 9, 82, 10]`, the output will be:
```
Original array: [38, 27, 43, 3, 9, 82, 10]
Sorted array: [3, 9, 10, 27, 38, 43, 82]
```

Feel free to ask if you have any questions or need further assistance!


## Merge Sort

Sure! Merge Sort is a classic sorting algorithm that uses the divide-and-conquer approach to sort an array. Here's a detailed Java implementation of Merge Sort:

### Merge Sort Algorithm

1. **Divide**: Split the array into two halves.
2. **Conquer**: Recursively sort each half.
3. **Combine**: Merge the two sorted halves to produce the sorted array.

### Java Implementation

Here's how you can implement Merge Sort in Java:

```java
import java.util.Arrays;

public class MergeSort {

    // Method to sort an array using Merge Sort
    public static void mergeSort(int[] array) {
        if (array.length < 2) {
            return;
        }

        int mid = array.length / 2;
        int[] left = Arrays.copyOfRange(array, 0, mid);
        int[] right = Arrays.copyOfRange(array, mid, array.length);

        mergeSort(left);
        mergeSort(right);

        merge(array, left, right);
    }

    // Method to merge two sorted arrays
    private static void merge(int[] array, int[] left, int[] right) {
        int i = 0, j = 0, k = 0;

        while (i < left.length && j < right.length) {
            if (left[i] <= right[j]) {
                array[k++] = left[i++];
            } else {
                array[k++] = right[j++];
            }
        }

        while (i < left.length) {
            array[k++] = left[i++];
        }

        while (j < right.length) {
            array[k++] = right[j++];
        }
    }

    public static void main(String[] args) {
        int[] array = {38, 27, 43, 3, 9, 82, 10};
        System.out.println("Original array: " + Arrays.toString(array));
        mergeSort(array);
        System.out.println("Sorted array: " + Arrays.toString(array));
    }
}
```

### Explanation:
1. **mergeSort Method**: This method takes an array and sorts it using the Merge Sort algorithm.
   - **Base Case**: If the array has less than two elements, it is already sorted.
   - **Divide**: The array is divided into two halves.
   - **Recursion**: The `mergeSort` method is called recursively on each half.
   - **Merge**: The `merge` method is used to merge the two sorted halves.

2. **merge Method**: This method merges two sorted arrays into a single sorted array.
   - **Pointers**: Three pointers (`i`, `j`, `k`) are used to keep track of the current index in the left array, right array, and merged array, respectively.
   - **Comparison**: Elements from the left and right arrays are compared and added to the merged array in sorted order.
   - **Remaining Elements**: Any remaining elements in the left or right array are added to the merged array.

### Example:
For the input array `[38, 27, 43, 3, 9, 82, 10]`, the output will be:
```
Original array: [38, 27, 43, 3, 9, 82, 10]
Sorted array: [3, 9, 10, 27, 38, 43, 82]
```

Feel free to ask if you have any questions or need further assistance!

## Quick Sort

Sure! Quick Sort is another efficient, divide-and-conquer sorting algorithm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.

### Quick Sort Algorithm

1. **Choose a Pivot**: Select an element as the pivot.
2. **Partition**: Rearrange the array so that elements less than the pivot are on the left, elements greater than the pivot are on the right.
3. **Recursively Sort**: Apply the same process to the left and right sub-arrays.

### Java Implementation

Here's how you can implement Quick Sort in Java:

```java
import java.util.Arrays;

public class QuickSort {

    // Method to sort an array using Quick Sort
    public static void quickSort(int[] array, int low, int high) {
        if (low < high) {
            int pi = partition(array, low, high);

            // Recursively sort elements before and after partition
            quickSort(array, low, pi - 1);
            quickSort(array, pi + 1, high);
        }
    }

    // Method to partition the array
    private static int partition(int[] array, int low, int high) {
        int pivot = array[high];
        int i = (low - 1); // Index of smaller element

        for (int j = low; j < high; j++) {
            // If current element is smaller than or equal to pivot
            if (array[j] <= pivot) {
                i++;

                // Swap array[i] and array[j]
                int temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }
        }

        // Swap array[i + 1] and array[high] (or pivot)
        int temp = array[i + 1];
        array[i + 1] = array[high];
        array[high] = temp;

        return i + 1;
    }

    public static void main(String[] args) {
        int[] array = {10, 7, 8, 9, 1, 5};
        System.out.println("Original array: " + Arrays.toString(array));
        quickSort(array, 0, array.length - 1);
        System.out.println("Sorted array: " + Arrays.toString(array));
    }
}
```

### Explanation:
1. **quickSort Method**: This method takes an array and sorts it using the Quick Sort algorithm.
   - **Base Case**: If the low index is less than the high index, the array is partitioned.
   - **Recursion**: The `quickSort` method is called recursively on the left and right sub-arrays.

2. **partition Method**: This method partitions the array around the pivot.
   - **Pivot**: The pivot is chosen as the last element of the array.
   - **Pointers**: Two pointers are used to keep track of the current index and the index of the smaller element.
   - **Swapping**: Elements are swapped to ensure that elements less than the pivot are on the left and elements greater than the pivot are on the right.

### Example:
For the input array `[10, 7, 8, 9, 1, 5]`, the output will be:
```
Original array: [10, 7, 8, 9, 1, 5]
Sorted array: [1, 5, 7, 8, 9, 10]
```

Feel free to ask if you have any questions or need further assistance!

## Top K Elements from Array

Finding the top K elements from an array is a common problem that can be solved using various approaches. One efficient way is to use a Min-Heap (PriorityQueue in Java). Here's a Java implementation to find the top K largest elements from an array:

### Java Implementation

```java
import java.util.PriorityQueue;
import java.util.Arrays;

public class TopKElements {

    // Method to find the top K largest elements from an array
    public static int[] findTopKElements(int[] array, int k) {
        if (k <= 0 || array == null || array.length == 0) {
            return new int[0];
        }

        PriorityQueue<Integer> minHeap = new PriorityQueue<>(k);

        for (int num : array) {
            if (minHeap.size() < k) {
                minHeap.add(num);
            } else if (num > minHeap.peek()) {
                minHeap.poll();
                minHeap.add(num);
            }
        }

        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = minHeap.poll();
        }

        return result;
    }

    public static void main(String[] args) {
        int[] array = {3, 2, 1, 5, 6, 4};
        int k = 2;
        int[] topK = findTopKElements(array, k);
        System.out.println("Top " + k + " elements: " + Arrays.toString(topK));
    }
}
```

### Explanation:
1. **findTopKElements Method**: This method takes an array and an integer `k`, and returns an array of the top `k` largest elements.
   - **Edge Cases**: If `k` is less than or equal to 0, or the array is null or empty, it returns an empty array.
   - **Min-Heap**: A `PriorityQueue` (Min-Heap) is used to keep track of the top `k` elements.
   - **Loop**: Iterates through the array. If the heap size is less than `k`, it adds the element to the heap. If the current element is larger than the smallest element in the heap, it removes the smallest element and adds the current element.
   - **Result Array**: The top `k` elements are extracted from the heap and stored in the result array.

### Example:
For the input array `[3, 2, 1, 5, 6, 4]` and `k = 2`, the output will be:
```
Top 2 elements: [5, 6]
```

Feel free to ask if you have any questions or need further assistance!

## Binary Search in Java

Sure! Binary Search is an efficient algorithm for finding an element in a sorted array. It works by repeatedly dividing the search interval in half. If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half. Otherwise, narrow it to the upper half. Repeatedly check until the value is found or the interval is empty.

### Java Implementation

Here's how you can implement Binary Search in Java:

```java
public class BinarySearch {

    // Method to perform binary search on a sorted array
    public static int binarySearch(int[] array, int target) {
        int left = 0;
        int right = array.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (array[mid] == target) {
                return mid; // Target found
            } else if (array[mid] < target) {
                left = mid + 1; // Search in the right half
            } else {
                right = mid - 1; // Search in the left half
            }
        }

        return -1; // Target not found
    }

    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        int target = 5;
        int result = binarySearch(array, target);
        if (result != -1) {
            System.out.println("Element found at index: " + result);
        } else {
            System.out.println("Element not found in the array.");
        }
    }
}
```

### Explanation:
1. **binarySearch Method**: This method takes a sorted array and a target value, and returns the index of the target value if found, or `-1` if not found.
   - **Pointers**: `left` and `right` pointers are used to keep track of the current search interval.
   - **Loop**: The loop continues as long as `left` is less than or equal to `right`.
   - **Midpoint Calculation**: The midpoint `mid` is calculated as `left + (right - left) / 2` to avoid potential overflow.
   - **Comparison**: If the target value is equal to the middle element, the index is returned. If the target value is less than the middle element, the search interval is narrowed to the left half. If the target value is greater than the middle element, the search interval is narrowed to the right half.

### Example:
For the input array `[1, 2, 3, 4, 5, 6, 7, 8, 9]` and target `5`, the output will be:
```
Element found at index: 4
```

Feel free to ask if you have any questions or need further assistance!

## Search in Rotated Array

Searching in a rotated sorted array is a common problem. The array is initially sorted but then rotated at some pivot. Here's a Java implementation to search for a target value in such an array:

### Java Implementation

```java
public class SearchInRotatedArray {

    // Method to search in a rotated sorted array
    public static int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                return mid; // Target found
            }

            // Determine which side is properly sorted
            if (nums[left] <= nums[mid]) {
                // Left side is sorted
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1; // Target is in the left side
                } else {
                    left = mid + 1; // Target is in the right side
                }
            } else {
                // Right side is sorted
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1; // Target is in the right side
                } else {
                    right = mid - 1; // Target is in the left side
                }
            }
        }

        return -1; // Target not found
    }

    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        int result = search(nums, target);
        if (result != -1) {
            System.out.println("Element found at index: " + result);
        } else {
            System.out.println("Element not found in the array.");
        }
    }
}
```

### Explanation:
1. **search Method**: This method takes a rotated sorted array and a target value, and returns the index of the target value if found, or `-1` if not found.
   - **Pointers**: `left` and `right` pointers are used to keep track of the current search interval.
   - **Loop**: The loop continues as long as `left` is less than or equal to `right`.
   - **Midpoint Calculation**: The midpoint `mid` is calculated as `left + (right - left) / 2` to avoid potential overflow.
   - **Comparison**: If the target value is equal to the middle element, the index is returned.
   - **Determine Sorted Side**: Check which side (left or right) is properly sorted.
     - **Left Side Sorted**: If the left side is sorted, check if the target is within the range of the left side. If it is, narrow the search to the left side. Otherwise, narrow the search to the right side.
     - **Right Side Sorted**: If the right side is sorted, check if the target is within the range of the right side. If it is, narrow the search to the right side. Otherwise, narrow the search to the left side.

### Example:
For the input array `[4, 5, 6, 7, 0, 1, 2]` and target `0`, the output will be:
```
Element found at index: 4
```

Feel free to ask if you have any questions or need further assistance!

## 2 Sum

Sure! The "Two Sum" problem involves finding two numbers in an array that add up to a specific target. Here's a Java solution using a `HashMap` to achieve this efficiently:

### Java Implementation

```java
import java.util.HashMap;
import java.util.Map;

public class TwoSum {

    // Method to find two numbers that add up to the target
    public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }

        throw new IllegalArgumentException("No two sum solution");
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        int[] result = twoSum(nums, target);
        System.out.println("Indices: " + result[0] + ", " + result[1]);
    }
}
```

### Explanation:
1. **twoSum Method**: This method takes an array of integers and a target value, and returns the indices of the two numbers that add up to the target.
   - **HashMap**: A `HashMap` is used to store the numbers and their indices.
   - **Loop**: Iterates through the array. For each number, it calculates the complement (the number needed to reach the target when added to the current number).
   - **Check Complement**: If the complement is already in the map, it means we have found the two numbers that add up to the target. The indices of these two numbers are returned.
   - **Store in Map**: If the complement is not found, the current number and its index are stored in the map.

### Example:
For the input array `[2, 7, 11, 15]` and target `9`, the output will be:
```
Indices: 0, 1
```
This means the numbers at indices 0 and 1 (i.e., 2 and 7) add up to the target 9.

Feel free to ask if you have any questions or need further assistance!

## 3 Sum

The "3 Sum" problem involves finding all unique triplets in an array that sum up to zero. Here's a Java solution for this problem:

### Java Implementation

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ThreeSum {

    // Method to find all unique triplets that sum up to zero
    public static List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);

        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue; // Skip duplicate elements
            }

            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));

                    while (left < right && nums[left] == nums[left + 1]) {
                        left++; // Skip duplicate elements
                    }
                    while (left < right && nums[right] == nums[right - 1]) {
                        right--; // Skip duplicate elements
                    }

                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> triplets = threeSum(nums);
        System.out.println("Triplets: " + triplets);
    }
}
```

### Explanation:
1. **threeSum Method**: This method takes an array of integers and returns a list of lists containing all unique triplets that sum up to zero.
   - **Sorting**: The array is sorted to make it easier to avoid duplicates and use the two-pointer technique.
   - **Loop**: Iterates through the array. For element, it uses two pointers (`left` and `right`) to find pairs that sum up to the negative of the current element.
   - **Skip Duplicates**: If the current element is the same as the previous element, it is skipped to avoid duplicate triplets.
   - **Two-Pointer Technique**: The `left` pointer starts just after the current element, and the `right` pointer starts at the end of the array. The sum of the three elements is calculated. If the sum is zero, the triplet is added to the result. If the sum is less than zero, the `left` pointer is moved to the right. If the sum is greater than zero, the `right` pointer is moved to the left.
   - **Skip Duplicate Pairs**: After finding a valid triplet, the `left` and `right` pointers are moved to skip any duplicate elements.

### Example:
For the input array `[-1, 0, 1, 2, -1, -4]`, the output will be:
```
Triplets: [[-1, -1, 2], [-1, 0, 1]]
```

Feel free to ask if you have any questions or need further assistance!

## 4 Sum

The "4 Sum" problem involves finding all unique quadruplets in an array that sum up to a specific target. Here's a Java solution for this problem:

### Java Implementation

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class FourSum {

    // Method to find all unique quadruplets that sum up to the target
    public static List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);

        for (int i = 0; i < nums.length - 3; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue; // Skip duplicate elements
            }

            for (int j = i + 1; j < nums.length - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue; // Skip duplicate elements
                }

                int left = j + 1;
                int right = nums.length - 1;

                while (left < right) {
                    int sum = nums[i] + nums[j] + nums[left] + nums[right];

                    if (sum == target) {
                        result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));

                        while (left < right && nums[left] == nums[left + 1]) {
                            left++; // Skip duplicate elements
                        }
                        while (left < right && nums[right] == nums[right - 1]) {
                            right--; // Skip duplicate elements
                        }

                        left++;
                        right--;
                    } else if (sum < target) {
                        left++;
                    } else {
                        right--;
                    }
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {1, 0, -1, 0, -2, 2};
        int target = 0;
        List<List<Integer>> quadruplets = fourSum(nums, target);
        System.out.println("Quadruplets: " + quadruplets);
    }
}
```

### Explanation:
1. **fourSum Method**: This method takes an array of integers and a target value, and returns a list of lists containing all unique quadruplets that sum up to the target.
   - **Sorting**: The array is sorted to make it easier to avoid duplicates and use the two-pointer technique.
   - **Outer Loops**: Two nested loops iterate through the array to fix the first two elements of the quadruplet.
   - **Skip Duplicates**: If the current element is the same as the previous element, it is skipped to avoid duplicate quadruplets.
   - **Two-Pointer Technique**: The `left` pointer starts just after the second fixed element, and the `right` pointer starts at the end of the array. The sum of the four elements is calculated. If the sum is equal to the target, the quadruplet is added to the result. If the sum is less than the target, the `left` pointer is moved to the right. If the sum is greater than the target, the `right` pointer is moved to the left.
   - **Skip Duplicate Pairs**: After finding a valid quadruplet, the `left` and `right` pointers are moved to skip any duplicate elements.

### Example:
For the input array `[1, 0, -1, 0, -2, 2]` and target `0`, the output will be:
```
Quadruplets: [[-2, -1, 1, 2], [-2, 0, 0, 2], [-1, 0, 0, 1]]
```

Feel free to ask if you have any questions or need further assistance!

## Coin Change

Sure! The Coin Change problem using Dynamic Programming (DP) is a classic problem where you need to find the minimum number of coins required to make a given amount. Here's a detailed Java implementation:

### Java Implementation

```java
import java.util.Arrays;

public class CoinChangeDP {

    // Method to find the minimum number of coins needed to make the amount
    public static int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;

        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (i - coin >= 0) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }

    public static void main(String[] args) {
        int[] coins = {1, 2, 5};
        int amount = 11;
        int result = coinChange(coins, amount);
        System.out.println("Minimum coins needed: " + result);
    }
}
```

### Explanation:
1. **DP Array**: `dp[i]` represents the minimum number of coins needed to make the amount `i`.
2. **Initialization**: The `dp` array is initialized with a value greater than the maximum possible amount (`amount + 1`), and `dp[0]` is set to 0.
3. **Nested Loops**: The outer loop iterates through each amount from 1 to `amount`. The inner loop iterates through each coin. If the current amount minus the coin value is non-negative, the `dp` value is updated to the minimum of its current value and `dp[i - coin] + 1`.
4. **Result**: If `dp[amount]` is greater than `amount`, it means it's not possible to make the amount with the given coins, so return -1. Otherwise, return `dp[amount]`.

### Example:
For the input array `[1, 2, 5]` and amount `11`, the output will be:
```
Minimum coins needed: 3
```
This is because the minimum number of coins needed to make 11 is 3 (5 + 5 + 1).

Feel free to ask if you have any questions or need further assistance!


## 0 1 Knapsack in Java

Sure! The 0/1 Knapsack problem is a classic problem in computer science and optimization. The problem is to determine the maximum value that can be obtained by selecting items with given weights and values, without exceeding a given weight capacity. Each item can either be included or excluded from the knapsack.

### Dynamic Programming Approach

The idea is to use a DP table where `dp[i][w]` represents the maximum value that can be obtained with the first `i` items and a weight capacity of `w`.

#### Java Implementation

```java
public class Knapsack {

    // Method to solve the 0/1 Knapsack problem
    public static int knapsack(int[] weights, int[] values, int capacity) {
        int n = weights.length;
        int[][] dp = new int[n + 1][capacity + 1];

        for (int i = 1; i <= n; i++) {
            for (int w = 0; w <= capacity; w++) {
                if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }

        return dp[n][capacity];
    }

    public static void main(String[] args) {
        int[] weights = {1, 3, 4, 5};
        int[] values = {1, 4, 5, 7};
        int capacity = 7;
        int maxValue = knapsack(weights, values, capacity);
        System.out.println("Maximum value in Knapsack: " + maxValue);
    }
}
```

### Explanation:
1. **knapsack Method**: This method takes arrays of weights and values, and the capacity of the knapsack, and returns the maximum value that can be obtained.
2. **DP Table**: A 2D array `dp` is used where `dp[i][w]` represents the maximum value that can be obtained with the first `i` items and a weight capacity of `w`.
3. **Nested Loops**: The outer loop iterates through the items, and the inner loop iterates through the weight capacities from 0 to the given capacity.
4. **Include or Exclude Item**: For each item, check if its weight is less than or equal to the current capacity. If it is, update the `dp` value to the maximum of excluding the item or including the item. If the item's weight is greater than the current capacity, exclude the item.
5. **Result**: The maximum value that can be obtained is stored in `dp[n][capacity]`.

### Example:
For the input weights `[1, 3, 4, 5]`, values `[1, 4, 5, 7]`, and capacity `7`, the output will be:
```
Maximum value in Knapsack: 9
```
This is because the maximum value that can be obtained is 9 (by including items with weights 3 and 4).

Feel free to ask if you have any questions or need further assistance!

## Explain Fractional Knapsack in Java

The fractional knapsack problem is a variation of the classic knapsack problem. In this version, you can take fractions of items rather than having to take an item in its entirety. This allows for a more optimal solution when dealing with items of varying weights and values.

### Problem Explanation

Given a set of items, each with a weight and a value, the goal is to determine the maximum value that can be obtained by putting items into a knapsack of a fixed capacity. Unlike the 0/1 knapsack problem, where you can either take an item or leave it, in the fractional knapsack problem, you can take any fraction of an item.

### Greedy Algorithm Approach

The fractional knapsack problem can be efficiently solved using a greedy algorithm. The idea is to take items in the order of their value-to-weight ratio (value per unit weight), starting with the highest. This ensures that we get the maximum value for the least weight.

### Java Implementation

Here's a step-by-step explanation of the Java implementation:

1. **Define the Item Class**: This class will store the weight and value of each item.
2. **Sort Items by Value-to-Weight Ratio**: Sort the items in descending order based on their value-to-weight ratio.
3. **Add Items to Knapsack**: Add items to the knapsack starting with the highest ratio. If the knapsack can't hold the entire item, add a fraction of it.

Here's the complete code:

```java
import java.util.Arrays;
import java.util.Comparator;

class Item {
    int weight;
    int value;

    Item(int weight, int value) {
        this.weight = weight;
        this.value = value;
    }
}

public class FractionalKnapsack {

    private static double getMaxValue(int capacity, Item[] items) {
        Arrays.sort(items, new Comparator<Item>() {
            @Override
            public int compare(Item o1, Item o2) {
                double r1 = (double) o1.value / o1.weight;
                double r2 = (double) o2.value / o2.weight;
                return Double.compare(r2, r1);
            }
        });

        double totalValue = 0.0;

        for (Item item : items) {
            if (capacity - item.weight >= 0) {
                capacity -= item.weight;
                totalValue += item.value;
            } else {
                totalValue += item.value * ((double) capacity / item.weight);
                break;
            }
        }

        return totalValue;
    }

    public static void main(String[] args) {
        Item[] items = {new Item(10, 60), new Item(20, 100), new Item(30, 120)};
        int capacity = 50;

        double maxValue = getMaxValue(capacity, items);
        System.out.println("Maximum value we can obtain = " + maxValue);
    }
}
```

### Explanation of the Code

1. **Item Class**: This class has two fields, `weight` and `value`, and a constructor to initialize them.
2. **getMaxValue Method**: This method sorts the items by their value-to-weight ratio in descending order. It then iterates through the sorted items, adding as much of each item as possible to the knapsack. If the knapsack can't hold the entire item, it adds a fraction of it.
3. **Main Method**: This method creates an array of items and a knapsack capacity. It then calls `getMaxValue` to find the maximum value that can be obtained and prints the result.

Feel free to ask if you have any questions or need further clarification!


## Edit Distance

The edit distance (or Levenshtein distance) is a measure of how dissimilar two strings are by counting the minimum number of operations required to transform one string into the other. The allowed operations are insertion, deletion, and substitution.

### Problem Explanation

Given two strings, the goal is to find the minimum number of operations required to convert one string into the other.

### Dynamic Programming Approach

A common approach to solve this problem is using dynamic programming. We create a 2D array `dp` where `dp[i][j]` represents the edit distance between the first `i` characters of the first string and the first `j` characters of the second string.

### Java Implementation

Here's a Java implementation of the edit distance algorithm:

```java
public class EditDistance {

    public static int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m + 1][n + 1];

        // Initialize the dp array
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }

        // Fill the dp array
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j - 1], // Substitution
                                            Math.min(dp[i - 1][j], // Deletion
                                                     dp[i][j - 1])); // Insertion
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String word1 = "kitten";
        String word2 = "sitting";

        int result = minDistance(word1, word2);
        System.out.println("Edit distance between \"" + word1 + "\" and \"" + word2 + "\" is " + result);
    }
}
```

### Explanation of the Code

1 We initialize a 2D array `dp` where `dp[i][j]` represents the edit distance between the first `i` characters of `word1` and the first `j` characters of `word2`. The first row and first column are initialized to represent the cost of converting an empty string to the other string.
2. **Filling the DP Array**: We iterate through each character of both strings. If the characters are the same, the edit distance is the same as for the previous characters. If they are different, we take the minimum of the three possible operations (substitution, deletion, insertion) and add one to it.
3. **Result**: The value at `dp[m][n]` gives the edit distance between the two strings.

### Example

For the strings "kitten" and "sitting":
- The edit distance is 3 (substitute 'k' with 's', substitute 'e' with 'i', and add 'g' at the end).

Feel free to ask if you have any questions or need further clarification!

## House Robber

The "House Robber" problem is a classic dynamic programming problem. The goal is to determine the maximum amount of money you can rob tonight without alerting the police, given that adjacent houses have security systems connected and will automatically contact the police if two adjacent houses are broken into on the same night.

### Problem Explanation

Given an array of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob without robbing two adjacent houses.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining an array `dp` where `dp[i]` represents the maximum amount of money that can be robbed from the first `i` houses.

### Java Implementation

Here's a Java implementation of the House Robber problem:

```java
public class HouseRobber {

    public static int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        if (nums.length == 1) {
            return nums[0];
        }

        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);

        for (int i = 2; i < nums.length; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
        }

        return dp[dp.length - 1];
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 9, 3, 1};
        int result = rob(nums);
        System.out.println("Maximum amount of money that can be robbed = " + result);
    }
}
```

### Explanation of the Code

1 **Base Cases**: If there are no houses (`nums.length == 0`), return 0. If there is only one house, return its value.
2. **Initialize DP Array**: Create a `dp` array where `dp[i]` represents the maximum amount of money that can be robbed from the first `i` houses.
3. **Fill DP Array**: 
   - For the first house, `dp[0]` is simply `nums[0]`.
   - For the second house, `dp[1]` is the maximum of `nums[0]` and `nums[1]`.
   - For each subsequent house, decide whether to rob it or not by comparing:
     - Not robbing it: `dp[i - 1]`
     - Robbing it: `dp[i - 2] + nums[i]`
4. **Result**: The value at `dp[dp.length - 1]` gives the maximum amount of money that can be robbed.

### Example

For the array `[2, 7, 9, 3, 1]`:
- The maximum amount of money that can be robbed is `12` (rob houses with amounts `2`, `9`, and `1`).

Feel free to ask if you have any questions or need further clarification!

## Unqiue Path 

The "Unique Paths" problem is a classic combinatorial problem. The goal is to find the number of unique paths from the top-left corner to the bottom-right corner of a grid, given that you can only move either down or right at any point in time.

### Problem Explanation

Given a grid with `m` rows and `n` columns, you need to find the number of unique paths from the top-left corner to the bottom-right corner.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining a 2D array `dp` where `dp[i][j]` represents the number of unique paths to reach cell `(i, j)`.

### Java Implementation

Here's a Java implementation of the Unique Paths problem:

```java
public class UniquePaths {

    public static int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];

        // Initialize the first row and first column
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            dp[0][j] = 1;
        }

        // Fill the dp array
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }

        return dp[m - 1][n - 1];
    }

    public static void main(String[] args) {
        int m = 3;
        int n = 7;

        int result = uniquePaths(m, n);
        System.out.println("Number of unique paths = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a 2D array `dp` where `dp[i][j]` represents the number of unique paths to reach cell `(i, j)`. The first row and first column are initialized to 1 because there is only one way to reach any cell in the first row or first column (either all the way right or all the way down).
2. **Filling the DP Array**: We iterate through the grid starting from cell `(1, 1)`. For each cell `(i, j)`, the number of unique paths to reach it is the sum of the unique paths to reach the cell directly above it `(i-1, j)` and the cell directly to the left of it `(i, j-1)`.
3. **Result**: The value at `dp[m-1][n-1]` gives the number of unique paths from the top-left corner to the bottom-right corner.

### Example

For a grid with `m = 3` and `n = 7`:
- The number of unique paths is `28`.

Feel free to ask if you have any questions or need further clarification!

## Maximum Product Subarray 

The "Maximum Product Subarray" problem involves finding the contiguous subarray within an array (containing at least one number) which has the largest product.

### Problem Explanation

Given an integer array `nums`, find the contiguous subarray within the array that has the largest product and return the product.

### Approach

To solve this problem, we need to keep track of both the maximum and minimum products up to the current position because a negative number can turn a small product into a large one and vice versa. We can use dynamic programming to maintain these values.

### Java Implementation

Here's a Java implementation of the Maximum Product Subarray problem:

```java
public class MaximumProductSubarray {

    public static int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int maxProduct = nums[0];
        int minProduct = nums[0];
        int result = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {
                // Swap maxProduct and minProduct when nums[i] is negative
                int temp = maxProduct;
                maxProduct = minProduct;
                minProduct = temp;
            }

            maxProduct = Math.max(nums[i], maxProduct * nums[i]);
            minProduct = Math.min(nums[i], minProduct * nums[i]);

            result = Math.max(result, maxProduct);
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, -2, 4};
        int result = maxProduct(nums);
        System.out.println("Maximum product subarray = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize `maxProduct`, `minProduct`, and `result` with the first element of the array. `maxProduct` and `minProduct` keep track of the maximum and minimum products up to the current position.
2. **Iterate Through the Array**: We iterate through the array starting from the second element. If the current element is negative, we swap `maxProduct` and `minProduct` because multiplying by a negative number flips the sign.
3. **Update Products**: We update `maxProduct` to be the maximum of the current element and the product of `maxProduct` and the current element. Similarly, we update `minProduct` to be the minimum of the current element and the product of `minProduct` and the current element.
4. **Update Result**: We update `result` to be the maximum of `result` and `maxProduct`.

### Example

For the array `[2, 3, -2, 4]`:
- The maximum product subarray is `[2, 3]` with a product of `6`.

Feel free to ask if you have any questions or need further clarification!

## LCS 

The Longest Common Subsequence (LCS) problem is a classic problem in computer science. The goal is to find the longest subsequence common to two sequences. A subsequence is a sequence that appears in the same relative order, but not necessarily consecutively.

### Problem Explanation

Given two strings, find the length of their longest common subsequence.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining a 2D array `dp` where `dp[i][j]` represents the length of the longest common subsequence of the first `i` characters of the first string and the first `j` characters of the second string.

### Java Implementation

Here's a Java implementation of the Longest Common Subsequence problem:

```java
public class LongestCommonSubsequence {

    public static int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];

        // Fill the dp array
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String text1 = "abcde";
        String text2 = "ace";

        int result = longestCommonSubsequence(text1, text2);
        System.out.println("Length of Longest Common Subsequence = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a 2D array `dp` where `dp[i][j]` represents the length of the longest common subsequence of the first `i` characters of `text1` and the first `j` characters of `text2`.
2. **Filling the DP Array**: We iterate through each character of both strings. If the characters are the same, the length of the LCS is incremented by 1 from the previous characters. If they are different, we take the maximum of the LCS lengths by either excluding the current character of `text1` or `text2`.
3. **Result**: The value at `dp[m][n]` gives the length of the longest common subsequence between the two strings.

### Example

For the strings "abcde" and "ace":
- The longest common subsequence is "ace" with a length of 3.

Feel free to ask if you have any questions or need further clarification!

## Longest Common Sequence

The Longest Common Subsequence (LCS) problem is a classic problem in computer science. The goal is to find the longest subsequence common to two sequences. A subsequence is a sequence that appears in the same relative order, but not necessarily consecutively.

### Problem Explanation

Given two strings, find the length of their longest common subsequence.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining a 2D array `dp` where `dp[i][j]` represents the length of the longest common subsequence of the first `i` characters of the first string and the first `j` characters of the second string.

### Java Implementation

Here's a Java implementation of the Longest Common Subsequence problem:

```java
public class LongestCommonSubsequence {

    public static int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];

        // Fill the dp array
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String text1 = "abcde";
        String text2 = "ace";

        int result = longestCommonSubsequence(text1, text2);
        System.out.println("Length of Longest Common Subsequence = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a 2D array `dp` where `dp[i][j]` represents the length of the longest common subsequence of the first `i` characters of `text1` and the first `j` characters of `text2`.
2. **Filling the DP Array**: We iterate through each character of both strings. If the characters are the same, the length of the LCS is incremented by 1 from the previous characters. If they are different, we take the maximum of the LCS lengths by either excluding the current character of `text1` or `text2`.
3. **Result**: The value at `dp[m][n]` gives the length of the longest common subsequence between the two strings.

### Example

For the strings "abcde" and "ace":
- The longest common subsequence is "ace" with a length of 3.

Feel free to ask if you have any questions or need further clarification!

## Longest Incresing Subsequence

The Longest Increasing Subsequence (LIS) problem involves finding the length of the longest subsequence in a given sequence such that all elements of the subsequence are sorted in increasing order. The subsequence does not need to be contiguous.

### Problem Explanation

Given an array of integers, find the length of the longest increasing subsequence.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining an array `dp` where `dp[i]` represents the length of the longest increasing subsequence that ends with the element at index `i`.

### Java Implementation

Here's a Java implementation of the Longest Increasing Subsequence problem:

```java
public class LongestIncreasingSubsequence {

    public static int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int[] dp = new int[nums.length];
        int maxLength = 1;

        // Initialize the dp array with 1s
        for (int i = 0; i < nums.length; i++) {
            dp[i] = 1;
        }

        // Fill the dp array
        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLength = Math.max(maxLength, dp[i]);
        }

        return maxLength;
    }

    public static void main(String[] args) {
        int[] nums = {10, 9, 2, 5, 3, 7, 101, 18};
        int result = lengthOfLIS(nums);
        System.out.println("Length of Longest Increasing Subsequence = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize an array `dp` where `dp[i]` represents the length of the longest increasing subsequence that ends with the element at index `i`. Each element is initialized to 1 because the minimum length of any increasing subsequence is 1 (the element itself).
2. **Filling the DP Array**: We iterate through the array. For each element `nums[i]`, we check all previous elements `nums[j]` (where `j < i`). If `nums[i]` is greater than `nums[j]`, it means `nums[i]` can extend the increasing subsequence that ends at `nums[j]`. We update `dp[i]` to be the maximum of `dp[i]` and `dp[j] + 1`.
3. **Result**: The maximum value in the `dp` array gives the length of the longest increasing subsequence.

### Example

For the array `[10, 9, 2, 5, 3, 7, 101, 18]`:
- The longest increasing subsequence is `[2, 3, 7, 101]` with a length of 4.

Feel free to ask if you have any questions or need further clarification!

## LPS

The Longest Palindromic Subsequence (LPS) problem involves finding the longest subsequence in a given sequence that reads the same forward and backward. Unlike substrings, subsequences are not required to occupy consecutive positions within the original string.

### Problem Explanation

Given a string, find the length of its longest palindromic subsequence.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining a 2D array `dp` where `dp[i][j]` represents the length of the longest palindromic subsequence in the substring from index `i` to `j`.

### Java Implementation

Here's a Java implementation of the Longest Palindromic Subsequence problem:

```java
public class LongestPalindromicSubsequence {

    public static int longestPalindromeSubseq(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];

        // Every single character is a palindrome of length 1
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

        // Fill the dp array
        for (int length = 2; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[0][n - 1];
    }

    public static void main(String[] args) {
        String s = "bbbab";
        int result = longestPalindromeSubseq(s);
        System.out.println("Length of Longest Palindromic Subsequence = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a 2D array `dp` where `dp[i][j]` represents the length of the longest palindromic subsequence in the substring from index `i` to `j`. Each single character is a palindrome of length 1, so we set `dp[i][i] = 1` for all `i`.
2. **Filling the DP Array**: We iterate through all possible lengths of substrings from 2 to `n`. For each substring, if the characters at the start and end of the substring are the same, the length of the LPS is `dp[i + 1][j - 1] + 2`. Otherwise, it is the maximum of `dp[i + 1][j]` and `dp[i][j - 1]`.
3. **Result**: The value at `dp[0][n - 1]` gives the length of the longest palindromic subsequence in the entire string.

### Example

For the string "bbbab":
- The longest palindromic subsequence is "bbbb" with a length of 4.

Feel free to ask if you have any questions or need further clarification!


## Longest Pallindromic Substring

The Longest Palindromic Substring (LPS) problem involves finding the longest substring in a given string that reads the same forward and backward.

### Problem Explanation

Given a string, find the longest palindromic substring within it.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining a 2D array `dp` where `dp[i][j]` represents whether the substring from index `i` to `j` is a palindrome.

### Java Implementation

Here's a Java implementation of the Longest Palindromic Substring problem:

```java
public class LongestPalindromicSubstring {

    public static String longestPalindrome(String s) {
        int n = s.length();
        if (n == 0) return "";

        boolean[][] dp = new boolean[n][n];
        int maxLength = 1;
        int start = 0;

        // All substrings of length 1 are palindromes
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }

        // Check for substrings of length 2
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                start = i;
                maxLength = 2;
            }
        }

        // Check for substrings of length greater than 2
        for (int length = 3; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    start = i;
                    maxLength = length;
                }
            }
        }

        return s.substring(start, start + maxLength);
    }

    public static void main(String[] args) {
        String s = "babad";
        String result = longestPalindrome(s);
        System.out.println("Longest Palindromic Substring = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a 2D array `dp` where `dp[i][j]` represents whether the substring from index `i` to `j` is a palindrome. We also initialize `maxLength` to 1 and `start` to 0 to keep track of the longest palindromic substring found so far.
2. **Single Character Substrings**: All substrings of length 1 are palindromes, so we set `dp[i][i] = true` for all `i`.
3. **Two Character Substrings**: We check for substrings of length 2. If the characters are the same, we set `dp[i][i + 1] = true` and update `start` and `maxLength`.
4. **Substrings of Length Greater Than 2**: We iterate through all possible lengths of substrings from 3 to `n`. For each substring, if the characters at the start and end of the substring are the same and the substring between them is a palindrome, we set `dp[i][j] = true` and update `start` and `maxLength`.
5. **Result**: The substring from `start` to `start + maxLength` gives the longest palindromic substring.

### Example

For the string "babad":
- The longest palindromic substring is "bab" or "aba".

Feel free to ask if you have any questions or need further clarification!

## Longest Valid Parenthesis

The "Longest Valid Parentheses" problem involves finding the length of the longest valid (well-formed) parentheses substring.

### Problem Explanation

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

### Approach

We can solve this problem using dynamic programming or a stack. Here, I'll provide the stack-based approach, which is intuitive and efficient.

### Java Implementation

Here's a Java implementation of the Longest Valid Parentheses problem using a stack:

```java
import java.util.Stack;

public class LongestValidParentheses {

    public static int longestValidParentheses(String s) {
        Stack<Integer> stack = new Stack<>();
        stack.push(-1); // Initialize stack with -1 to handle the base case
        int maxLength = 0;

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.isEmpty()) {
                    stack.push(i);
                } else {
                    maxLength = Math.max(maxLength, i - stack.peek());
                }
            }
        }

        return maxLength;
    }

    public static void main(String[] args) {
        String s = "(()))())(";
        int result = longestValidParentheses(s);
        System.out.println("Length of Longest Valid Parentheses = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a stack and push `-1` onto it to handle the base case where the valid substring starts from the beginning of the string. We also initialize `maxLength` to keep track of the longest valid parentheses substring found so far.
2. **Iterate Through the String**: We iterate through the string. For each character:
   - If it is `'('`, we push its index onto the stack.
   - If it is `')'`, we pop the top of the stack. If the stack becomes empty, we push the current index onto the stack. Otherwise, we calculate the length of the current valid substring by subtracting the index of the element at the top of the stack from the current index and update `maxLength` if this length is greater.
3. **Result**: The value of `maxLength` gives the length of the longest valid parentheses substring.

### Example

For the string "(()))())(":
- The longest valid parentheses substring is "(()))()" with a length of 4.

Feel free to ask if you have any questions or need further clarification!


## Minimum Path sum

The "Minimum Path Sum" problem involves finding the path from the top-left corner to the bottom-right corner of a grid that minimizes the sum of the numbers along the path. You can only move either down or right at any point in time.

### Problem Explanation

Given a `m x n` grid filled with non-negative numbers, find a path from the top-left to the bottom-right which minimizes the sum of all numbers along its path.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining a 2D array `dp` where `dp[i][j]` represents the minimum path sum to reach cell `(i, j)`.

### Java Implementation

Here's a Java implementation of the Minimum Path Sum problem:

```java
public class MinimumPathSum {

    public static int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];

        dp[0][0] = grid[0][0];

        // Initialize the first row
        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0] + grid[i][0];
        }

        // Initialize the first column
        for (int j = 1; j < n; j++) {
            dp[0][j] = dp[0][j - 1] + grid[0][j];
        }

        // Fill the dp array
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = grid[i][j] + Math.min(dp[i - 1][j], dp[i][j - 1]);
            }
        }

        return dp[m - 1][n - 1];
    }

    public static void main(String[] args) {
        int[][] grid = {
           1},
            {1, 5, 1},
            {4, 2, 1}
        };

        int result = minPathSum(grid);
        System.out.println("Minimum path sum = " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a 2D array `dp` where `dp[i][j]` represents the minimum path sum to reach cell `(i, j)`. The starting point `dp[0][0]` is initialized to `grid[0][0]`.
2. **First Row and Column**: We initialize the first row and first column because there is only one way to reach any cell in the first row (moving right) or the first column (moving down).
3. **Filling the DP Array**: We iterate through the grid starting from cell `(1, 1)`. For each cell `(i, j)`, the minimum path sum to reach it is the value of the cell itself plus the minimum of the path sums to reach the cell directly above it `(i-1, j)` and the cell directly to the left of it `(i, j-1)`.
4. **Result**: The value at `dp[m-1][n-1]` gives the minimum path sum from the top-left corner to the bottom-right corner.

### Example

For the grid:
```
[
  [1, 3, 1],
  [1, 5, 1],
  [4, 2, 1]
]
```
- The minimum path sum is `7` (1 → 3 → 1 → 1 → 1).

Feel free to ask if you have any questions or need further clarification!

## Climbing Stairs 

The "Climbing Stairs" problem is a classic dynamic programming problem. The goal is to determine the number of distinct ways to climb to the top of a staircase with `n` steps, given that you can either take one step or two steps at a time.

### Problem Explanation

Given `n` steps, you need to find the number of distinct ways to reach the top. 

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining an array `dp` where `dp[i]` represents the number of distinct ways to reach the `i`-th step.

### Java Implementation

Here's a Java implementation of the Climbing Stairs problem:

```java
public class ClimbingStairs {

    public static int climbStairs(int n) {
        if (n <= 1) {
            return 1;
        }

        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }

    public static void main(String[] args) {
        int n = 5;
        int result = climbStairs(n);
        System.out.println("Number of ways to climb " + n + " steps = " + result);
    }
}
```

### Explanation of the Code

1. **Base Cases**: If `n` is 0 or 1, there is only one way to climb the stairs (either stay at the ground or take one step).
2. **Initialize DP Array**: We initialize a `dp` array where `dp[i]` represents the number of distinct ways to reach the `i`-th step. We set `dp[0]` and `dp[1]` to 1 because there is only one way to reach the 0th and 1st steps.
3. **Fill DP Array**: We iterate from the 2nd step to the `n`-th step. For each step `i`, the number of ways to reach it is the sum of the ways to reach the `(i-1)`-th step and the `(i-2)`-th step.
4. **Result**: The value at `dp[n]` gives the number of distinct ways to reach the `n`-th step.

### Example

For `n = 5`:
- The number of ways to climb 5 steps is `8`.

Feel free to ask if you have any questions or need further clarification!

## Word break in Java

The "Word Break" problem involves determining if a given string can be segmented into a space-separated sequence of one or more dictionary words.

### Problem Explanation

Given a string `s` and a dictionary of words `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

### Dynamic Programming Approach

We can solve this problem using dynamic programming by maintaining a boolean array `dp` where `dp[i]` represents whether the substring `s[0...i-1]` can be segmented into dictionary words.

### Java Implementation

Here's a Java implementation of the Word Break problem:

```java
import java.util.*;

public class WordBreak {

    public static boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordSet = new HashSet<>(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[s.length()];
    }

    public static void main(String[] args) {
        String s = "leetcode";
        List<String> wordDict = Arrays.asList("leet", "code");

        boolean result = wordBreak(s, wordDict);
        System.out.println("Can the string \"" + s + "\" be segmented? " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a boolean array `dp` where `dp[i]` represents whether the substring `s[0...i-1]` can be segmented into dictionary words. We set `dp[0]` to `true` because an empty string can always be segmented.
2. **Fill DP Array**: We iterate through the string `s`. For each position `i`, we check all possible substrings `s[j...i-1]` (where `0 <= j < i`). If `dp[j]` is `true` and `s.substring(j, i)` is in the dictionary, we set `dp[i]` to `true` and break out of the inner loop.
3. **Result**: The value at `dp[s.length()]` gives whether the entire string `s` can be segmented into dictionary words.

### Example

For the string "leetcode" and the dictionary `["leet", "code"]`:
- The string can be segmented as "leet code", so the output is `true`.

Feel free to ask if you have any questions or need further clarification!

## Jump Game

The "Jump Game" problem involves determining if you can reach the last index of an array, given that each element in the array represents the maximum jump length at that position.

### Problem Explanation

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array. Each element in the array represents your maximum jump length at that position. Determine if you can reach the last index.

### Greedy Approach

A common and efficient approach to solve this problem is using a greedy algorithm. The idea is to keep track of the farthest index that can be reached and update it as you iterate through the array.

### Java Implementation

Here's a Java implementation of the Jump Game problem:

```java
public class JumpGame {

    public static boolean canJump(int[] nums) {
        int maxReach = 0;

        for (int i = 0; i < nums.length; i++) {
            if (i > maxReach) {
                return false;
            }
            maxReach = Math.max(maxReach, i + nums[i]);
        }

        return true;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        boolean result = canJump(nums);
        System.out.println("Can jump to the last index? " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We initialize a variable `maxReach` to keep track of the farthest index that can be reached.
2. **Iterate Through the Array**: We iterate through the array. For each index `i`:
   - If `i` is greater than `maxReach`, it means we cannot reach this index, so we return `false`.
   - Otherwise, we update `maxReach` to be the maximum of `maxReach` and `i + nums[i]`.
3. **Result**: If we complete the iteration without returning `false`, it means we can reach the last index, so we return `true`.

### Example

For the array `[2, 3, 1, 1, 4]`:
- You can jump from index 0 to index 1 (jump length 2), then from index 1 to index 4 (jump length 3). Therefore, the output is `true`.

Feel free to ask if you have any questions or need further clarification!

## Word Search 

The "Word Search" problem involves finding if a given word exists in a grid of characters. The word can be constructed from letters of sequentially adjacent cells, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

### Problem Explanation

Given a 2D board and a word, find if the word exists in the grid. The word can be constructed from letters of sequentially adjacent cells, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

### Depth-First Search (DFS) Approach

We can solve this problem using Depth-First Search (DFS) with backtracking. The idea is to start from each cell and try to find the word by exploring all possible paths.

### Java Implementation

Here's a Java implementation of the Word Search problem:

```java
public class WordSearch {

    public static boolean exist(char[][] board, String word) {
        int rows = board.length;
        int cols = board[0].length;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (dfs(board, word, i, j, 0)) {
                    return true;
                }
            }
        }

        return false;
    }

    private static boolean dfs(char[][] board, String word, int i, int j, int index) {
        if (index == word.length()) {
            return true;
        }

        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(index)) {
            return false;
        }

        char temp = board[i][j];
        board[i][j] = '#'; // Mark the cell as visited

        boolean found = dfs(board, word, i + 1, j, index + 1) ||
                        dfs(board, word, i - 1, j, index + 1) ||
                        dfs(board, word, i, j + 1, index + 1) ||
                        dfs(board, word, i, j - 1, index + 1);

        board[i][j] = temp; // Unmark the cell

        return found;
    }

    public static void main(String[] args) {
        char[][] board = {
            {'A', 'B', 'C', 'E'},
            {'S', 'F', 'C', 'S'},
            {'A', 'D', 'E', 'E'}
        };
        String word = "ABCCED";

        boolean result = exist(board, word);
        System.out.println("Does the word \"" + word + "\" exist in the board? " + result);
    }
}
```

### Explanation of the Code

1. **Initialization**: We iterate through each cell in the grid. For each cell, we start a DFS to check if we can find the word starting from that cell.
2. **DFS Function**: The `dfs` function checks if the current cell matches the current character of the word. If it does, it marks the cell as visited and recursively checks the neighboring cells. If the word is found, it returns `true`. Otherwise, it backtracks by unmarking the cell and continues the search.
3. **Result**: The `exist` function returns `true` if the word is found starting from any cell in the grid, otherwise it returns `false`.

###`
[
  ['A', 'B', 'C', 'E'],
  ['S', 'F', 'C', 'S'],
  ['A', 'D', 'E', 'E']
]
```
and the word "ABCCED":
- The word exists in the board, so the output is `true`.

Feel free to ask if you have any questions or need further clarification!

