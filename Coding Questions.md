## Phone Directory Search Directory

Sure! Let's break down the `PhoneDirectory` class step by step:

### Class Definition
```java
public class PhoneDirectory {
    private Map<String, String> directory;

    public PhoneDirectory() {
        directory = new HashMap<>();
    }
}
```
- **Class Declaration**: The `PhoneDirectory` class is defined as a public class.
- **Instance Variable**: A `HashMap` named `directory` is used to store the contacts, where the key is the contact name (a `String`) and the value is the phone number (also a `String`).
- **Constructor**: The constructor initializes the `directory` as a new `HashMap`.

### Adding a Contact
```java
public void addContact(String name, String phoneNumber) {
    directory.put(name, phoneNumber);
}
```
- **Method Declaration**: The `addContact` method takes two parameters: `name` and `phoneNumber`.
- **Adding to Directory**: The method adds the contact to the `directory` using the `put` method of the `HashMap`.

### Searching for a Contact
```java
public String searchContact(String name) {
    return directory.getOrDefault(name, "Contact not found");
}
```
- **Method Declaration**: The `searchContact` method takes one parameter: `name`.
- **Searching in Directory**: The method uses the `getOrDefault` method of the `HashMap` to retrieve the phone number associated with the given name. If the name is not found, it returns "Contact not found".

### Deleting a Contact
```java
public void deleteContact(String name) {
    if (directory.containsKey(name)) {
        directory.remove(name);
        System.out.println("Contact deleted: " + name);
    } else {
        System.out.println("Contact not found: " + name);
    }
}
```
- **Method Declaration**: The `deleteContact` method takes one parameter: `name`.
- **Checking Existence**: The method checks if the `directory` contains the given name using the `containsKey` method.
- **Removing from Directory**: If the name exists, it removes the contact using the `remove` method and prints a confirmation message. If the name does not exist, it prints "Contact not found".

### Main Method
```java
public static void main(String[] args) {
    PhoneDirectory phoneDirectory = new PhoneDirectory();
    phoneDirectory.addContact("Alice", "123-456-7890");
    phoneDirectory.addContact("Bob", "987-654-3210");

    System.out.println("Search for Alice: " + phoneDirectory.searchContact("Alice"));
    System.out.println("Search for Charlie: " + phoneDirectory.searchContact("Charlie"));

    phoneDirectory.deleteContact("Bob");
    System.out.println("Search for Bob: " + phoneDirectory.searchContact("Bob"));
}
```
- **Creating an Instance**: The `main` method creates an instance of the `PhoneDirectory` class.
- **Adding Contacts**: It adds two contacts, "Alice" and "Bob".
- **Searching Contacts**: It searches for "Alice" and "Charlie" (who is not in the directory).
- **Deleting a Contact**: It deletes "Bob" and then searches for "Bob" again to confirm the deletion.

This class provides a simple way to manage a phone directory with basic operations like adding, searching, and deleting contacts. If you have any questions or need further details, feel free to ask!

## K Closest Points to Origin

Sure! Here's a Java solution to find the K closest points to the origin using a max-heap (priority queue):

```java
import java.util.PriorityQueue;

public class KClosestPointsToOrigin {
    public static int[][] kClosest(int[][] points, int K) {
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> 
            Integer.compare(distance(b), distance(a))
        );

        for (int[] point : points) {
            maxHeap.offer(point);
            if (maxHeap.size() > K) {
                maxHeap.poll();
            }
        }

        int[][] result = new int[K][2];
        for (int i = 0; i < K; i++) {
            result[i] = maxHeap.poll();
        }

        return result;
    }

    private static int distance(int[] point) {
        return point[0] * point[0] + point[1] * point[1];
    }

    public static void main(String[] args) {
        int[][] points = {{1, 3}, {-2, 2}, {5, 8}, {0, 1}};
        int K = 2;
        int[][] closestPoints = kClosest(points, K);
        System.out.println("K Closest Points to Origin:");
        for (int[] point : closestPoints) {
            System.out.println("[" + point[0] + ", " + point[1] + "]");
        }
    }
}
```

This code defines a `KClosestPointsToOrigin` class with a method `kClosest` that finds the K closest points to the origin. The method uses a max-heap (priority queue) to keep track of the closest points. The `distance` method calculates the squared distance of a point from the origin.

If you have any questions or need further assistance, feel free to ask!

## Median of Subarrays of Specific Size

Sure! Here's a Java solution to find the median of all subarrays of a specific size `k` in an array. This solution uses a sliding window approach along with a balanced binary search tree to efficiently find the median:

```java
import java.util.*;

public class MedianOfSubarrays {
    public static List<Double> medianSlidingWindow(int[] nums, int k) {
        List<Double> result = new ArrayList<>();
        TreeSet<Integer> minHeap = new TreeSet<>((a, b) -> nums[a] != nums[b] ? Integer.compare(nums[a], nums[b]) : a - b);
        TreeSet<Integer> maxHeap = new TreeSet<>((a, b) -> nums[a] != nums[b] ? Integer.compare(nums[b], nums[a]) : b - a);

        for (int i = 0; i < nums.length; i++) {
            if (i >= k) {
                if (!minHeap.remove(i - k)) {
                    maxHeap.remove(i - k);
                }
            }

            maxHeap.add(i);
            minHeap.add(maxHeap.pollFirst());

            if (minHeap.size() > maxHeap.size()) {
                maxHeap.add(minHeap.pollFirst());
            }

            if (i >= k - 1) {
                if (k % 2 == 0) {
                    result.add(((double) nums[minHeap.first()] + nums[maxHeap.first()]) / 2);
                } else {
                    result.add((double) nums[maxHeap.first()]);
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        List<Double> medians = medianSlidingWindow(nums, k);
        System.out.println("Medians of subarrays of size " + k + ": " + medians);
    }
}
```

This code defines a `MedianOfSubarrays` class with a method `medianSlidingWindow` that calculates the median of all subarrays of size `k` in an array. The method uses two balanced binary search trees (min-heap and max-heap) to maintain the elements of the current window and efficiently find the median.

If you have any questions or need further assistance, feel free to ask!

## Missing Number in java
Sure! Here's a Java solution to find the missing number in an array containing `n` distinct numbers taken from the range `0` to `n`:

```java
public class MissingNumber {
    public static int missingNumber(int[] nums) {
        int n = nums.length;
        int expectedSum = n * (n + 1) / 2;
        int actualSum = 0;

        for (int num : nums) {
            actualSum += num;
        }

        return expectedSum - actualSum;
    }

    public static void main(String[] args) {
        int[] nums = {3, 0, 1};
        int missing = missingNumber(nums);
        System.out.println("The missing number is: " + missing);
    }
}
```

This code defines a `MissingNumber` class with a method `missingNumber` that calculates the missing number in an array. The method uses the formula for the sum of the first `n` natural numbers to find the expected sum and then subtracts the actual sum of the array elements to find the missing number.

If you have any questions or need further assistance, feel free to ask!

## Crazy Numbers Pattern in java

Creating a "Crazy Numbers Pattern" can be a fun exercise in Java. Let's assume you want to generate a pattern where numbers are printed in a specific crazy or interesting format. Here's an example of a pattern you might want to generate:

### Example Pattern:
```
1
2 3
4 5 6
7 8 9 10
11 12 13 14 15
```

### Code Example:

```java
public class CrazyNumbersPattern {
    public static void main(String[] args) {
        int n = 5; // Number of rows
        printCrazyNumbersPattern(n);
    }

    public static void printCrazyNumbersPattern(int n) {
        int number = 1;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(number + " ");
                number++;
            }
            System.out.println();
        }
    }
}
```

### Explanation:
1. **Main Method:** Sets the number of rows (`n`) for the pattern and calls the `printCrazyNumbersPattern` method.
2. **printCrazyNumbersPattern Method:**
   - **Initialize Number:** Starts with the number 1.
   - **Outer Loop (Rows):** Iterates through each row from 1 to `n`.
   - **Inner Loop (Columns):** Iterates through each column in the current row, printing the current number and incrementing it.
   - **New Line:** Moves to the next line after completing each row.

This code will generate a pattern where each row contains an increasing number of integers, starting from 1 and continuing sequentially.

Feel free to modify the pattern or the number of rows to create your own crazy number patterns! If you have any specific pattern in mind or need further assistance, let me know!

## Fenwick Tree Problem 

A Fenwick Tree, also known as a Binary Indexed Tree (BIT), is a data structure that provides efficient methods for cumulative frequency tables. It supports point updates and prefix sum queries in logarithmic time.

### Problem Statement:
Implement a Fenwick Tree to support the following operations:
1. **Update:** Add a value to an element.
2. **Query:** Get the prefix sum up to a given index.

### Code Example:

```java
public class FenwickTree {
    private int[] fenwickTree;

    public FenwickTree(int size) {
        fenwickTree = new int[size + 1];
    }

    // Update the Fenwick Tree with value at index
    public void update(int index, int value) {
        index++; // Fenwick Tree is 1-indexed
        while (index < fenwickTree.length) {
            fenwickTree[index] += value;
            index += index & -index;
        }
    }

    // Query the prefix sum up to index
    public int query(int index) {
        index++; // Fenwick Tree is 1-indexed
        int sum = 0;
        while (index > 0) {
            sum += fenwickTree[index];
            index -= index & -index;
        }
        return sum;
    }

    public static void main(String[] args) {
        int[] arr = {1, 7, 3, 0, 7, 8, 3, 2, 6, 2};
        FenwickTree fenwickTree = new FenwickTree(arr.length);

        // Build the Fenwick Tree
        for (int i = 0; i < arr.length; i++) {
            fenwickTree.update(i, arr[i]);
        }

        // Query the prefix sum up to index 5
        System.out.println("Prefix sum up to index 5: " + fenwickTree.query(5));

        // Update the value at index 3
        fenwickTree.update(3, 5);
        System.out.println("Prefix sum up to index 5 after update: " + fenwickTree.query(5));
    }
}
```

### Explanation:
1. **FenwickTree Class:**
   - **Constructor:** Initializes the Fenwick Tree array with a size of `size + 1` to handle 1-based indexing.
   - **update Method:** Adds a value to an element at a given index and updates the tree accordingly.
   - **query Method:** Computes the prefix sum up to a given index.

2. **Main Method:**
   - **Initialize Array:** Creates an example array.
   - **Build Tree:** Updates the Fenwick Tree with the values from the array.
   - **Query Sum:** Queries the prefix sum up to a specific index.
   - **Update Value:** Updates a value in the array and queries the prefix sum again to reflect the change.

This implementation provides efficient updates and queries, making it suitable for problems involving cumulative frequency tables or range queries.

Feel free to test this code and let me know if you have any questions or need further assistance!

## AVL tree
An AVL tree is a self-balancing binary search tree where the difference between the heights of the left and right subtrees of any node is at most one. This property ensures that the tree remains balanced, providing efficient operations for insertion, deletion, and lookup.

### Key Operations:
1. **Insertion:** Insert a node and then balance the tree if necessary.
2. **Deletion:** Remove a node and then balance the tree if necessary.
3. **Rotations:** Perform rotations (left, right, left-right, right-left) to maintain balance.

### Code Example:

```java
class AVLTree {
    class Node {
        int key, height;
        Node left, right;

        Node(int d) {
            key = d;
            height = 1;
        }
    }

    private Node root;

    // Get the height of the node
    private int height(Node N) {
        if (N == null)
            return 0;
        return N.height;
    }

    // Get the balance factor of the node
    private int getBalance(Node N) {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
    }

    // Right rotate subtree rooted with y
    private Node rightRotate(Node y) {
        Node x = y.left;
        Node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = Math.max(height(y.left), height(y.right)) + 1;
        x.height = Math.max(height(x.left), height(x.right)) + 1;

        // Return new root
        return x;
    }

    // Left rotate subtree rooted with x
    private Node leftRotate(Node x) {
        Node y = x.right;
        Node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        // Return new root
        return y;
    }

    // Insert a node
    public void insert(int key) {
        root = insertRec(root, key);
    }

    private Node insertRec(Node node, int key) {
        if (node == null)
            return new Node(key);

        if (key < node.key)
            node.left = insertRec(node.left, key);
        else if (key > node.key)
            node.right = insertRec(node.right, key);
        else
            return node;

        // Update height of this ancestor node
        node.height = 1 + Math.max(height(node.left), height(node.right));

        // Get the balance factor of this ancestor node to check whether this node became unbalanced
        int balance = getBalance(node);

        // If the node becomes unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        return node;
    }

    // Print the tree
    public void preOrder() {
        preOrderRec(root);
    }

    private void preOrderRec(Node node) {
        if (node != null) {
            System.out.print(node.key + " ");
            preOrderRec(node.left);
            preOrderRec(node.right);
        }
    }

    public static void main(String[] args) {
        AVLTree tree = new AVLTree();

        tree.insert(10);
        tree.insert(20);
        tree.insert(30);
        tree.insert(40);
        tree.insert(50);
        tree.insert(25);

        System.out.println("Preorder traversal of the constructed AVL tree is:");
        tree.preOrder();
    }
}
```

### Explanation:
1. **Node Class:** Defines the structure of a tree node with key, height, left, and right pointers.
2. **height Method:** Returns the height of a node.
3. **getBalance Method:** Calculates the balance factor of a node.
4. **Rotations:** Implements right and left rotations to maintain balance.
5. **insert Method:** Inserts a node into the AVL tree and balances the tree if necessary.
6. **preOrder Method:** Prints the tree in pre-order traversal.

This implementation ensures that the AVL tree remains balanced after each insertion, providing efficient operations.

Feel free to test this code and let me know if you have any questions or need further assistance!

## LCM and GCD in java
To calculate the Least Common Multiple (LCM) and Greatest Common Divisor (GCD) in Java, you can use the Euclidean algorithm for GCD and then derive the LCM using the relationship between GCD and LCM.

### GCD (Greatest Common Divisor):
The GCD of two numbers is the largest number that divides both of them without leaving a remainder. The Euclidean algorithm is an efficient way to compute the GCD.

### LCM (Least Common Multiple):
The LCM of two numbers is the smallest number that is a multiple of both. The relationship between GCD and LCM is given by:
\[ \text{LCM}(a, b) = \frac{|a \times b|}{\text{GCD}(a, b)} \]

### Code Example:

```java
public class LCMAndGCD {
    public static void main(String[] args) {
        int num1 = 12;
        int num2 = 18;

        int gcd = findGCD(num1, num2);
        int lcm = findLCM(num1, num2, gcd);

        System.out.println("GCD of " + num1 + " and " + num2 + " is: " + gcd);
        System.out.println("LCM of " + num1 + " and " + num2 + " is: " + lcm);
    }

    // Method to find GCD using Euclidean algorithm
    public static int findGCD(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    // Method to find LCM using the relationship between GCD and LCM
    public static int findLCM(int a, int b, int gcd) {
        return Math.abs(a * b) / gcd;
    }
}
```

### Explanation:
1. **Main Method:**
   - Defines two numbers (`num1` and `num2`).
   - Calls `findGCD` to compute the GCD of the two numbers.
   - Calls `findLCM` to compute the LCM using the GCD.
   - Prints the results.

2. **findGCD Method:**
   - Uses the Euclidean algorithm to find the GCD of two numbers.
   - Continues to compute the remainder until `b` becomes 0, at which point `a` is the GCD.

3. **findLCM Method:**
   - Uses the relationship between GCD and LCM to compute the LCM.
   - Calculates the LCM as \(\frac{|a \times b|}{\text{GCD}(a, b)}\).

This code efficiently computes both the GCD and LCM of two numbers. Feel free to test it with different values and let me know if you have any questions or need further assistance!

## Swap array without using 3rd variable

Swapping elements in an array without using a third variable can be done using arithmetic operations or bitwise XOR. Here's how you can do it in Java:

### Using Arithmetic Operations:
You can swap two elements by adding and subtracting their values.

```java
public class SwapArrayElements {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int i = 1; // Index of the first element to swap
        int j = 3; // Index of the second element to swap

        System.out.println("Before swap: " + arr[i] + ", " + arr[j]);
        swapUsingArithmetic(arr, i, j);
        System.out.println("After swap: " + arr[i] + ", " + arr[j]);
    }

    public static void swapUsingArithmetic(int[] arr, int i, int j) {
        arr[i] = arr[i] + arr[j];
        arr[j] = arr[i] - arr[j];
        arr[i] = arr[i] - arr[j];
    }
}
```

### Using Bitwise XOR:
You can also swap two elements using the XOR bitwise operator.

```java
public class SwapArrayElements {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int i = 1; // Index of the first element to swap
        int j = 3; // Index of the second element to swap

        System.out.println("Before swap: " + arr[i] + ", " + arr[j]);
        swapUsingXOR(arr, i, j);
        System.out.println("After swap: " + arr[i] + ", " + arr[j]);
    }

    public static void swapUsingXOR(int[] arr, int i, int j) {
        arr[i] = arr[i] ^ arr[j];
        arr[j] = arr[i] ^ arr[j];
       [i] = arr[i] ^ arr[j];
    }
}
```

### Explanation:
1. **Using Arithmetic Operations:**
   - Add the values of the two elements and store the result in the first element.
   - Subtract the second element from the first element and store the result in the second element.
   - Subtract the second element (now holding the original value of the first element) from the first element to get the original value of the second element.

2. **Using Bitwise XOR:**
   - XOR the values of the two elements and store the result in the first element.
   - XOR the first element (now holding the XOR result) with the second element to get the original value of the first element.
   - XOR the first element (now holding the original value of the second element) with the second element to get the original value of the first element.

Both methods effectively swap the elements without using a third variable. Feel free to test these methods and let me know if you have any questions or need further assistance!

## Reverse numbers
Reversing a number mathematically in Java involves extracting the digits of the number one by one and constructing the reversed number. Here's a simple approach to achieve this:

### Code Example:

```java
public class ReverseNumber {
    public static void main(String[] args) {
        int num = 12345;
        int reversed = reverseNumber(num);
        System.out.println("Original number: " + num);
        System.out.println("Reversed number: " + reversed);
    }

    public static int reverseNumber(int num) {
        int reversed = 0;
        while (num != 0) {
            int digit = num % 10; // Extract the last digit
            reversed = reversed * 10 + digit; // Append the digit to the reversed number
            num /= 10; // Remove the last digit from the original number
        }
        return reversed;
    }
}
```

### Explanation:
1. **Main Method:**
   - Defines an example number (`num`).
   - Calls the `reverseNumber` method to reverse the number.
   - Prints the original and reversed numbers.

2. **reverseNumber Method:**
   - **Initialize Reversed:** Starts with `reversed` set to 0.
   - **Extract Digits:** Uses the modulus operator (`%`) to extract the last digit of the number.
   - **Construct Reversed Number:** Multiplies the current `reversed` number by 10 and adds the extracted digit to it.
   - **Remove Last Digit:** Uses integer division (`/`) to remove the last digit from the original number.
   - **Loop Until Zero:** Continues the process until the original number becomes 0.

This method efficiently reverses the digits of the number using basic arithmetic operations. Feel free to test this code with different numbers and let me know if you have any questions or need further assistance!


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


## Product of Array Except Self

Sure! The "Product of Array Except Self" problem requires you to return an array such that each element at index `i` of the array is the product of all the numbers in the original array except the one at `i`. Here's a Java solution that solves this problem without using division and in O(n) time complexity:

```java
public class ProductOfArrayExceptSelf {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];

        // Initialize the result array with 1s
        for (int i = 0; i < n; i++) {
            result[i] = 1;
        }

        // Calculate left products
        int leftProduct = 1;
        for (int i = 0; i < n; i++) {
            result[i] *= leftProduct;
            leftProduct *= nums[i];
        }

        // Calculate right products
        int rightProduct = 1;
        for (int i = n - 1; i >= 0; i--) {
            result[i] *= rightProduct;
            rightProduct *= nums[i];
        }

        return result;
    }

    public static void main(String[] args) {
        ProductOfArrayExceptSelf solution = new ProductOfArrayExceptSelf();
        int[] nums = {1, 2, 3, 4};
        int[] result = solution.productExceptSelf(nums);
        System.out.print("Product of array except self: ");
        for (int num : result) {
            System.out.print(num + " ");
        }
        // Output: 24 12 8 6
    }
}
```

This code uses two passes to calculate the product of all elements except the current one. The first pass calculates the product of all elements to the left of each element, and the second pass calculates the product of all elements to the right of each element. The result array is updated in place to store the final product.

Feel free to ask if you have any questions or need further assistance!

## Maximum Subarray

The "Maximum Subarray" problem involves finding the contiguous subarray within a one-dimensional array of numbers that has the largest sum. This is a classic problem that can be efficiently solved using Kadane's Algorithm.

Here's a Java solution for finding the maximum subarray sum:

```java
public class MaximumSubarray {
    public int maxSubArray(int[] nums) {
        int maxSoFar = nums[0];
        int maxEndingHere = nums[0];

        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }

        return maxSoFar;
    }

    public static void main(String[] args) {
        MaximumSubarray solution = new MaximumSubarray();
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum subarray sum: " + solution.maxSubArray(nums)); // Output: 6
    }
}
```

This code uses Kadane's Algorithm, which iterates through the array while maintaining the maximum sum of the subarray ending at the current position (`maxEndingHere`). It also keeps track of the overall maximum sum found so far (`maxSoFar`).

Feel free to ask if you have any questions or need further assistance!

## Perfect Squares

Sure! Here's a Java solution to find the least number of perfect square numbers that sum up to a given number `n` using dynamic programming:

```java
import java.util.Arrays;

public class PerfectSquares {
    public static int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j * j <= i; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }

        return dp[n];
    }

    public static void main(String[] args) {
        int n = 12;
        int result = numSquares(n);
        System.out.println("Least number of perfect squares for " + n + " is: " + result);
    }
}
```

This code defines a `PerfectSquares` class with a method `numSquares` that calculates the least number of perfect square numbers that sum up to a given number `n`. The method uses dynamic programming to build up the solution, where `dp[i]` represents the least number of perfect squares that sum up to `i`.

If you have any questions or need further assistance, feel free to ask!

## Partition Equal Subset Sum

Sure! Here's a Java solution to determine if a given array can be partitioned into two subsets such that the sum of elements in both subsets is equal. This problem can be solved using dynamic programming:

```java
public class PartitionEqualSubsetSum {
    public static boolean canPartition(int[] nums) {
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }

        // If the total sum is odd, it's not possible to partition it into two equal subsets
        if (totalSum % 2 != 0) {
            return false;
        }

        int target = totalSum / 2;
        boolean[] dp = new boolean[target + 1];
        dp[0] = true;

        for (int num : nums) {
            for (int j = target; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp[target];
    }

    public static void main(String[] args) {
        int[] nums = {1, 5, 11, 5};
        boolean result = canPartition(nums);
        System result);
    }
}
```

This code defines a `PartitionEqualSubsetSum` class with a method `canPartition` that determines if the array can be partitioned into two subsets with equal sum. The method uses dynamic programming to keep track

## Maximum Product Subarray

The "Maximum Product Subarray" problem involves finding the contiguous subarray within a one-dimensional array of numbers that has the largest product. This problem can be solved using a dynamic programming approach.

Here's a Java solution for finding the maximum product subarray:

```java
public class MaximumProductSubarray {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int maxProduct = nums[0];
        int minProduct = nums[0];
        int result = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {
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
        MaximumProductSubarray solution = new MaximumProductSubarray();
        int[] nums = {2, 3, -2, 4};
        System.out.println("Maximum product subarray: " + solution.maxProduct(nums)); // Output: 6

        nums = {-2, 0, -1};
        System.out.println("Maximum product subarray: " + solution.maxProduct(nums)); // Output: 0
    }
}
```

This code keeps track of the maximum and minimum products up to the current position, as the minimum product can become the maximum product when multiplied by a negative number. It iterates through the array, updating the maximum and minimum products and the result accordingly.

Feel free to ask if you have any questions or need further assistance!

## Majority Element

The "Majority Element" problem involves finding the element that appears more than half the time in a given array. This can be efficiently solved using the Boyer-Moore Voting Algorithm.

Here's a Java solution for finding the majority element:

```java
public class MajorityElement {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }

    public static void main(String[] args) {
        MajorityElement solution = new MajorityElement();
        int[] nums = {3, 2, 3};
        System.out.println("Majority element: " + solution.majorityElement(nums)); // Output: 3

        nums = new int[]{2, 2, 1, 1, 1, 2, 2};
        System.out.println("Majority element: " + solution.majorityElement(nums)); // Output: 2
    }
}
```

This code uses the Boyer-Moore Voting Algorithm, which maintains a count that is incremented or decremented based on whether the current element matches the candidate. When the count reaches zero, the candidate is updated to the current element. The final candidate is the majority element.

Feel free to ask if you have any questions or need further assistance!


## Roman to Integer

Sure! Converting a Roman numeral to an integer involves mapping each Roman numeral character to its corresponding integer value and then processing the string from left to right. If a smaller value precedes a larger value, you subtract the smaller value; otherwise, you add the value.

Here's a Java solution to convert a Roman numeral to an integer:

```java
import java.util.HashMap;
import java.util.Map;

public class RomanToInteger {
    public int romanToInt(String s) {
        Map<Character, Integer> romanMap = new HashMap<>();
        romanMap.put('I', 1);
        romanMap.put('V', 5);
        romanMap.put('X', 10);
        romanMap.put('L', 50);
        romanMap.put('C', 100);
        romanMap.put('D', 500);
        romanMap.put('M', 1000);

        int total = 0;
        int prevValue = 0;

        for (int i = s.length() - 1; i >= 0; i--) {
            int currentValue = romanMap.get(s.charAt(i));
            if (currentValue < prevValue) {
                total -= currentValue;
            } else {
                total += currentValue;
            }
            prevValue = currentValue;
        }

        return total;
    }

    public static void main(String[] args) {
        RomanToInteger solution = new RomanToInteger();
        String roman = "MCMXCIV";
        System.out.println("Integer value: " + solution.romanToInt(roman)); // Output: 1994
    }
}
```

This code uses a hash map to store the integer values of Roman numeral characters. It then iterates through the string from right to left, adding or subtracting the values based on the rules of Roman numerals.

Feel free to ask if you have any questions or need further assistance!

## Integer to Roman

Sure! Converting an integer to a Roman numeral involves mapping integer values to their corresponding Roman numeral symbols and constructing the numeral by repeatedly subtracting the largest possible values.

Here's a Java solution to convert an integer to a Roman numeral:

```java
public class IntegerToRoman {
    public String intToRoman(int num) {
        String[] thousands = {"", "M", "MM", "MMM"};
        String[] hundreds = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String[] tens = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String[] ones = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};

        return thousands[num / 1000] +
               hundreds[(num % 1000) / 100] +
               tens[(num % 100) / 10] +
               ones[num % 10];
    }

    public static void main(String[] args) {
        IntegerToRoman solution = new IntegerToRoman();
        int num = 1994;
        System.out.println("Roman numeral: " + solution.intToRoman(num)); // Output: MCMXCIV
    }
}
```

This code uses arrays to store the Roman numeral symbols for thousands, hundreds, tens, and ones. It then constructs the Roman numeral by concatenating the appropriate symbols based on the value of the input number.

Feel free to ask if you have any questions or need further assistance!

## 2 Sum

Sure! The "Two Sum" problem involves finding two numbers in an array that add up to a specific target sum. Here's a Java solution using a hash map to achieve this in O(n) time complexity:

```java
import java.util.HashMap;
import java.util.Map;

public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
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
        TwoSum solution = new TwoSum();
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        int[] result = solution.twoSum(nums, target);
        System.out.println("Indices: " + result[0] + ", " + result[1]); // Output: Indices: 0, 1
    }
}
```

This code uses a hash map to store the indices of the elements as it iterates through the array. For each element, it checks if the complement (target - current element) exists in the map. If it does, it returns the indices of the two elements.

Feel free to ask if you have any questions or need further assistance!

## 3 sum

Sure! The "3 Sum" problem involves finding all unique triplets in an array that sum up to zero. Here's a Java solution using sorting and the two-pointer technique:

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ThreeSum {
    public List<List<Integer>> threeSum(int[] nums) {
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
        ThreeSum solution = new ThreeSum();
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> result = solution.threeSum(nums);
        System.out.println("Triplets that sum to zero: " + result); // Output: [[-1, -1, 2], [-1, 0, 1]]
    }
}
```

This code first sorts the array and then uses a for loop to iterate through the elements. For each element, it uses two pointers (`left` and `right`) to find pairs that sum up to the negative of the current element. It also skips duplicate elements to ensure that the result contains only unique triplets.

Feel free to ask if you have any questions or need further assistance!


## 4 sum

Sure! The "4 Sum" problem involves finding all unique quadruplets in an array that sum up to a given target. Here's a Java solution using sorting and the two-pointer technique:

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class FourSum {
    public List<List<Integer>> fourSum(int[] nums, int target) {
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
                    if (sum < target) {
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
        FourSum solution = new FourSum();
        int[] nums = {1, 0, -1, 0, -2, 2};
        int target = 0;
        List<List<Integer>> result = solution.fourSum(nums, target);
        sum to target: " + result); // Output: [[-2, -1, 1, 2], [-2, 0, 0, 2], [-1, 0, 0, 1]]
    }
}
```

This code first sorts the array and then uses nested loops to iterate through the elements. For each pair of elements, it uses two pointers (`left` and `right`) to find pairs that sum up to the target minus the sum of the current pair. It also skips duplicate elements to ensure that the result contains only unique quadruplets.

Feel free to ask if you have any questions or need further assistance!

## Trapping Rain Water

Sure, I can help with that! Trapping rain water is a common coding problem where you need to find the amount of water that can be trapped after raining, given an array of non-negative integers representing the height of bars in a histogram.

Here's a simple Java solution using the two-pointer technique:

```java
public class TrappingRainWater {
    public int trap(int[] height) {
        if (height == null || height.length == 0) {
            return 0;
        }

        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int waterTrapped = 0;

        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    waterTrapped += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    waterTrapped += rightMax - height[right];
                }
                right--;
            }
        }

        return waterTrapped;
    }

    public static void main(String[] args) {
        TrappingRainWater solution = new TrappingRainWater();
        int[] height = {0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1};
        System.out.println("Water trapped: " + solution.trap(height)); // Output: 6
    }
}
```

This code initializes two pointers, `left` and `right`, at the beginning and end of the array, respectively. It then iterates through the array, updating the maximum heights seen so far from both ends and calculating the trapped water based on the difference between the current height and the maximum height.

Feel free to ask if you have any questions or need further clarification!


## 4 Sum

Sure! The "4 Sum" problem involves finding all unique quadruplets in an array that sum up to a given target. Here's a Java solution using sorting and the two-pointer technique:

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class FourSum {
    public List<List<Integer>> fourSum(int[] nums, int target) {
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
        FourSum solution = new FourSum();
        int[] nums = {1, 0, -1, 0, -2, 2};
        int target = 0;
        List<List<Integer>> result = solution.fourSum(nums, target);
       ruplets that sum to target: " + result); // Output: [[-2, -1, 1, 2], [-2, 0, 0, 2], [-1, 0, 0, 1]]
    }
}
```

This code first sorts the array and then uses nested loops to iterate through the elements. For each pair of elements, it uses two pointers (`left` and `right`) to find pairs that sum up to the target minus the sum of the current pair. It also skips duplicate elements to ensure that the result contains only unique quadruplets.

Feel free to ask if you have any questions or need further assistance!

## Merge Sorted Array

## Sort 0 1 2 

Sure! Sorting an array containing only 0s, 1s, and 2s can be efficiently done using the Dutch National Flag algorithm. This algorithm sorts the array in a single pass with O(n) time complexity.

Here's a Java solution to sort an array of 0s, 1s, and 2s:

```java
public class SortColors {
    public void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length - 1;

        while (mid <= high) {
            switch (nums[mid]) {
                case 0:
                    swap(nums, low++, mid++);
                    break;
                case 1:
                    mid++;
                    break;
                case 2:
                    swap(nums, mid, high--);
                    break;
            }
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    public static void main(String[] args) {
        SortColors solution = new SortColors();
        int[] nums = {2, 0, 2, 1, 1, 0};
        solution.sortColors(nums);
        System.out.print("Sorted array: ");
        for (int num : nums) {
            System.out.print(num + " ");
        }
        // Output: 0 0 1 1 2 2
    }
}
```

This code uses three pointers: `low`, `mid`, and `high`. The `low` pointer tracks the position of the next 0, the `mid` pointer scans through the array, and the `high` pointer tracks the position of the next 2. The algorithm swaps elements to ensure that all 0s are at the beginning, all 1s are in the middle, and all 2s are at the end.

Feel free to ask if you have any questions or need further assistance!

## Move Zeros

Sure! The "Move Zeros" problem involves moving all zeros in an array to the end while maintaining the relative order of the non-zero elements. Here's a Java solution to achieve this in O(n) time complexity:

```java
public class MoveZeros {
    public void moveZeroes(int[] nums) {
        int lastNonZeroFoundAt = 0;

        // Move all non-zero elements to the beginning of the array
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[lastNonZeroFoundAt++] = nums[i];
            }
        }

        // Fill the remaining positions with zeros
        for (int i = lastNonZeroFoundAt; i < nums.length; i++) {
            nums[i] = 0;
        }
    }

    public static void main(String[] args) {
        MoveZeros solution = new MoveZeros();
        int[] nums = {0, 1, 0, 3, 12};
        solution.moveZeroes(nums);
        System.out.print("Array after moving zeros: ");
        for (int num : nums) {
            System.out.print(num + " ");
        }
        // Output: 1 3 12 0 0
    }
}
```

This code uses a two-pass approach. In the first pass, it moves all non-zero elements to the beginning of the array. In the second pass, it fills the remaining positions with zeros.

Feel free to ask if you have any questions or need further assistance!

## Move Positive and Negative

Sure! If you want to move all positive numbers to one side and all negative numbers to the other side of an array, you can use a two-pointer approach. Here's a Java solution to achieve this:

```java
public class MovePositiveNegative {
    public void movePositiveNegative(int[] nums) {
        int left = 0, right = nums.length - 1;

        while (left < right) {
            // Move the left pointer until we find a positive number
            while (left < right && nums[left] < 0) {
                left++;
            }

            // Move the right pointer until we find a negative number
            while (left < right && nums[right] >= 0) {
                right--;
            }

            // Swap the positive number at left with the negative number at right
            if (left < right) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
            }
        }
    }

    public static void main(String[] args) {
        MovePositiveNegative solution = new MovePositiveNegative();
        int[] nums = {-1, 2, -3, 4, -5, 6};
        solution.movePositiveNegative(nums);
        System.out.print("Array after moving positives and negatives: ");
        for (int num : nums) {
            System.out.print(num + " ");
        }
        // Output: -1 -5 -3 4 2 6
    }
}
```

This code uses two pointers, `left` and `right`, to scan the array from both ends. The `left` pointer moves until it finds a positive number, and the `right` pointer moves until it finds a negative number. When both pointers find the respective numbers, they are swapped.

Feel free to ask if you have any questions or need further assistance!

## Valid Palindrome

Sure! A valid palindrome is a string that reads the same forward and backward, ignoring non-alphanumeric characters and case differences. Here's a simple Java solution to check if a given string is a valid palindrome:

```java
public class ValidPalindrome {
    public boolean isPalindrome(String s) {
        if (s == null) {
            return false;
        }

        int left = 0, right = s.length() - 1;
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }
            left++;
            right--;
        }

        return true;
    }

    public static void main(String[] args) {
        ValidPalindrome solution = new ValidPalindrome();
        String s = "A man, a plan, a canal: Panama";
        System.out.println("Is palindrome: " + solution.isPalindrome(s)); // Output: true

        s = "race a car";
        System.out.println("Is palindrome: " + solution.isPalindrome(s)); // Output: false
    }
}
```

This code uses two pointers, `left` and `right`, to traverse the string from both ends. It skips non-alphanumeric characters and compares the remaining characters in a case-insensitive manner.

Feel free to ask if you have any questions or need further assistance!


## Sliding Window Maximum

Sure! The "Sliding Window Maximum" problem involves finding the maximum value in each sliding window of size `k` in a given array of integers. Here's a Java solution using a deque to achieve this efficiently:

```java
import java.util.Deque;
import java.util.LinkedList;

public class SlidingWindowMaximum {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }

        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> deque = new LinkedList<>();

        for (int i = 0; i < n; i++) {
            // Remove elements not within the sliding window
            if (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }

            // Remove elements smaller than the current element from the deque
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }

            // Add the current element's index to the deque
            deque.offerLast(i);

            // The front of the deque contains the index of the maximum element for the current window
            if (i >= k - 1) {
                result[i - k + 1] = nums[deque.peekFirst()];
            }
        }

        return result;
    }

    public static void main(String[] args) {
        SlidingWindowMaximum solution = new SlidingWindowMaximum();
        int[] nums = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        int[] result = solution.maxSlidingWindow(nums, k);
        System.out.print("Sliding window maximums: ");
        for (int num : result) {
            System.out.print(num + " ");
        }
        // Output: 3 3 5 5 6 7
    }
}
```

This code uses a deque to store the indices of elements in the current window. The deque is maintained such that the maximum element is always at the front. As the window slides, elements that are out of the window's range are removed from the deque, and elements smaller than the current element are also removed to ensure the deque contains only useful elements.

Feel free to ask if you have any questions or need further assistance!

## Maximum Sum Subarray of Size K
Sure! The "Maximum Sum Subarray of Size K" problem involves finding the maximum sum of a subarray of size `k` in a given array of integers. Here's a Java solution using the sliding window technique:

```java
public class MaximumSumSubarrayOfSizeK {
    public int maxSumSubarray(int[] nums, int k) {
        if (nums == null || nums.length < k) {
            throw new IllegalArgumentException("Invalid input");
        }

        int maxSum = 0;
        int windowSum = 0;

        // Calculate the sum of the first window
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }

        maxSum = windowSum;

        // Slide the window over the array
        for (int i = k; i < nums.length; i++) {
            windowSum += nums[i] - nums[i - k];
            maxSum = Math.max(maxSum, windowSum);
        }

        return maxSum;
    }

    public static void main(String[] args) {
        MaximumSumSubarrayOfSizeK solution = new MaximumSumSubarrayOfSizeK();
        int[] nums = {2, 1, 5, 1, 3, 2};
        int k = 3;
        System.out.println("Maximum sum of subarray of size " + k + ": " + solution.maxSumSubarray(nums, k)); // Output: 9
    }
}
```

This code first calculates the sum of the initial window of size `k`. Then, it slides the window over the array by adding the next element and subtracting the element that is left behind. The maximum sum is updated accordingly.

Feel free to ask if you have any questions or need further assistance!

## Minimum Window Substring

Sure! The "Minimum Window Substring" problem involves finding the smallest substring in a given string `s` that contains all the characters of another string `t`. Here's a Java solution using the sliding window technique:

```java
import java.util.HashMap;
import java.util.Map;

public class MinimumWindowSubstring {
    public String minWindow(String s, String t) {
        if (s == null || t == null || s.length() < t.length()) {
            return "";
        }

        Map<Character, Integer> tFreq = new HashMap<>();
        for (char c : t.toCharArray()) {
            tFreq.put(c, tFreq.getOrDefault(c, 0) + 1);
        }

        int left = 0, right = 0, minLength = Integer.MAX_VALUE, minStart = 0;
        int required = tFreq.size();
        int formed = 0;
        Map<Character, Integer> windowCounts = new HashMap<>();

        while (right < s.length()) {
            char c = s.charAt(right);
            windowCounts.put(c, windowCounts.getOrDefault(c, 0) + 1);

            if (tFreq.containsKey(c) && windowCounts.get(c).intValue() == tFreq.get(c).intValue()) {
                formed++;
            }

            while (left <= right && formed == required) {
                c = s.charAt(left);
                if (right - left + 1 < minLength) {
                    minLength = right - left + 1;
                    minStart = left;
                }

                windowCounts.put(c, windowCounts.get(c) - 1);
                if (tFreq.containsKey(c) && windowCounts.get(c).intValue() < tFreq.get(c).intValue()) {
                    formed--;
                }
                left++;
            }
            right++;
        }

        return minLength == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLength);
    }

    public static void main(String[] args) {
        MinimumWindowSubstring solution = new MinimumWindowSubstring();
        String s = "ADOBECODEBANC";
        String t = "ABC";
        System.out.println("Minimum window substring: " + solution.minWindow(s, t)); // Output: "BANC"
    }
}
```

This code uses a sliding window approach to expand and contract the window while keeping track of the characters in `t` that are present in the current window. It maintains a count of the characters and checks if the current window contains all characters of `t`. If it does, it tries to minimize the window size.

Feel free to ask if you have any questions or need further assistance!


## Longest Substring with At Most K Distinct Characters

Sure! The "Longest Substring with At Most K Distinct Characters" problem involves finding the length of the longest substring that contains at most `k` distinct characters. Here's a Java solution using the sliding window technique:

```java
import java.util.HashMap;
import java.util.Map;

public class LongestSubstringWithKDistinct {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (s == null || s.length() == 0 || k == 0) {
            return 0;
        }

        Map<Character, Integer> charCount = new HashMap<>();
        int left = 0, right = 0, maxLength = 0;

        while (right < s.length()) {
            char c = s.charAt(right);
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);

            while (charCount.size() > k) {
                char leftChar = s.charAt(left);
                charCount.put(leftChar, charCount.get(leftChar) - 1);
                if (charCount.get(leftChar) == 0) {
                    charCount.remove(leftChar);
                }
                left++;
            }

            maxLength = Math.max(maxLength, right - left + 1);
            right++;
        }

        return maxLength;
    }

    public static void main(String[] args) {
        LongestSubstringWithKDistinct solution = new LongestSubstringWithKDistinct();
        String s = "eceba";
        int k = 2;
        System.out.println("Length of longest substring with at most " + k + " distinct characters: " + solution.lengthOfLongestSubstringKDistinct(s, k)); // Output: 3
    }
}
```

This code uses a sliding window to keep track of the current substring with at most `k` distinct characters. It uses a hash map to store the frequency of characters in the current window and adjusts the window size as needed. The `maxLength` variable keeps track of the length of the longest valid substring found.

Feel free to ask if you have any questions or need further assistance!

## Kaden Algorithm

Kadane's Algorithm is a popular algorithm used to find the maximum sum of a contiguous subarray within a one-dimensional array of numbers. It's efficient and runs in O(n) time complexity.

Here's a Java implementation of Kadane's Algorithm:

```java
public class KadaneAlgorithm {
    public int maxSubArray(int[] nums) {
        int maxSoFar = nums[0];
        int maxEndingHere = nums[0];

        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }

        return maxSoFar;
    }

    public static void main(String[] args) {
        KadaneAlgorithm solution = new KadaneAlgorithm();
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum subarray sum: " + solution.maxSubArray(nums)); // Output: 6
    }
}
```

### Explanation:
1. **Initialization**: 
   - `maxSoFar` is initialized to the first element of the array. It keeps track of the maximum sum found so far.
   - `maxEndingHere` is also initialized to the first element. It keeps track of the maximum sum of the subarray ending at the current position.

2. **Iteration**:
   - Iterate through the array starting from the second element.
   - For each element, update `maxEndingHere` to be the maximum of the current element itself or the sum of `maxEndingHere` and the current element. This step decides whether to start a new subarray at the current element or to extend the existing subarray.
   - Update `maxSoFar` to be the maximum of `maxSoFar` and `maxEndingHere`.

3. **Result**:
   - After iterating through the array, `maxSoFar` will contain the maximum sum of the contiguous subarray.

Feel free to ask if you have any questions or need further assistance!

## Longest Decreasing Subsequence 

To find the longest decreasing subsequence in a given array, you can use dynamic programming. Here's a step-by-step approach and a sample implementation in Java:

### Approach
1. **Dynamic Programming Array**: Use an array `dp` where `dp[i]` represents the length of the longest decreasing subsequence ending at index `i`.
2. **Initialization**: Initialize all elements of `dp` to 1, as the minimum length of any subsequence is 1 (the element itself).
3. **Update the DP Array**: For each element, check all previous elements. If a previous element is greater than the current element, update the `dp` value for the current element.
4. **Find the Maximum Value**: The maximum value in the `dp` array will be the length of the longest decreasing subsequence.

### Example Code (Java)
Here's a sample implementation in Java:

```java
public class LongestDecreasingSubsequence {
    public static int lengthOfLDS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int n = nums.length;
        int[] dp = new int[n];
        int maxLength = 1;

        // Initialize dp array
        for (int i = 0; i < n; i++) {
            dp[i] = 1;
        }

        // Fill dp array
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] > nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLength = Math.max(maxLength, dp[i]);
        }

        return maxLength;
    }

    public static void main(String[] args) {
        int[] nums = {9, 4, 3, 2, 5, 4, 3, 2};
        System.out.println(lengthOfLDS(nums));  // Output: 4
    }
}
```

This code will return `4` for the input array `{9, 4, 3, 2, 5, 4, 3, 2}`, as the longest decreasing subsequence is `{9, 4, 3, 2}`.

If you have any questions or need further assistance, feel free to ask!

## Pythagorean Triplets Detection

Sure! Let's break down the optimized solution for detecting Pythagorean triplets in Java step by step.

### Code Explanation

```java
public class PythagoreanTripletsOptimized {
    public static void main(String[] args) {
        int limit = 100; // Define the range limit
        findPythagoreanTriplets(limit);
    }

    public static void findPythagoreanTriplets(int limit) {
        for (int a = 1; a <= limit; a++) {
            for (int b = a; b <= limit; b++) {
                int cSquare = a * a + b * b;
                int c = (int) Math.sqrt(cSquare);
                if (c * c == cSquare && c <= limit) {
                    System.out.println("Pythagorean Triplet: " + a + ", " + b + ", " + c);
                }
            }
        }
    }
}
```

### Detailed Steps

1. **Class and Main Method:**
   - We define a class `PythagoreanTripletsOptimized`.
   - The `main` method sets a limit for the range within which we want to find Pythagorean triplets (in this case, 100).
   - The `findPythagoreanTriplets` method is called with this limit.

2. **findPythagoreanTriplets Method:**
   - **Outer Loop (Variable `a`):** This loop iterates through all possible values of `a` from 1 to the specified limit.
   - **Inner Loop (Variable `b`):** This loop iterates through all possible values of `b` starting from `a` to the limit. This ensures that we don't repeat triplets (e.g., (3, 4, 5) and (4, 3, 5)).
   - **Calculate `cSquare`:** For each pair `(a, b)`, we calculate `cSquare` as \(a^2 + b^2\).
   - **Calculate `c`:** We then calculate `c` as the integer square root of `cSquare` using `Math.sqrt(cSquare)`.
   - **Check for Pythagorean Triplet:**
     - We check if `c` squared (`c * c`) is equal to `cSquare`. This ensures that `c` is an integer.
     - We also check if `c` is within the specified limit.
   - **Print the Triplet:** If both conditions are met, we print the triplet `(a, b, c)`.

### Optimization Benefits

- **Reduced Iterations:** By calculating `c` directly and checking its validity, we eliminate the need for a third nested loop, significantly reducing the number of iterations.
- **Avoiding Redundancy:** By starting the inner loop from `a`, we avoid checking the same triplet in different orders (e.g., (3, 4, 5) and (4, 3, 5)).

This optimized approach is more efficient and faster, especially for larger ranges.

If you have any further questions or need additional clarifications, feel free to ask!

## Longest Substring Without Repeating Characters

Sure, I can help with that! Here's how you can find the longest substring without repeating characters in Java:

### Problem Explanation
Given a string, you need to find the length of the longest substring that does not contain any repeating characters.

### Example
- Input: "abcabcbb"
- Output: 3 (The answer is "abc", with the length of 3.)

### Approach
We can use a sliding window technique with two pointers to solve this problem efficiently. The idea is to use a set to keep track of characters in the current window and adjust the window size as we encounter repeating characters.

### Java Code
Here's a sample implementation in Java:

```java
import java.util.HashSet;
import java.util.Set;

public class LongestSubstringWithoutRepeatingCharacters {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> charSet = new HashSet<>();
        int left = 0, maxLength = 0;

        for (int right = 0; right < s.length(); right++) {
            while (charSet.contains(s.charAt(right))) {
                charSet.remove(s.charAt(left));
                left++;
            }
            charSet.add(s.charAt(right));
            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;
    }

    public static void main(String[] args) {
        LongestSubstringWithoutRepeatingCharacters solution = new LongestSubstringWithoutRepeatingCharacters();
        String s = "abcabcbb";
        System.out.println(solution.lengthOfLongestSubstring(s));  // Output: 3
    }
}
```

### Explanation
1. **Initialize** a set `charSet` to store characters in the current window, and two pointers `left` and `right` to represent the window's boundaries.
2. **Iterate** through the string with the `right` pointer.
3. **Adjust** the `left` pointer and remove characters from `charSet` until there are no repeating characters in the window.
4. **Update** the maximum length of the substring found so far.

Feel free to ask if you have any questions or need further clarification!


## Longest Repeating Character Replacement

Sure, I can help with that! Here's how you can find the longest substring with the same characters after replacing at most `k` characters in Java:

### Problem Explanation
Given a string `s` and an integer `k`, you need to find the length of the longest substring that contains the same character after replacing at most `k` characters.

### Example
- Input: `s = "AABABBA", k = 1`
- Output: 4 (The answer is "AABA" after replacing one 'B' with 'A'.)

### Approach
We can use a sliding window technique to solve this problem efficiently. The idea is to keep track of the frequency of characters in the current window and adjust the window size based on the number of replacements allowed.

### Java Code
Here's a sample implementation in Java:

```java
import java.util.HashMap;
import java.util.Map;

public class LongestRepeatingCharacterReplacement {
    public int characterReplacement(String s, int k) {
        Map<Character, Integer> count = new HashMap<>();
        int maxCount = 0, left = 0, maxLength = 0;

        for (int right = 0; right < s.length(); right++) {
            count.put(s.charAt(right), count.getOrDefault(s.charAt(right), 0) + 1);
            maxCount = Math.max(maxCount, count.get(s.charAt(right)));

            while (right - left + 1 - maxCount > k) {
                count.put(s.charAt(left), count.get(s.charAt(left)) - 1);
                left++;
            }

            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;
    }

    public static void main(String[] args) {
        LongestRepeatingCharacterReplacement solution = new LongestRepeatingCharacterReplacement();
        String s = "AABABBA";
        int k = 1;
        System.out.println(solution.characterReplacement(s, k));  // Output: 4
    }
}
```

### Explanation
1. **Initialize** a map `count` to store the frequency of characters in the current window, and variables `maxCount`, `left`, and `maxLength`.
2. **Iterate** through the string with the `right` pointer.
3. **Update** the frequency of the current character and the `maxCount` of any character in the current window.
4. **Adjust** the `left` pointer if the number of characters to be replaced exceeds `k`.
5. **Update** the maximum length of the substring found so far.

Feel free to ask if you have any questions or need further clarification!


## Longest Palindromic Substring

Sure, I can help with that! Using dynamic programming (DP) to find the longest palindromic substring is a classic approach. Here's how you can implement it in Java:

### Problem Explanation
Given a string `s`, you need to find the longest substring that is a palindrome.

### Example
- Input: "babad"
- Output: "bab" or "aba" (Both are valid answers.)

### Approach
We can use a 2D DP array to keep track of palindromic substrings. The idea is to fill the DP table such that `dp[i][j]` is `true` if the substring `s[i...j]` is a palindrome.

### Java Code
Here's a sample implementation in Java:

```java
public class LongestPalindromicSubstringDP {
    public String longestPalindrome(String s) {
        int n = s.length();
        if (n == 0) return "";

        boolean[][] dp = new boolean[n][n];
        int start = 0, maxLength = 1;

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
        LongestPalindromicSubstringDP solution = new LongestPalindromicSubstringDP();
        String s = "babad";
        System.out.println(solution.longestPalindrome(s));  // Output: "bab" or "aba"
    }
}
```

### Explanation
1. **Initialize** a 2D DP array `dp` where `dp[i][j]` is `true` if the substring `s[i...j]` is a palindrome.
2. **Single Character Substrings**: All substrings of length 1 are palindromes.
3. **Two Character Substrings**: Check for palindromes of length 2.
4. **Longer Substrings**: For substrings longer than 2 characters, check if the current substring is a palindrome by comparing the characters at the ends and the DP value of the inner substring.
5. **Update** the starting index and maximum length of the longest palindromic substring found.

Feel free to ask if you have any questions or need further clarification!


## Longest Palindromic Subsequence

Sure, I can help with that! Finding the longest palindromic subsequence in a given string is another interesting problem. Unlike substrings, subsequences do not require the characters to be contiguous. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
Given a string `s`, you need to find the length of the longest subsequence that is a palindrome.

### Example
- Input: "bbbab"
- Output: 4 (The longest palindromic subsequence is "bbbb".)

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to use a 2D DP array where `dp[i][j]` represents the length of the longest palindromic subsequence in the substring `s[i...j]`.

### Java Code
Here's a sample implementation in Java:

```java
public class LongestPalindromicSubsequence {
    public int longestPalindromeSubseq(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];

        // Base case: single character substrings are palindromes of length 1
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

        // Fill the DP table
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
        LongestPalindromicSubsequence solution = new LongestPalindromicSubsequence();
        String s = "bbbab";
        System.out.println(solution.longestPalindromeSubseq(s));  // Output: 4
    }
}
```

### Explanation
1. **Initialize** a 2D DP array `dp` where `dp[i][j]` represents the length of the longest palindromic subsequence in the substring `s[i...j]`.
2. **Single Character Substrings**: All single character substrings are palindromes of length 1.
3 **Fill the DP Table**: For substrings of length greater than 1, if the characters at the ends are the same, the length of the longest palindromic subsequence is `dp[i + 1][j - 1] + 2`. Otherwise, it is the maximum of `dp[i + 1][j]` and `dp[i][j - 1]`.
4. **Return the Result**: The value `dp[0][n - 1]` gives the length of the longest palindromic subsequence in the entire string.

Feel free to ask if you have any questions or need further clarification!


## Longest Increasing Subsequence

Sure, I can help with that! Finding the longest increasing subsequence (LIS) in a given array is a classic problem in computer science. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
Given an array of integers, you need to find the length of the longest subsequence such that all elements of the subsequence are sorted in increasing order.

### Example
- Input: [10, 9, 2, 5, 3, 7, 101, 18]
- Output: 4 (The longest increasing subsequence is [2, 3, 7, 101].)

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to maintain an array `dp` where `dp[i]` represents the length of the longest increasing subsequence that ends with the element at index `i`.

### Java Code
Here's a sample implementation in Java:

```java
public class LongestIncreasingSubsequence {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int n = nums.length;
        int[] dp = new int[n];
        int maxLength = 1;

        // Initialize the dp array with 1, as the minimum length of LIS ending at each element is 1
        for (int i = 0; i < n; i++) {
            dp[i] = 1;
        }

        // Fill the dp array
        for (int i = 1; i < n; i++) {
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
        LongestIncreasingSubsequence solution = new LongestIncreasingSubsequence();
        int[] nums = {10, 9, 2, 5, 3, 7, 101, 18};
        System.out.println(solution.lengthOfLIS(nums));  // Output: 4
    }
}
```

### Explanation
1. **Initialize** an array `dp` where `dp[i]` represents the length of the longest increasing subsequence that ends with the element at index `i`. Initialize all elements of `dp` to 1, as the minimum length of LIS ending at each element is 1.
2. **Fill the DP Array**: For each element `nums[i]`, check all previous elements `nums[j]` (where `j < i`). If `nums[i] > nums[j]`, update `dp[i]` to be the maximum of `dp[i]` and `dp[j] + 1`.
3. **Update the Maximum have any questions or need further clarification!


## Longest Common Subsequence

Sure, I can help with that! Finding the longest common subsequence (LCS) between two strings is a classic problem in computer science. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
Given two strings `text1` and `text2`, you need to find the length of their longest common subsequence. A subsequence is a sequence that appears in the same relative order, but not necessarily consecutively.

### Example
- Input: `text1 = "abcde"`, `text2 = "ace"`
- Output: 3 (The longest common subsequence is "ace".)

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to use a 2D DP array where `dp[i][j]` represents the length of the longest common subsequence of the substrings `text1[0...i-1]` and `text2[0...j-1]`.

### Java Code
Here's a sample implementation in Java:

```java
public class LongestCommonSubsequence {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];

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
        LongestCommonSubsequence solution = new LongestCommonSubsequence();
        String text1 = "abcde";
        String text2 = "ace";
        System.out.println(solution.longestCommonSubsequence(text1, text2));  // Output: 3
    }
}
```

### Explanation
1. **Initialize** a 2D DP array `dp` where `dp[i][j]` represents the length of the longest common subsequence of the substrings `text1[0...i-1]` and `text2[0...j-1]`.
2. **Fill the DP Table**: Iterate through each character of `text1` and `text2`. If the characters match, `dp[i][j] = dp[i - 1][j - 1] + 1`. Otherwise, `dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1])`.
3. **Return the Result**: The value `dp[m][n]` gives the length of the longest common subsequence of the entire strings.

Feel free to ask if you have any questions or need further clarification!

## Minimum Path Sum

Sure! Here's a Java solution to find the minimum path sum in a grid. The path can only move either down or right at any point in time:

```java
public class MinimumPathSum {
    public static int minPathSum(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }

        int rows = grid.length;
        int cols = grid[0].length;

        // Initialize the first row
        for (int i = 1; i < cols; i++) {
            grid[0][i] += grid[0][i - 1];
        }

        // Initialize the first column
        for (int i = 1; i < rows; i++) {
            grid[i][0] += grid[i - 1][0];
        }

        // Fill in the rest of the grid
        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                grid[i][j] += Math.min(grid[i - 1][j], grid[i][j - 1]);
            }
        }

        return grid[rows - 1][cols - 1];
    }

    public static void main(String[] args) {
        int[][] grid = {
            {1, 3, 1},
            {1, 5, 1},
            {4, 2, 1}
        };
        int result = minPathSum(grid);
        System.out.println("Minimum Path Sum: " + result);
    }
}
```

This code defines a `MinimumPathSum` class with a method `minPathSum` that calculates the minimum path sum in a grid. The method uses dynamic programming to update the grid in place, ensuring that each cell contains the minimum path sum to reach that cell.

If you have any questions or need further assistance, feel free to ask!




## Coin Change

Sure, I can help with that! The coin change problem can be efficiently solved using dynamic programming. Here's how you can implement it in Java:

### Problem Explanation
Given an array of coins of different denominations and an integer amount, you need to find the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

### Example
- Input: `coins = [1, 2, 5]`, `amount = 11`
- Output: 3 (The fewest number of coins to make up 11 is 3: 5 + 5 + 1.)

### Approach
We can use a 1D DP array where `dp[i]` represents the minimum number of coins needed to make up amount `i`.

### Java Code
Here's a sample implementation in Java:

```java
public class CoinChange {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;

        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (i - coin >= 0) {
                    dp[i] = Math.max(dp[i], dp[i - coin] + 1);
                }
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }

    public static void main(String[] args) {
        CoinChange solution = new CoinChange();
        int[] coins = {1, 2, 5};
        int amount = 11;
        System.out.println(solution.coinChange(coins, amount));  // Output: 3
    }
}
```

### Explanation
1. **Initialize** a 1D DP array `dp` where `dp[i]` represents the minimum number of coins needed to make up amount `i`. Initialize all elements to `amount + 1` (a value greater than any possible number of coins needed) except `dp[0]`, which is 0 because 0 amount requires 0 coins.
2. **Fill the DP Array**: For each amount from 1 to `amount`, iterate through each coin. If the coin can be used (i.e., `i - coin >= 0`), update `dp[i]` to be the minimum of its current value and `dp[i - coin] + 1`.
3. **Return the Result**: The value `dp[amount]` gives the minimum number of coins needed to make up the amount. If it's still greater than `amount`, return -1 indicating it's not possible to make up the amount with the given coins.

Feel free to ask if you have any questions or need further clarification!

## 0 1 Knapsack

Sure, I can help with that! The 0/1 Knapsack problem is a classic dynamic programming problem. Here's how you can solve it using dynamic programming in Java:

### Problem Explanation
Given a set of items, each with a weight and a value, determine the maximum value that can be obtained by selecting items such that the total weight does not exceed a given capacity. Each item can be included or excluded (0/1).

### Example
- Input: `weights = [1, 3, 4, 5]`, `values = [1, 4, 5, 7]`, `capacity = 7`
- Output: 9 (The maximum value is obtained by selecting items with weights 3 and 4.)

### Approach
We can use a 2D DP array where `dp[i][j]` represents the maximum value that can be obtained with the first `i` items and a knapsack capacity of `j`.

### Java Code
Here's a sample implementation in Java:

```java
public class Knapsack {
    public int knapsack(int[] weights, int[] values, int capacity) {
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
        Knapsack solution = new Knapsack();
        int[] weights = {1, 3, 4, 5};
        int[] values = {1, 4, 5, 7};
        int capacity = 7;
        System.out.println(solution.knapsack(weights, values, capacity));  // Output: 9
    }
}
```

### Explanation
1. **Initialize** a 2D DP array `dp` where `dp[i][j]` represents the maximum value that can be obtained with the first `i` items and a knapsack capacity of `j`.
2. **Fill the DP Table**: For each item and each capacity, update the DP table based on whether the current item is included or excluded.
   - If the current item's weight is less than or equal to the current capacity, update `dp[i][w]` to be the maximum of:
     - The value without including the current item (`dp[i - 1][w]`).
     - The value including the current item (`dp[i - 1][w - weights[i - 1]] + values[i - 1]`).
   - If the current item's weight is greater than the current capacity, the current item cannot be included, so `dp[i][w] = dp[i - 1][w]`.
3. **Return the Result**: The value `dp[n][capacity]` gives the maximum value that can be obtained with the given items and capacity.

Feel free to ask if you have any questions or need further clarification!


## Fractional KnapSack

The 0/1 Knapsack problem and the Fractional Knapsack problem are typically solved using different approaches. The 0/1 Knapsack problem is solved using dynamic programming, while the Fractional Knapsack problem is best solved using a greedy algorithm. However, if you are looking for a solution that combines elements of both, it's important to clarify that the Fractional Knapsack problem inherently allows for fractional parts of items, which doesn't align with the 0/1 constraint (where items are either taken whole or not at all).

If you still want to explore a dynamic programming approach for a problem that involves fractional items, it would be more of a theoretical exercise rather than a practical one, as the greedy approach is optimal for the Fractional Knapsack problem.

### 0/1 Knapsack Problem Using 2D DP in Java
Here's a reminder of how the 0/1 Knapsack problem is solved using dynamic programming:

```java
public class Knapsack {
    public int knapsack(int[] weights, int[] values, int capacity) {
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
        Knapsack solution = new Knapsack();
        int[] weights = {1, 3, 4, 5};
        int[] values = {1, 4, 5, 7};
        int capacity = 7;
        System.out.println(solution.knapsack(weights, values, capacity));  // Output: 9
    }
}
```

### Explanation
1. **Initialize** a 2D DP array `dp` where `dp[i][j]` represents the maximum value that can be obtained with the first `i` items and a knapsack capacity of `j`.
2. **Fill the DP Table**: For each item and each capacity, update the DP table based on whether the current item is included or excluded.
   - If the current item's weight is less than or equal to the current capacity, update `dp[i][w]` to be the maximum of:
     - The value without including the current item (`dp[i - 1][w]`).
     - The value including the current item (`dp[i - 1][w - weights[i - 1]] + values[i - 1]`).
   - If the current item's weight is greater than the current capacity, the current item cannot be included, so `dp[i][w] = dp[i - 1][w]`.
3. **Return the Result**: The value `dp[n][capacity]` gives the maximum value that can be obtained with the given items and capacity.

For the Fractional Knapsack problem, the greedy approach is optimal and more efficient. If you have any specific requirements or further questions, feel free to ask!




## Jump Game

Sure, I can help with that! The Jump Game problem is a classic problem where you need to determine if you can reach the last index of an array starting from the first index. Each element in the array represents the maximum jump length at that position.

### Problem Explanation
Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array. Each element in the array represents your maximum jump length at that position. Determine if you can reach the last index.

### Example
- Input: `nums = [2, 3, 1, 1, 4]`
- Output: `true` (You can jump to the last index by jumping 1 step to index 1, then 3 steps to the last index.)

### Approach
We can solve this problem using a greedy algorithm. The idea is to keep track of the farthest index that can be reached and update it as we iterate through the array.

### Java Code
Here's a sample implementation in Java:

```java
public class JumpGame {
    public boolean canJump(int[] nums) {
        int maxReach = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i > maxReach) {
                return false;
            }
            maxReach = Math.max(maxReach, i + nums[i]);
        }
        return maxReach >= nums.length - 1;
    }

    public static void main(String[] args) {
        JumpGame solution = new JumpGame();
        int[] nums = {2, 3, 1, 1, 4};
        System.out.println(solution.canJump(nums));  // Output: true
    }
}
```

### Explanation
1. **Initialize** a variable `maxReach` to keep track of the farthest index that can be reached.
2. **Iterate** through the array:
   - If the current index `i` is greater than `maxReach`, return `false` because it means you cannot reach this index.
   - Update `maxReach` to be the maximum of its current value and `i + nums[i]`.
3. **Return** `true` if `maxReach` is greater than or equal to the last index of the array.

Feel free to ask if you have any questions or need further clarification!

## Edit Distance

Sure, I can help with that! The Edit Distance problem, also known as the Levenshtein Distance, is a classic problem in computer science. It measures the minimum number of operations required to convert one string into another. The allowed operations are insertion, deletion, and substitution.

### Problem Explanation
Given two strings `word1` and `word2`, you need to find the minimum number of operations required to convert `word1` into `word2`.

### Example
- Input: `word1 = "horse"`, `word2 = "ros"`
- Output: 3 (The minimum operations are: "horse" -> "rorse" (replace 'h' with 'r'), "rorse" -> "rose" (remove 'r'), "rose" -> "ros" (remove 'e').)

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to use a 2D DP array where `dp[i][j]` represents the minimum number of operations required to convert the first `i` characters of `word1` to the first `j` characters of `word2`.

### Java Code
Here's a sample implementation in Java:

```java
public class EditDistance {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m + 1][n + 1];

        // Initialize the DP table
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }

        // Fill the DP table
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
               (i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        EditDistance solution = new EditDistance();
        String word1 = "horse";
        String word2 = "ros";
        System.out.println(solution.minDistance(word1, word2));  // Output: 3
    }
}
```

### Explanation
1. **Initialize** a 2D DP array `dp` where `dp[i][j]` represents the minimum number of operations required to convert the first `i` characters of `word1` to the first `j` characters of `word2`.
2. **Base Cases**: 
   - `dp[i][0] = i` for all `i` because converting any string to an empty string requires `i` deletions.
   - `dp[0][j] = j` for all `j` because converting an empty string to any string requires `j` insertions.
3. **Fill the DP Table**: For each character in `word1` and `word2`, update the DP table based on whether the characters match or not.
   - If the characters match, `dp[i][j] = dp[i - 1][j - 1]`.
   - If the characters do not match, `dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1`.
4. **Return the Result**: The value `dp[m][n]` gives the minimum number of operations required to convert `word1` to `word2`.

Feel free to ask if you have any questions or need further clarification!

## Pascal's Triangle in java

Sure! Here's a Java solution to generate Pascal's Triangle up to a given number of rows:

```java
import java.util.ArrayList;
import java.util.List;

public class PascalsTriangle {
    public static List<List<Integer>> generate(int numRows) {
        List<List<Integer>> triangle = new ArrayList<>();

        if (numRows <= 0) {
            return triangle;
        }

        // First row is always [1]
        triangle.add(new ArrayList<>());
        triangle.get(0).add(1);

        for (int rowNum = 1; rowNum < numRows; rowNum++) {
            List<Integer> row = new ArrayList<>();
            List<Integer> prevRow = triangle.get(rowNum - 1);

            // First element of each row is always 1
            row.add(1);

            // Each element is the sum of the two elements above it
            for (int j = 1; j < rowNum; j++) {
                row.add(prevRow.get(j - 1) + prevRow.get(j));
            }

            // Last element of each row is always 1
            row.add(1);

            triangle.add(row);
        }

        return triangle;
    }

    public static void main(String[] args) {
        int numRows = 5;
        List<List<Integer>> triangle = generate(numRows);
        for (List<Integer> row : triangle) {
            System.out.println(row);
        }
    }
}
```

This code defines a `PascalsTriangle` class with a method `generate` that generates Pascal's Triangle up to a specified number of rows. The method uses a list of lists to store the triangle, and each row is constructed based on the values of the previous row.

If you have any questions or need further assistance, feel free to ask!


## Climb Stairs

Sure, I can help with that! The Climbing Stairs problem is a classic dynamic programming problem. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

### Example
- Input: `n = 3`
- Output: 3 (There are three ways to climb to the top: 1 step + 1 step + 1 step, 1 step + 2 steps, 2 steps + 1 step.)

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to use a DP array where `dp[i]` represents the number of distinct ways to reach the `i`-th step.

### Java Code
Here's a sample implementation in Java:

```java
public class ClimbStairs {
    public int climbStairs(int n) {
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
        ClimbStairs solution = new ClimbStairs();
        int n = 3;
        System.out.println(solution.climbStairs(n));  // Output: 3
    }
}
```

### Explanation
1. **Base Cases**: 
   - `dp[0] = 1` because there is one way to stay at the ground (doing nothing).
   - `dp[1] = 1` because there is one way to reach the first step (one step).
2. **Fill the DP Array**: For each step from 2 to `n`, the number of ways to reach that step is the sum of the ways to reach the previous step (`dp[i - 1]`) and the ways to reach the step before the previous step (`dp[i - 2]`).
3. **Return the Result**: The value `dp[n]` gives the number of distinct ways to reach the `n`-th step.

Feel free to ask if you have any questions or need further clarification!


## Unique Paths

Sure, I can help with that! The Unique Paths problem is a classic dynamic programming problem. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

### Example
- Input: `m = 3`, `n = 7`
- Output: 28

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to use a 2D DP array where `dp[i][j]` represents the number of unique paths to reach the cell `(i, j)`.

### Java Code
Here's a sample implementation in Java:

```java
public class UniquePaths {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];

        // Initialize {
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            dp[0][j] = 1;
        }

        // Fill the DP table
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }

        return dp[m - 1][n - 1];
    }

    public static void main(String[] args) {
        UniquePaths solution = new UniquePaths();
        int m = 3;
        int n = 7;
        System.out.println(solution.uniquePaths(m, n));  // Output: 28
    }
}
```

### Explanation
1. **Initialize** a 2D DP array `dp` where `dp[i][j]` represents the number of unique paths to reach the cell `(i, j)`.
2. **Base Cases**: 
   - The first row and the first column can only be reached in one way (either all the way right or all the way down).
3. **Fill the DP Table**: For each cell `(i, j)`, the number of unique paths to reach that cell is the sum of the unique paths to reach the cell directly above it (`dp[i - 1][j]`) and the cell directly to the left of it (`dp[i][j - 1]`).
4. **Return the Result**: The value `dp[m - 1][n - 1]` gives the number of unique paths to reach the bottom-right corner of the grid.

Feel free to ask if you have any questions or need further clarification!


## Word Break

Sure, I can help with that! The Word Break problem is a classic dynamic programming problem. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
Given a string `s` and a dictionary of strings `wordDict`, determine if `s` can be segmented into a space-separated sequence of one or more dictionary words.

### Example
- Input: `s = "leetcode"`, `wordDict = ["leet", "code"]`
- Output: `true` (The string can be segmented as "leet code".)

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to use a DP array where `dp[i]` represents whether the substring `s[0...i-1]` can be segmented into dictionary words.

### Java Code
Here's a sample implementation in Java:

```java
import java.util.List;
import java.util.Set;
import java.util.HashSet;

public class WordBreak {
    public boolean wordBreak(String s, List<String> wordDict) {
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
        WordBreak solution = new WordBreak();
        String s = "leetcode";
        List<String> wordDict = List.of("leet", "code");
       .out.println(solution.wordBreak(s, wordDict));  // Output: true
    }
}
```

### Explanation
1. **Initialize** a boolean array `dp` where `dp[i]` represents whether the substring `s[0...i-1]` can be segmented into dictionary words. Set `dp[0]` to `true` because an empty string can always be segmented.
2. **Fill the DP Array**: For each position `i` in the string, check all possible substrings `s[j...i-1]` where `0 <= j < i`. If `dp[j]` is `true` and the substring `s[j...i-1]` is in the dictionary, set `dp[i]` to `true` and break the inner loop.
3. **Return the Result**: The value `dp[s.length()]` gives whether the entire string can be segmented into dictionary words.

Feel free to ask if you have any questions or need further clarification!

## House Robber

Sure, I can help with that! The House Robber problem is a classic dynamic programming problem. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, and the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array `nums` representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

### Example
- Input: `nums = [1, 2, 3, 1]`
- Output: 4 (Rob house 1 (money = 1) and then rob house 3 (money = 3). Total amount you can rob = 1 + 3 = 4.)

### Approach
We can use dynamic programming to solve this problem efficiently. The idea is to use a DP array where `dp[i]` represents the maximum amount of money that can be robbed from the first `i` houses.

### Java Code
Here's a sample implementation in Java:

```java
public class HouseRobber {
    public int rob(int[] nums) {
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

        return dp[nums.length - 1];
    }

    public static void main(String[] args) {
        HouseRobber solution = new HouseRobber();
        int[] nums = {1, 2, 3, 1};
        System.out.println(solution.rob(nums));  // Output: 4
    }
}
```

### Explanation
1. **Base Cases**: 
   - If there are no houses, the maximum amount of money is 0.
   - If there is only one house, the maximum amount of money is the value of that house.
2. **Initialize** a DP array `dp` where `dp[i]` represents the maximum amount of money that can be robbed from the first `i` houses.
   - `dp[0] = nums[0]` because the maximum amount of money from the first house is its value.
   - `dp[1] = Math.max(nums[0], nums[1])` because the maximum amount of money from the first two houses is the maximum of their values.
3. **Fill the DP Array**: For each house from the third one onwards, the maximum amount of money that can be robbed is the maximum of:
   - The maximum amount of money robbed from the previous house (`dp[i - 1]`).
   - The maximum amount of money robbed from the house before the previous one plus the current house's value (`dp[i - 2] + nums[i]`).
4. **Return the Result**: The value `dp[nums.length - 1]` gives the maximum amount of money that can be robbed from all the houses.

Feel free to ask if you have any questions or need further clarification!

## Isomorphic String

Sure, I can help with that! The problem of determining if two strings are isomorphic is a common one in computer science. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`. All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

### Example
- Input: `s = "egg"`, `t = "add"`
- Output: `true`
- Input: `s = "foo"`, `t = "bar"`
- Output: `false`

### Approach
We can solve this problem by using two hash maps to keep track of the character mappings from `s` to `t` and from `t` to `s`.

### Java Code
Here's a sample implementation in Java:

```java
import java.util.HashMap;
import java.util.Map;

public class IsomorphicStrings {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        Map<Character, Character> mapS = new HashMap<>();
        Map<Character, Character> mapT = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char charS = s.charAt(i);
            char charT = t.charAt(i);

            if (mapS.containsKey(charS)) {
                if (mapS.get(charS) != charT) {
                    return false;
                }
            } else {
                mapS.put(charS, charT);
            }

            if (mapT.containsKey(charT)) {
                if (mapT.get(charT) != charS) {
                    return false;
                }
            } else {
                mapT.put(charT, charS);
            }
        }

        return true;
    }

    public static void main(String[] args) {
        IsomorphicStrings solution = new IsomorphicStrings();
        System.out.println(solution.isIsomorphic("egg", "add"));  // Output: true
        System.out.println(solution.isIsomorphic("foo", "bar"));  // Output: false
        System.out.println(solution.isIsomorphic("paper", "title"));  // Output: true
    }
}
```

### Explanation
1. **Check Lengths**: If the lengths of the two strings are not the same, they cannot be isomorphic.
2. **Initialize Maps**: Use two hash maps to keep track of the character mappings from `s` to `t` and from `t` to `s`.
3. **Iterate Through Strings**: For each character in the strings, check if the current character mapping is consistent with the previous mappings. If not, return `false`.
4. **Return Result**: If all character mappings are consistent, return `true`.

Feel free to ask if you have any questions or need further clarification!


## Valid Anagrams
Sure, I can help with that! The problem of determining if two strings are anagrams is a common one in computer science. Here's a brief explanation and a sample solution in Java:

### Problem Explanation
Two strings `s` and `t` are anagrams if they contain the same characters with the same frequencies.

### Example
- Input: `s = "anagram"`, `t = "nagaram"`
- Output: `true`
- Input: `s = "rat"`, `t = "car"`
- Output: `false`

### Approach
We can solve this problem by using a hash map to count the frequency of each character in both strings and then compare the frequency counts.

### Java Code
Here's a sample implementation in Java:

```java
import java.util.HashMap;
import java.util.Map;

public class ValidAnagram {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        Map<Character, Integer> countMap = new HashMap<>();

        for (char c : s.toCharArray()) {
            countMap.put(c, countMap.getOrDefault(c, 0) + 1);
        }

        for (char c : t.toCharArray()) {
            if (!countMap.containsKey(c)) {
                return false;
            }
            countMap.put(c, countMap.get(c) - 1);
            if (countMap.get(c) == 0) {
                countMap.remove(c);
            }
        }

        return countMap.isEmpty();
    }

    public static void main(String[] args) {
        ValidAnagram solution = new ValidAnagram();
        System.out.println(solution.isAnagram("anagram", "nagaram"));  // Output: true
        System.out.println(solution.isAnagram("rat", "car"));  // Output: false
    }
}
```

### Explanation
1. **Check Lengths**: If the lengths of the two strings are not the same, they cannot be anagrams.
2. **Count Characters in `s`**: Use a hash map to count the frequency of each character in the first string `s`.
3. **Compare with `t`**: For each character in the second string `t`, decrement the count in the hash map. If a character is not found or the count goes below zero, return `false`.
4. **Check Map**: If the hash map is empty after processing both strings, the strings are anagrams.

Feel free to ask if you have any questions or need further clarification!

## Group Anagrams

Sure, I can help with that! Grouping anagrams involves taking a list of words and grouping them together if they are anagrams of each other. Here's a simple way to do it in Java:

```java
import java.util.*;

public class GroupAnagrams {
    public static List<List<String>> groupAnagrams(String[] strs) {
        if (strs == null || strs.length == 0) return new ArrayList<>();
        Map<String, List<String>> map = new HashMap<>();
        for (String s : strs) {
            char[] ca = s.toCharArray();
            Arrays.sort(ca);
            String key = String.valueOf(ca);
            if (!map.containsKey(key)) map.put(key, new ArrayList<>());
            map.get(key).add(s);
        }
        return new ArrayList<>(map.values());
    }

    public static void main(String[] args) {
        String[] input = {"eat", "tea", "tan", "ate", "nat", "bat"};
        List<List<String>> result = groupAnagrams(input);
        for (List<String> group : result) {
            System.out.println(group);
        }
    }
}
```

This code does the following:
1. Converts each string to a character array and sorts it.
2. Uses the sorted string as a key in a hashmap.
3. Groups all strings with the same sorted key together.

You can run this code to see the grouped anagrams. If you have any questions or need further assistance, feel free to ask!


## Word Pattern
Sure, I can help with that! The "Word Pattern" problem typically involves checking if a given pattern matches a string in such a way that each character in the pattern corresponds to a word in the string. Here's a simple implementation in Java:

```java
import java.util.HashMap;
import java.util.Map;

public class WordPattern {
    public static boolean wordPattern(String pattern, String str) {
        String[] words = str.split(" ");
        if (pattern.length() != words.length) return false;

        Map<Character, String> charToWord = new HashMap<>();
        Map<String, Character> wordToChar = new HashMap<>();

        for (int i = 0; i < pattern.length(); i++) {
            char c = pattern.charAt(i);
            String word = words[i];

            if (!charToWord.containsKey(c)) {
                if (wordToChar.containsKey(word)) {
                    return false;
                }
                charToWord.put(c, word);
                wordToChar.put(word, c);
            } else {
                if (!charToWord.get(c).equals(word)) {
                    return false;
                }
            }
        }
        return true;
    }

    public static void main(String[] args) {
        String pattern = "abba";
        String str = "dog cat cat dog";
        boolean result = wordPattern(pattern, str);
        System.out.println(result); // Output: true
    }
}
```

This code does the following:
1. Splits the input string into words.
2. Checks if the length of the pattern matches the number of words.
3. Uses two hash maps to map characters to words and words to characters.
4. Ensures that each character maps to the same word and each word maps to the same character.

You can run this code to check if a pattern matches a given string. If you have any questions or need further assistance, feel free to ask!

## Search a 2D Matrix
Sure! Here's a Java solution to search for a target value in a 2D matrix. The matrix has the properties that each row is sorted in ascending order, and the first integer of each row is greater than the last integer of the previous row:

```java
public class Search2DMatrix {
    public static boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        int rows = matrix.length;
        int cols = matrix[0].length;
        int left = 0;
        int right = rows * cols - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            int midValue = matrix[mid / cols][mid % cols];

            if (midValue == target) {
                return true;
            } else if (midValue < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return false;
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1, 3, 5, 7},
            {10, 11, 16, 20},
            {23, 30, 34, 60}
        };
        int target = 3;
        boolean found = searchMatrix(matrix, target);
        System.out.println("Target " + target + " found: " + found);
    }
}
```

This code defines a `Search2DMatrix` class with a method `searchMatrix` that searches for a target value in a 2D matrix. The method uses a binary search approach to efficiently find the target value.

If you have any questions or need further assistance, feel free to ask!

## Binary Tree Maximum Path Sum

Sure! Here's a Java solution to find the maximum path sum in a binary tree. The path can start and end at any node in the tree:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeMaximumPathSum {
    private static int maxSum;

    public static int maxPathSum(TreeNode root) {
        maxSum = Integer.MIN_VALUE;
        maxGain(root);
        return maxSum;
    }

    private static int maxGain(TreeNode node) {
        if (node == null) {
            return 0;
        }

        // Recursively call maxGain on left and right subtrees
        int leftGain = Math.max(maxGain(node.left), 0);
        int rightGain = Math.max(maxGain(node.right), 0);

        // Current path sum including the current node
        int currentPathSum = node.val + leftGain + rightGain;

        // Update maxSum if the current path sum is greater
        maxSum = Math.max(maxSum, currentPathSum);

        // Return the maximum gain if continuing the same path
        return node.val + Math.max(leftGain, rightGain);
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(-10);
        root.left = new TreeNode(9);
        root.right = new TreeNode(20);
        root.right.left = new TreeNode(15);
        root.right.right = new TreeNode(7);

        int result = maxPathSum(root);
        System.out.println("Maximum Path Sum: " + result);
    }
}
```

This code defines a `BinaryTreeMaximumPathSum` class with a method `maxPathSum` that calculates the maximum path sum in a binary tree. The `maxGain` method is used to recursively compute the maximum gain from each node, updating the global `maxSum` variable with the highest path sum found.

If you have any questions or need further assistance, feel free to ask!

## Counting Nodes in a Complete Binary Tree in java

Counting the number of nodes in a complete binary tree can be optimized by leveraging the properties of the tree. A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.

Here's an efficient approach to count the nodes in a complete binary tree using Java:

### Approach:
1. **Calculate the Depth:** Determine the depth of the tree.
2. **Binary Search:** Use binary search to count the nodes in the last level.

### Code Example:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class CompleteBinaryTree {
    public static void main(String[] args) {
        // Example tree construction
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);

        System.out.println("Number of nodes: " + countNodes(root));
    }

    public static int countNodes(TreeNode root) {
        if (root == null) return 0;

        int leftDepth = getDepth(root.left);
        int rightDepth = getDepth(root.right);

        if (leftDepth == rightDepth) {
            return (1 << leftDepth) + countNodes(root.right);
        } else {
            return (1 << rightDepth) + countNodes(root.left);
        }
    }

    private static int getDepth(TreeNode node) {
        int depth = 0;
        while (node != null) {
            depth++;
            node = node.left;
        }
        return depth;
    }
}
```

### Explanation:
1. **TreeNode Class:** Defines the structure of a tree node.
2. **countNodes Method:**
   - **Base Case:** If the root is null, return 0.
   - **Calculate Depths:** Get the depth of the left and right subtrees.
   - **Check Depths:** If the depths are equal, the left subtree is a perfect binary tree. Use the formula \(2^{\text{depth}} - 1\) to count the nodes in the left subtree and add the nodes in the right subtree.
   - **Recursive Call:** If the depths are not equal, the right subtree is a perfect binary tree. Use the same formula for the right subtree and add the nodes in the left subtree.
3. **getDepth Method:** Calculates the depth of the tree by traversing the leftmost path.

This approach ensures that the time complexity is \(O(\log^2 n)\), making it efficient for large trees.

Feel free to test this code and let me know if you have any questions or need further assistance!

## K Closest Points to Origin in java

To find the K closest points to the origin in Java, you can use a priority queue (min-heap) to efficiently manage and retrieve the closest points. Here's a step-by-step approach:

### Approach:
1. **Calculate the Distance:** Compute the Euclidean distance of each point from the origin.
2. **Use a Priority Queue:** Maintain a max-heap of size K to keep track of the K closest points.
3. **Iterate Through Points:** For each point, calculate its distance and manage the heap accordingly.

### Code Example:

```java
import java.util.PriorityQueue;
import java.util.Comparator;

class Point {
    int x, y;
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
}

public class KClosestPoints {
    public static void main(String[] args) {
        Point[] points = {
            new Point(1, 3),
            new Point(-2, 2),
            new Point(5, 8),
            new Point(0, 1)
        };
        int K = 2;
        Point[] closestPoints = findKClosestPoints(points, K);
        
        System.out.println("The " + K + " closest points to the origin are:");
        for (Point p : closestPoints) {
            System.out.println("(" + p.x + ", " + p.y + ")");
        }
    }

    public static Point[] findKClosestPoints(Point[] points, int K) {
        PriorityQueue<Point> maxHeap = new PriorityQueue<>(K, new Comparator<Point>() {
            public int compare(Point p1, Point p2) {
                return Double.compare(p2.distanceFromOrigin(), p1.distanceFromOrigin());
            }
        });

        for (Point point : points) {
            if (maxHeap.size() < K) {
                maxHeap.offer(point);
            } else if (point.distanceFromOrigin() < maxHeap.peek().distanceFromOrigin()) {
                maxHeap.poll();
                maxHeap.offer(point);
            }
        }

        Point[] result = new Point[K];
        for (int i = 0; i < K; i++) {
            result[i] = maxHeap.poll();
        }
        return result;
    }
}
```

### Explanation:
1. **Point Class:** Defines the structure of a point with `x` and `y` coordinates and a method to calculate the distance from the origin.
2. **findKClosestPoints Method:**
   - **Priority Queue:** Uses a max-heap to keep track of the K closest points. The comparator ensures that the point with the largest distance is at the top.
   - **Iterate Through Points:** For each point, if the heap size is less than K, add the point to the heap. If the heap is full and the current point is closer than the farthest point in the heap, replace the farthest point.
   - **Extract Results:** Extract the points from the heap to get the K closest points.
3. **Main Method:** Demonstrates the usage of the `findKClosestPoints` method with an example.

This approach ensures that the solution is efficient, with a time complexity of \(O(N \log K)\), where \(N\) is the number of points.

Feel free to test this code and let me know if you have any questions or need further assistance!

## Phone Directory Search Directory in java

Creating a phone directory search application in Java involves designing a simple data structure to store contact information and implementing search functionality. Here's a basic example using a `HashMap` to store the directory and a method to search for contacts by name:

### Code Example:

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class PhoneDirectory {
    private Map<String, String> directory;

    public PhoneDirectory() {
        directory = new HashMap<>();
    }

    public void addContact(String name, String phoneNumber) {
        directory.put(name, phoneNumber);
    }

    public String searchContact(String name) {
        return directory.getOrDefault(name, "Contact not found");
    }

    public static void main(String[] args) {
        PhoneDirectory phoneDirectory = new PhoneDirectory();
        phoneDirectory.addContact("Alice", "123-456-7890");
        phoneDirectory.addContact("Bob", "987-654-3210");
        phoneDirectory.addContact("Charlie", "555-555-5555");

        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter the name to search:");
        String name = scanner.nextLine();

        String result = phoneDirectory.searchContact(name);
        System.out.println("Phone number: " + result);
    }
}
```

### Explanation:
1. **PhoneDirectory Class:**
   - **directory:** A `HashMap` to store contact names as keys and phone numbers as values.
   - **addContact Method:** Adds a new contact to the directory.
   - **searchContact Method:** Searches for a contact by name and returns the phone number or a "Contact not found" message if the contact doesn't exist.

2. **Main Method:**
   - **Create Directory:** Initializes the phone directory and adds some sample contacts.
   - **User Input:** Prompts the user to enter a name to search for.
   - **Search and Display:** Searches the directory for the entered name and displays the result.

This basic implementation can be expanded with additional features such as deleting contacts, updating phone numbers, and more sophisticated search capabilities.

Would you like to add any specific features or functionalities to this phone directory application?

## Kth Ancestor in a Binary Tree

To find the Kth ancestor of a node in a binary tree, you can use a recursive approach to traverse the tree and keep track of the ancestors. Here's a step-by-step solution in Java:

### Approach:
1. **Recursive Traversal:** Traverse the tree recursively to find the target node.
2. **Track Ancestors:** Use a list or array to keep track of the ancestors.
3. **Return Kth Ancestor:** Once the target node is found, return the Kth ancestor from the list.

### Code Example:

```java
import java.util.ArrayList;
import java.util.List;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class KthAncestor {
    public static void main(String[] args) {
        // Example tree construction
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);

        int target = 5;
        int k = 2;
        TreeNode ancestor = findKthAncestor(root, target, k);
        if (ancestor != null) {
            System.out.println("The " + k + "th ancestor of node " + target + " is: " + ancestor.val);
        } else {
            System.out.println("The " + k + "th ancestor of node " + target + " does not exist.");
        }
    }

    public static TreeNode findKthAncestor(TreeNode root, int target, int k) {
        List<TreeNode> ancestors = new ArrayList<>();
        if (findNode(root, target, ancestors)) {
            if (ancestors.size() >= k) {
                return ancestors.get(ancestors.size() - k);
            }
        }
        return null;
    }

    private static boolean findNode(TreeNode node, int target, List<TreeNode> ancestors) {
        if (node == null) {
            return false;
        }
        if (node.val == target) {
            return true;
        }
        ancestors.add(node);
        if (findNode(node.left, target, ancestors) || findNode(node.right, target, ancestors)) {
            return true;
        }
        ancestors.remove(ancestors.size() - 1);
        return false;
    }
}
```

### Explanation:
1. **TreeNode Class:** Defines the structure of a tree node.
2. **findKthAncestor Method:**
   - **Ancestors List:** Uses a list to keep track of the ancestors during the traversal.
   - **findNode Method:** Recursively traverses the tree to find the target node and populates the ancestors list.
   - **Check Ancestors List:** After finding the target node, checks if the list has enough ancestors to return the Kth ancestor.
3. **findNode Method:**
   - **Base Case:** Returns false if the node is null.
   - **Target Node:** Returns true if the current node is the target node.
   - **Recursive Calls:** Adds the current node to the ancestors list and recursively searches the left and right subtrees.
   - **Backtracking:** Removes the current node from the ancestors list if the target node is not found in the current subtree.

This approach ensures that the tree is traversed efficiently, and the Kth ancestor is found if it exists.

Feel free to test this code and let me know if you have any questions or need further assistance!

## Find K-th Smallest Element in BST

To find the K-th smallest element in a Binary Search Tree (BST), you can perform an in-order traversal. An in-order traversal of a BST visits the nodes in ascending order, which makes it ideal for this task.

### Approach:
1. **In-order Traversal:** Traverse the tree in in-order fashion.
2. **Count Nodes:** Keep a count of the nodes visited.
3. **Return K-th Node:** When the count reaches K, return the node's value.

### Code Example:

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class KthSmallestElementBST {
    private static int count = 0;
    private static int result = -1;

    public static void main(String[] args) {
        // Example tree construction
        TreeNode root = new TreeNode(5);
        root.left = new TreeNode(3);
        root.right = new TreeNode(6);
        root.left.left = new TreeNode(2);
        root.left.right = new TreeNode(4);
        root.left.left.left = new TreeNode(1);

        kthSmallest = findKthSmallest(root, k);
        System.out.println("The " + k + "th smallest element in the BST is: " + kthSmallest);
    }

    public static int findKthSmallest(TreeNode root, int k) {
        inOrderTraversal(root, k);
        return result;
    }

    private static void inOrderTraversal(TreeNode node, int k) {
        if (node == null) {
            return;
        }

        inOrderTraversal(node.left, k);

        count++;
        if (count == k) {
            result = node.val;
           ;
        }

        inOrderTraversal(node.right, k);
    }
}
```

### Explanation:
1. **TreeNode Class:** Defines the structure of a tree node.
2. **findKthSmallest Method:**
   - **In-order Traversal:** Calls the `inOrderTraversal` method to traverse the tree.
   - **Return Result:** Returns the K-th smallest element found during the traversal.
3. **inOrderTraversal Method:**
   - **Base Case:** Returns if the node is null.
   - **Left Subtree:** Recursively traverses the left subtree.
   - **Count Nodes:** Increments the count of visited nodes. If the count equals K, sets the result to the current node's value and returns.
   - **Right Subtree:** Recursively traverses the right subtree.

This approach ensures that the tree is traversed in ascending order, and the K-th smallest element is found efficiently.

Feel free to test this code and let me know if you have any questions or need further assistance!

## 

## Find Minimum in Rotated Sorted Array
Sure! Here's a Java solution to find the minimum element in a rotated sorted array using a binary search approach:

```java
public class FindMinimumInRotatedSortedArray {
    public static int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            throw new IllegalArgumentException("Input array is empty or null");
        }

        int left = 0;
        int right = nums.length - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] > nums[right]) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }

        return nums[left];
    }

    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int min = findMin(nums);
        System.out.println("The minimum element is: " + min);
    }
}
```

This code defines a `FindMinimumInRotatedSortedArray` class with a method `findMin` that finds the minimum element in a rotated sorted array. The method uses a binary search approach to efficiently locate the minimum element.

If you have any questions or need further assistance, feel free to ask!

## Jump Game
Sure! Here's a Java solution to determine if you can reach the last index of an array where each element represents the maximum jump length at that position:

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
        return maxReach >= nums.length - 1;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        boolean result = canJump(nums);
        System.out.println("Can jump to the last index: " + result);
    }
}
```

This code defines a `JumpGame` class with a method `canJump` that determines if you can reach the last index of the array. The method uses a greedy approach to keep track of the maximum reachable index as it iterates through the array.

If you have any questions or need further assistance, feel free to ask!

## Jump Game II
Sure! Here's a Java solution to solve the Jump Game II problem, where you need to find the minimum number of jumps required to reach the last index of an array:

```java
public class JumpGameII {
    public static int jump(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int jumps = 0;
        int currentEnd = 0;
        int farthest = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);

            if (i == currentEnd) {
                jumps++;
                currentEnd = farthest;

                if (currentEnd >= nums.length - 1) {
                    break;
                }
            }
        }

        return jumps;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        int result = jump(nums);
        System.out.println("Minimum number of jumps to reach the last index: " + result);
    }
}
```

This code defines a `JumpGameII` class with a method `jump` that calculates the minimum number of jumps required to reach the last index of the array. The method uses a greedy approach to keep track of the farthest point that can be reached and increments the jump count whenever the current end of the reachable range is reached.

If you have any questions or need further assistance, feel free to ask!

## Partition Labels

Sure! Here's a Java solution to solve the Partition Labels problem, where you need to partition a string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts:

```java
import java.util.ArrayList;
import java.util.List;

public class PartitionLabels {
    public static List<Integer> partitionLabels(String s) {
        List<Integer> result = new ArrayList<>();
        int[] lastIndex = new int[26];

        // Record the last index of each character
        for (int i = 0; i < s.length(); i++) {
            lastIndex[s.charAt(i) - 'a'] = i;
        }

        int start = 0;
        int end = 0;

        // Iterate through the string to partition it
        for (int i = 0; i < s.length(); i++) {
            end = Math.max(end, lastIndex[s.charAt(i) - 'a']);
            if (i == end) {
                result.add(end - start + 1);
                start = i + 1;
            }
        }

        return result;
    }

    public static void main(String[] args) {
        String s = "ababcbacadefegdehijhklij";
        List<Integer> partitions = partitionLabels(s);
        System.out.println("Partition sizes: " + partitions);
    }
}
```

This code defines a `PartitionLabels` class with a method `partitionLabels` that partitions the string into as many parts as possible so that each letter appears in at most one part. The method uses an array to record the last index of each character and iterates through the string to determine the partitions.

If you have any questions or need further assistance, feel free to ask!

## Find First and Last Position of Element in Sorted Array
Sure! Here's a Java solution to find the first and last position of a given target element in a sorted array using binary search:

```java
public class FindFirstAndLastPosition {
    public static int[] searchRange(int[] nums, int target) {
        int[] result = {-1, -1};
        result[0] = findFirstPosition(nums, target);
        result[1] = findLastPosition(nums, target);
        return result;
    }

    private static int findFirstPosition(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int firstPosition = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                firstPosition = mid;
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return firstPosition;
    }

    private static int findLastPosition(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int lastPosition = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                lastPosition = mid;
                left = mid + 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return lastPosition;
    }

    public static void main(String[] args) {
        int[] nums = {5, 7, 7, 8, 8, 10};
        int target = 8;
        int[] positions = searchRange(nums, target);
        System.out.println("First and Last Position: [" + positions[0] + ", " + positions[1] + "]");
    }
}
```

This code defines a `FindFirstAndLastPosition` class with a method `searchRange` that finds the first and last positions of a given target element in a sorted array. The `findFirstPosition` and `findLastPosition` methods use binary search to efficiently locate the target element's positions.

If you have any questions or need further assistance, feel free to ask!

## Search Insert Position
Sure, I can help with that! The "Search Insert Position" problem involves finding the index at which a target value should be inserted into a sorted array. Here's a simple implementation in Java:

```java
public class SearchInsertPosition {
    public static int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return left;
    }

    public static void main(String[] args) {
        int[] nums = {1, 3, 5, 6};
        int target = 5;
        System.out.println(searchInsert(nums, target)); // Output: 2

        target = 2;
        System.out.println(searchInsert(nums, target)); // Output: 1

        target = 7;
        System.out.println(searchInsert(nums, target)); // Output: 4

        target = 0;
        System.out.println(searchInsert(nums, target)); // Output: 0
    }
}
```

This code does the following:
1. Uses a binary search algorithm to find the target or the position where it should be inserted.
2. If the target is found, it returns the index.
3. If the target is not found, it returns the index where the target should be inserted to maintain the sorted order.

You can run this code to see how it works with different target values. If you have any questions or need further assistance, feel free to ask!



## Binary Tree inorder/preorder/postorder
Sure, I can help with that! Traversing a binary tree can be done in three common ways: inorder, preorder, and postorder. Here are the implementations for each traversal in Java:

### Inorder Traversal (Left, Root, Right)
```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeInorderTraversal {
    public void inorderTraversal(TreeNode root) {
        if (root != null) {
            inorderTraversal(root.left);
            System.out.print(root.val + " ");
            inorderTraversal(root.right);
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.right = new TreeNode(2);
        root.right.left = new TreeNode(3);

        BinaryTreeInorderTraversal tree = new BinaryTreeInorderTraversal();
        tree.inorderTraversal(root); // Output: 1 3 2
    }
}
```

### Preorder Traversal (Root, Left, Right)
```java
public class BinaryTreePreorderTraversal {
    public void preorderTraversal(TreeNode root) {
        if (root != null) {
            System.out.print(root.val + " ");
            preorderTraversal(root.left);
            preorderTraversal(root.right);
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.right = new TreeNode(2);
        root.right.left = new TreeNode(3);

        BinaryTreePreorderTraversal tree = new BinaryTreePreorderTraversal();
        tree.preorderTraversal(root); // Output: 1 2 3
    }
}
```

### Postorder Traversal (Left, Right, Root)
```java
public class BinaryTreePostorderTraversal {
    public void postorderTraversal(TreeNode root) {
        if (root != null) {
            postorderTraversal(root.left);
            postorderTraversal(root.right);
            System.out.print(root.val + " ");
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.right = new TreeNode(2);
        root.right.left = new TreeNode(3);

        BinaryTreePostorderTraversal tree = new BinaryTreePostorderTraversal();
        tree.postorderTraversal(root); // Output: 3 2 1
    }
}
```

These implementations will help you traverse a binary tree in different orders. If you have any questions or need further assistance, feel free to ask!
## Binary Tree Hieght
Sure, I can help with that! Calculating the height of a binary tree involves finding the longest path from the root node to a leaf node. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeHeight {
    public int height(TreeNode root) {
        if (root == null) {
            return 0;
        } else {
            int leftHeight = height(root.left);
            int rightHeight = height(root.right);
            return Math.max(leftHeight, rightHeight) + 1;
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);

        BinaryTreeHeight tree = new BinaryTreeHeight();
        System.out.println("Height of the tree is: " + tree.height(root)); // Output: 3
    }
}
``This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements a `height` method that recursively calculates the height of the tree.
3. Uses the `Math.max` function to determine the maximum height between the left and right subtrees and adds 1 to account for the current node.

You can run this code to calculate the height of a binary tree. If you have any questions or need further assistance, feel free to ask!
```
## Binary Tree Diameter
Sure, I can help with that! The diameter of a binary tree is the length of the longest path between any two nodes in the tree. This path may or may not pass through the root. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeDiameter {
    private int diameter;

    public int diameterOfBinaryTree(TreeNode root) {
        diameter = 0;
        height(root);
        return diameter;
    }

    private int height(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int leftHeight = height(node.left);
        int rightHeight = height(node.right);
        diameter = Math.max(diameter, leftHeight + rightHeight);
        return Math.max(leftHeight, rightHeight) + 1;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);

        BinaryTreeDiameter tree = new BinaryTreeDiameter();
        System.out.println("Diameter of the tree is: " + tree.diameterOfBinaryTree(root)); // Output: 3
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements a `diameterOfBinaryTree` method that initializes the diameter and calls a helper method to calculate the height.
3. The `height` method recursively calculates the height of the tree and updates the diameter by considering the sum of the heights of the left and right subtrees at each node.

You can run this code to calculate the diameter of a binary tree. If you have any questions or need further assistance, feel free to ask!
## Maximum Depth of Tree
Sure, I can help with that! The maximum depth (or height) of a binary tree is the number of nodes along the longest path from the root node down to the farthest leaf node. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class MaximumDepthOfBinaryTree {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        } else {
            int leftDepth = maxDepth(root.left);
            int rightDepth = maxDepth(root.right);
            return Math.max(leftDepth, rightDepth) + 1;
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);

        MaximumDepthOfBinaryTree tree = new MaximumDepthOfBinaryTree();
        System.out.println("Maximum depth of the tree is: " + tree.maxDepth(root)); // Output: 3
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements a `maxDepth` method that recursively calculates the maximum depth of the tree.
3. Uses the `Math.max` function to determine the maximum depth between the left and right subtrees and adds 1 to account for the current node.

You can run this code to calculate the maximum depth of a binary tree. If you have any questions or need further assistance, feel free to ask!
## Sum root of leaf of binary tree
Sure, I can help with that! Calculating the sum of all root-to-leaf paths in a binary tree involves traversing the tree and summing up the values from the root to each leaf node. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class SumRootToLeaf {
    public int sumNumbers(TreeNode root) {
        return sumNumbersHelper(root, 0);
    }

    private int sumNumbersHelper(TreeNode node, int currentSum) {
        if (node == null) {
            return 0;
        }
        currentSum = currentSum * 10 + node.val;
        if (node.left == null && node.right == null) {
            return currentSum;
        }
        return sumNumbersHelper(node.left, currentSum) + sumNumbersHelper(node.right, currentSum);
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);

        SumRootToLeaf tree = new SumRootToLeaf();
        System.out.println("Sum of root-to-leaf numbers: " + tree.sumNumbers(root)); // Output: 25
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements a `sumNumbers` method that initializes the sum and calls a helper method.
3. The `sumNumbersHelper` method recursively calculates the sum of all root-to-leaf paths by traversing the tree and updating the current sum at each node.

You can run this code to calculate the sum of all root-to-leaf paths in a binary tree. If you have any questions or need further assistance, feel free to ask!
## Mirror view of Binary Tree
Sure, I can help with that! Creating a mirror view (or inverted view) of a binary tree involves swapping the left and right children of all nodes in the tree. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class MirrorBinaryTree {
    public TreeNode mirrorTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        TreeNode left = mirrorTree(root.left);
        TreeNode right = mirrorTree(root.right);
        root.left = right;
        root.right = left;
        return root;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);

        MirrorBinaryTree tree = new MirrorBinaryTree();
        TreeNode mirroredRoot = tree.mirrorTree(root);

        // Function to print the tree in inorder traversal
        printInorder(mirroredRoot); // Output: 3 1 5 2 4
    }

    // Helper function to print the tree in inorder traversal
    public static void printInorder(TreeNode node) {
        if (node != null) {
            printInorder(node.left);
            System.out.print(node.val + " ");
            printInorder(node.right);
        }
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2 `mirrorTree` method that recursively swaps the left and right children of each node.
3. Includes a `printInorder` helper method to print the tree in inorder traversal for verification.

You can run this code to create and verify the mirror view of a binary tree. If you have any questions or need further assistance, feel free to ask!

## Binary Tree level order
Sure, I can help with that! Level order traversal of a binary tree involves visiting each node level by level from left to right. This can be achieved using a queue. Here's a simple implementation in Java:

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeLevelOrderTraversal {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            List<Integer> currentLevel = new ArrayList<>();

            for (int i = 0; i < levelSize; i++) {
                TreeNode currentNode = queue.poll();
                currentLevel.add(currentNode.val);

                if (currentNode.left != null) {
                    queue.add(currentNode.left);
                }
                if (currentNode.right != null) {
                    queue.add(currentNode.right);
                }
            }
            result.add(currentLevel);
        }
        return result;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);

        BinaryTreeLevelOrderTraversal tree = new BinaryTreeLevelOrderTraversal();
        List<List<Integer>> result = tree.levelOrder(root);

        for (List<Integer> level : result) {
            System.out.println(level);
        }
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements a `levelOrder` method that uses a queue to traverse the tree level by level.
3. Adds each level's nodes to a list and then adds that list to the result.

You can run this code to perform a level order traversal of a binary tree. If you have any questions or need further assistance, feel free to ask!
## Binary Tree Top View
Sure, I can help with that! The top view of a binary tree is the set of nodes visible when the tree is viewed from the top. To achieve this, we can use a level-order traversal with a queue and a map to keep track of the horizontal distance of nodes from the root. Here's a simple implementation in Java:

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeTopView {
    static class Pair {
        TreeNode node;
        int hd; // horizontal distance

        Pair(TreeNode node, int hd) {
            this.node = node;
            this.hd = hd;
        }
    }

    public List<Integer> topView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Map<Integer, Integer> map = new TreeMap<>();
        Queue<Pair> queue = new LinkedList<>();
        queue.add(new Pair(root, 0));

        while (!queue.isEmpty()) {
            Pair current = queue.poll();
            TreeNode node = current.node;
            int hd = current.hd;

            if (!map.containsKey(hd)) {
                map.put(hd, node.val);
            }

            if (node.left != null) {
                queue.add(new Pair(node.left, hd - 1));
            }
            if (node.right != null) {
                queue.add(new Pair(node.right, hd + 1));
            }
        }

        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            result.add(entry.getValue());
        }

        return result;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);

        BinaryTreeTopView tree = new BinaryTreeTopView();
        List<Integer> topView = tree.topView(root);

        System.out.println("Top view of the binary tree: " + topView); // Output: [4, 2, 1, 3, 7]
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Uses a `Pair` class to store nodes along with their horizontal distance from the root.
3. Implements a `topView` method that performs a level-order traversal using a queue and a map to track the first node encountered at each horizontal distance.
4. Collects the values from the map to form the top view of the tree.

You can run this code to get the top view of a binary tree. If you have any questions or need further assistance, feel free to ask!
## Binary Tree Left view
Sure, I can help with that! The left view of a binary tree is the set of nodes visible when the tree is viewed from the left side. To achieve this, we can use a level-order traversal and keep track of the first node at each level. Here's a simple implementation in Java:

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeLeftView {
    public List<Integer> leftView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            for (int i = 0; i < levelSize; i++) {
                TreeNode currentNode = queue.poll();
                if (i == 0) {
                    result.add(currentNode.val);
                }
                if (currentNode.left != null) {
                    queue.add(currentNode.left);
                }
                if (currentNode.right != null) {
                    queue.add(currentNode.right);
                }
            }
        }
        return result;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);

        BinaryTreeLeftView tree = new BinaryTreeLeftView();
        List<Integer> leftView = tree.leftView(root);

        System.out.println("Left view of the binary tree: " + leftView); // Output: [1, 2, 4]
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements a `leftView` method that uses a queue to perform a level-order traversal.
3. Adds each level to the result list.

You can run this code to get the left view of a binary tree. If you have any questions or need further assistance, feel free to ask!
## Flatten Binary Tree to Linked List
Sure, I can help with that! Flattening a binary tree to a linked list involves transforming the tree into a "right-skewed" tree where each node's right child points to the next node in a pre-order traversal. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class FlattenBinaryTree {
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }

        TreeNode current = root;
        while (current != null) {
            if (current.left != null) {
                TreeNode rightmost = current.left;
                while (rightmost.right != null) {
                    rightmost = rightmost.right;
                }
                rightmost.right = current.right;
                current.right = current.left;
                current.left = null;
            }
            current = current.right;
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(5);
        root.left.left = new TreeNode(3);
        root.left.right = new TreeNode(4);
        root.right.right = new TreeNode(6);

        FlattenBinaryTree tree = new FlattenBinaryTree();
        tree.flatten(root);

        // Function to print the flattened tree
        printFlattenedTree(root); // Output: 1 2 3 4 5 6
    }

    // Helper function to print the flattened tree
    public static void printFlattenedTree(TreeNode root) {
        TreeNode current = root;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.right;
        }
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements a `flatten` method that transforms the tree into a linked list using a pre-order traversal.
3. Includes a `printFlattenedTree` helper method to print the flattened tree for verification.

You can run this code to flatten a binary tree into a linked list. If you have any questions or need further assistance, feel free to ask!

## Binary Search Tree
Sure, I can help with that! Building a Binary Search Tree (BST) from an array involves inserting each element of the array into the BST. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BuildBST {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        if (val < root.val) {
            root.left = insertIntoBST(root.left, val);
        } else {
            root.right = insertIntoBST(root.right, val);
        }
        return root;
    }

    public TreeNode buildBST(int[] nums) {
        TreeNode root = null;
        for (int num : nums) {
            root = insertIntoBST(root, num);
        }
        return root;
    }

    public static void main(String[] args) {
        int[] nums = {5, 3, 8, 1, 4, 7, 10};
        BuildBST tree = new BuildBST();
        TreeNode root = tree.buildBST(nums);

        Function to print the tree in inorder traversal
        printInorder(root); // Output: 1 3 4 5 7 8 10
    }

    // Helper function to print the tree in inorder traversal
    public static void printInorder(TreeNode node) {
        if (node != null) {
            printInorder(node.left);
            System.out.print(node.val + " ");
            printInorder(node.right);
        }
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements an `insertIntoBST` method that inserts a value into the BST.
3. Implements a `buildBST` method that builds the BST from an array by inserting each element.
4. Includes a `printInorder` helper method to print the tree in inorder traversal for verification.

You can run this code to build a Binary Search Tree from an array and verify it by printing the inorder traversal. If you have any questions or need further assistance, feel free to ask!

## Symmetric Tree

Sure! Here's a Java solution to check if a binary tree is symmetric around its center:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class SymmetricTree {
    public static boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return isMirror(root.left, root.right);
    }

    private static boolean isMirror(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        }
        if (left == null || right == null) {
            return false;
        }
        return (left.val == right.val)
                && isMirror(left.left, right.right)
                && isMirror(left.right, right.left);
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(2);
        root.left.left = new TreeNode(3);
        root.left.right = new TreeNode(4);
        root.right.left = new TreeNode(4);
        root.right.right = new TreeNode(3);

        boolean result = isSymmetric(root);
        System.out.println("Is the tree symmetric? " + result);
    }
}
```

This code defines a `SymmetricTree` class with a method `isSymmetric` that checks if a binary tree is symmetric. The `isMirror` method is used to recursively compare the left and right subtrees to determine if they are mirror images of each other.

If you have any questions or need further assistance, feel free to ask!

## Convert Sorted Array to Binary Search Tree
Sure! Here's a Java solution to convert a sorted array into a height-balanced binary search tree (BST):

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class ConvertSortedArrayToBST {
    public static TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0) {
            return null;
        }
        return convertToBST(nums, 0, nums.length - 1);
    }

    private static TreeNode convertToBST(int[] nums, int left, int right) {
        if (left > right) {
            return null;
        }

        int mid = left + (right - left) / 2;
        TreeNode node = new TreeNode(nums[mid]);
        node.left = convertToBST(nums, left, mid - 1);
        node.right = convertToBST(nums, mid + 1, right);
        return node;
    }

    public static void main(String[] args) {
        int[] nums = {-10, -3, 0, 5, 9};
        TreeNode root = sortedArrayToBST(nums);
        printTree(root);
    }

    private static void printTree(TreeNode node) {
        if (node != null) {
            printTree(node.left);
            System.out.print(node.val + " ");
            printTree(node.right);
        }
    }
}
```

This code defines a `ConvertSortedArrayToBST` class with a method `sortedArrayToBST` that converts a sorted array into a height-balanced BST. The `convertToBST` method is used to recursively build the tree by selecting the middle element as the root and constructing the left and right subtrees.

If you have any questions or need further assistance, feel free to ask!
## Flatten Binary Tree to Linked List in java

Sure! Here's a Java solution to flatten a binary tree to a linked list in-place:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class FlattenBinaryTreeToLinkedList {
    public static void flatten(TreeNode root) {
        if (root == null) {
            return;
        }

        TreeNode current = root;
        while (current != null) {
            if (current.left != null) {
                TreeNode rightmost = current.left;
                while (rightmost.right != null) {
                    rightmost = rightmost.right;
                }
                rightmost.right = current.right;
                current.right = current.left;
                current.left = null;
            }
            current = current.right;
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(5);
        root.left.left = new TreeNode(3);
        root.left.right = new TreeNode(4);
        root.right.right = new TreeNode(6);

        flatten(root);
        printLinkedList(root);
    }

    private static void printLinkedList(TreeNode node) {
        while (node != null) {
            System.out.print(node.val + " ");
            node = node.right;
        }
    }
}
```

This code defines a `FlattenBinaryTreeToLinkedList` class with a method `flatten` that flattens a binary tree to a linked list in-place. The method uses an iterative approach to rearrange the tree nodes.

If you have any questions or need further assistance, feel free to ask!

## Binary Tree Right Side View

Sure! Here's a Java solution to get the right side view of a binary tree using a level-order traversal approach:

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BinaryTreeRightSideView {
    public static List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            for (int i = 0; i < levelSize; i++) {
                TreeNode currentNode = queue.poll();
                if (i == levelSize - 1) {
                    result.add(currentNode.val);
                }
                if (currentNode.left != null) {
                    queue.offer(currentNode.left);
               .right != null) {
                    queue.offer(currentNode.right);
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.right = new TreeNode(5);
        root.right.right = new TreeNode(4);

        List<Integer> rightView = rightSideView(root);
        System.out.println("Right Side View: " + rightView);
    }
}
```

This code defines a `BinaryTreeRightSideView` class with a method `rightSideView` that returns the right side view of a binary tree. The method uses a level-order traversal (BFS) to capture the last node at each level, which represents the rightmost node visible from the right side.

If you have any questions or need further assistance, feel free to ask!

##  Invert Binary Tree

Sure! Here's a Java solution to invert a binary tree:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class InvertBinaryTree {
    public static TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }

        TreeNode left = invertTree(root.left);
        TreeNode right = invertTree(root.right);

        root.left = right;
        root.right = left;

        return root;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(4);
        root.left = new TreeNode(2);
        root.right = new TreeNode(7);
        root.left.left = new TreeNode(1);
        root.left.right = new TreeNode(3);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(9);

        TreeNode invertedRoot = invertTree(root);
        printTree(invertedRoot);
    }

    private static void printTree(TreeNode node) {
        if (node != null) {
           .left);
            System.out.print(node.val + " ");
            printTree(node.right);
        }
    }
}
```

This code defines an `InvertBinaryTree` class with a method `invertTree` that inverts a binary tree. The method uses a recursive approach to swap the left and right children of each node.

If you have any questions or need further assistance, feel free to ask!

## Kth Smallest Element in a BST
Sure! Here's a Java solution to find the k-th smallest element in a Binary Search Tree (BST) using an in-order traversal:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class KthSmallestElementInBST {
    private static int count = 0;
    private static int result = -1;

    public static int kthSmallest(TreeNode root, int k) {
        inOrderTraversal(root, k);
        return result;
    }

    private static void inOrderTraversal(TreeNode node, int k) {
        if (node == null) {
            return;
        }

        inOrderTraversal(node.left, k);

        count++;
        if (count == k) {
            result = node.val;
            return;
        }

        inOrderTraversal(node.right, k);
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(3);
        root.left = new TreeNode(1);
        root.right = new TreeNode(4);
        root.left.right = new TreeNode(2);

        int k = 2;
        int kthSmallest = kthSmallest(root, k);
        System.out.println("The " + k + "-th smallest element is: " + kthSmallest);
    }
}
```

This code defines a `KthSmallestElementInBST` class with a method `kthSmallest` that finds the k-th smallest element in a BST. The method uses an in-order traversal to visit nodes in ascending order and keeps track of the count to identify the k-th smallest element.

If you have any questions or need further assistance, feel free to ask!

##  Lowest Common Ancestor of a Binary Tree

Sure! Here's a Java solution to find the lowest common ancestor (LCA) of two nodes in a binary tree:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class LowestCommonAncestor {
    public static TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null) {
            return root;
        }

        return left != null ? left : right;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(3);
        root.left = new TreeNode(5);
        root.right = new TreeNode(1);
        root.left.left = new TreeNode(6);
        root.left.right = new TreeNode(2);
        root.right.left = new TreeNode(0);
        root.right.right = new TreeNode(8);
        root.left.right.left = new TreeNode(7);
        root.left.right.right = new TreeNode(4);

        TreeNode p = root.left; // Node with value 5
        TreeNode q = root.left.right.right; // Node with value 4

        TreeNode lca = lowestCommonAncestor(root, p, q);
        System.out.println("Lowest Common Ancestor: " + lca.val);
    }
}
```

This code defines a `LowestCommonAncestor` class with a method `lowestCommonAncestor` that finds the LCA of two nodes in a binary tree. The method uses a recursive approach to traverse the tree and determine the LCA.

If you have any questions or need further assistance, feel free to ask!

## Path Sum III
Sure! Here's a Java solution to find the number of paths that sum to a given value in a binary tree. This solution uses a recursive approach along with a hashmap to store the cumulative sum frequencies:

```java
import java.util.HashMap;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class PathSumIII {
    public static int pathSum(TreeNode root, int sum) {
        HashMap<Integer, Integer> prefixSumCount = new HashMap<>();
        prefixSumCount.put(0, 1); // Base case to handle sum from root
        return dfs(root, 0, sum, prefixSumCount);
    }

    private static int dfs(TreeNode node, int currentSum, int target, HashMap<Integer, Integer> prefixSumCount) {
        if (node == null) {
            return 0;
        }

        currentSum += node.val;
        int numPathsToCurr = prefixSumCount.getOrDefault(currentSum - target, 0);
        prefixSumCount.put(currentSum, prefixSumCount.getOrDefault(currentSum, 0) + 1);

        int result = numPathsToCurr + dfs(node.left, currentSum, target, prefixSumCount) + dfs(node.right, currentSum, target, prefixSumCount);

        prefixSumCount.put(currentSum, prefixSumCount.get(currentSum) - 1); // Remove the current node's sum from the hashmap

        return result;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(10);
        root.left = new TreeNode(5);
        root.right = new TreeNode(-3);
        root.left.left = new TreeNode(3);
        root.left.right = new TreeNode(2);
        root.right.right = new TreeNode(11);
        root.left.left.left = new TreeNode(3);
        root.left.left.right = new TreeNode(-2);
        root.left.right.right = new TreeNode(1);

        int sum = 8;
        int result = pathSum(root, sum);
        System.out.println("Number of paths with sum " + sum + ": " + result);
    }
}
```

This code defines a `PathSumIII` class with a method `pathSum` that calculates the number of paths that sum to a given value in a binary tree. The `dfs` method is used to perform a depth-first search, and a hashmap is used to store the cumulative sum frequencies to efficiently find the number of valid paths.

If you have any questions or need further assistance, feel free to ask!

## Validate Binary Search Tree
Sure, I can help with that! Validating a Binary Search Tree (BST) involves ensuring that for every node, all nodes in its left subtree are less than the node's value, and all nodes in its right subtree are greater than the node's value. Here's a simple implementation in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class ValidateBST {
    public boolean isValidBST(TreeNode root) {
        return isValidBSTHelper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean isValidBSTHelper(TreeNode node, long min, long max) {
        if (node == null) {
            return true;
        }
        if (node.val <= min || node.val >= max) {
            return false;
        }
        return isValidBSTHelper(node.left, min, node.val) && isValidBSTHelper(node.right, node.val, max);
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(2);
        root.left = new TreeNode(1);
        root.right = new TreeNode(3);

        ValidateBST tree = new ValidateBST();
        System.out.println("Is the tree a valid BST? " + tree.isValidBST(root)); // Output: true
    }
}
```

This code does the following:
1. Defines a `TreeNode` class to represent each node in the binary tree.
2. Implements an `isValidBST` method that initializes the validation process.
3. Uses a helper method `isValidBSTHelper` that recursively checks if the tree satisfies the BST properties by ensuring each node's value is within a valid range.

You can run this code to validate whether a binary tree is a BST. If you have any questions or need further assistance, feel free to ask!
## Median of Two Sorted Arrays
Sure, I can help with that! Using a priority queue (min-heap and max-heap) to find the median of two sorted arrays is an interesting approach. Here's how you can do it in Java:

```java
import java.util.PriorityQueue;

public class MedianOfTwoSortedArraysUsingPQ {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);

        for (int num : nums1) {
            addNumber(num, minHeap, maxHeap);
        }
        for (int num : nums2) {
            addNumber(num, minHeap, maxHeap);
        }

        return getMedian(minHeap, maxHeap);
    }

    private void addNumber(int num, PriorityQueue<Integer> minHeap, PriorityQueue<Integer> maxHeap) {
        if (maxHeap.isEmpty() || num <= maxHeap.peek()) {
            maxHeap.add(num);
        } else {
            minHeap.add(num);
        }

        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.add(maxHeap.poll());
        } else if (minHeap.size() > maxHeap.size()) {
            maxHeap.add(minHeap.poll());
        }
    }

    private double getMedian(PriorityQueue<Integer> minHeap, PriorityQueue<Integer> maxHeap) {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        } else {
            return maxHeap.peek();
        }
    }

    public static void main(String[] args) {
        MedianOfTwoSortedArraysUsingPQ solution = new MedianOfTwoSortedArraysUsingPQ();
        int[] nums1 = {1, 3};
        int[] nums2 = {2};
        System.out.println("Median is: " + solution.findMedianSortedArrays(nums1, nums2)); // Output: 2.0

        int[] nums1 = {1, 2};
        int[] nums2 = {3, 4};
        System.out.println("Median is: " + solution.findMedianSortedArrays(nums1, nums2)); // Output: 2.5
    }
}
```

This code does the following:
1. Uses two priority queues (min-heap and max-heap) to maintain the lower and upper halves of the numbers.
2. Adds numbers to the appropriate heap and balances the heaps to ensure the size difference is at most one.
3. Calculates the median based on the sizes of the heaps.

You can run this code to find the median of two sorted arrays using priority queues. If you have any questions or need further assistance, feel free to ask!

## Min Heap with Heapify
Sure, I can help with that! A Min Heap is a binary tree where the value of each node is less than or equal to the values of its children. Heapify is the process of converting a binary tree into a heap. Here's a simple implementation of a Min Heap with heapify in Java:

```java
import java.util.Arrays;

public class MinHeap {
    private int[] heap;
    private int size;
    private int capacity;

    public MinHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.heap = new int[capacity];
    }

    private int parent(int i) { return (i - 1) / 2; }
    private int leftChild(int i) { return 2 * i + 1; }
    private int rightChild(int i) { return 2 * i + 2; }

    private void swap(int i, int j) {
        int temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }

    public void insert(int key) {
        if (size == capacity) {
            throw new IllegalStateException("Heap is full");
        }
        size++;
        int i = size - 1;
        heap[i] = key;

        while (i != 0 && heap[parent(i)] > heap[i]) {
            swap(i, parent(i));
            i = parent(i);
        }
    }

    public void heapify(int i) {
        int smallest = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < size && heap[left] < heap[smallest]) {
            smallest = left;
        }
        if (right < size && heap[right] < heap[smallest]) {
            smallest = right;
        }
        if (smallest != i) {
            swap(i, smallest);
            heapify(smallest);
        }
    }

    public int extractMin() {
        if (size <= 0) {
            throw new IllegalStateException("Heap is empty");
        }
        if (size == 1) {
            size--;
            return heap[0];
        }

        int root = heap[0];
        heap[0] = heap[size - 1];
        size--;
        heapify(0);

        return root;
    }

    public void buildHeap(int[] arr) {
        if (arr.length > capacity) {
            throw new IllegalStateException("Array size exceeds heap capacity");
        }
        size = arr.length;
        heap = Arrays.copyOf(arr, arr.length);

        for (int i = size / 2 - 1; i >= 0; i--) {
            heapify(i);
        }
    }

    public void printHeap() {
        for (int i = 0; i < size; i++) {
            System.out.print(heap[i] + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        MinHeap minHeap = new MinHeap(10);
        int[] arr = {3, 2, 1, 5, 4, 6};
        minHeap.buildHeap(arr);
        minHeap.printHeap(); // Output: 1 2 3 5 4 6

        minHeap.insert(0);
        minHeap.printHeap(); // Output: 0 1 3 2 4 6 5

        System.out.println("Extracted min: " + minHeap.extractMin()); // Output: 0
        minHeap.printHeap(); // Output: 1 2 3 5 4 6
    }
}
```

This code does the following:
1. Defines a `MinHeap` class with methods for inserting elements, heapifying, extracting the minimum element, and building a heap from an array.
2. Uses a `heapify` method to maintain the heap property.
3. Includes a `buildHeap` method to convert an array into a heap.
4. Provides a `printHeap` method to display the heap elements.

You can run this code to create and manipulate a Min Heap. If you have any questions or need further assistance, feel free to ask!
## Kth Largest Element in an Array
Sure, I can help with that! Finding the k-th largest element in an array can be efficiently done using a min-heap (priority queue). Here's a simple implementation in Java:

```java
import java.util.PriorityQueue;

public class KthLargestElement {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (int num : nums) {
            minHeap.add(num);
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

        return minHeap.peek();
    }

    public static void main(String[] args) {
        KthLargestElement solution = new KthLargestElement();
        int[] nums = {3, 2, 1, 5, 6, 4};
        int k = 2;
        System.out.println("The " + k + "-th largest element is: " + solution.findKthLargest(nums, k)); // Output: 5

        nums = new int[]{3, 2, 3, 1, 2, 4, 5, 5, 6};
        k = 4;
        System.out.println("The " + k + "-th largest element is: " + solution.findKthLargest(nums, k)); // Output: 4
    }
}
```

This code does the following:
1. Uses a `PriorityQueue` (min-heap) to keep track of the k largest elements.
2. Adds elements to the heap and removes the smallest element if the heap size exceeds k.
3. The root of the heap (the smallest element in the heap) will be the k-th largest element in the array.

You can run this code to find the k-th largest element in an array. If you have any questions or need further assistance, feel free to ask!

## Find Median from Data Stream
Sure, I can help with that! Finding the median from a data stream can be efficiently done using two heaps: a max-heap to store the smaller half of the numbers and a min-heap to store the larger half. Here's a simple implementation in Java:

```java
import java.util.PriorityQueue;
import java.util.Collections;

public class MedianFinder {
    private PriorityQueue<Integer> maxHeap; // to store the smaller half of the numbers
    private PriorityQueue<Integer> minHeap; // to store the larger half of the numbers

    public MedianFinder() {
        maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        minHeap = new PriorityQueue<>();
    }

    public void addNum(int num) {
        if (maxHeap.isEmpty() || num <= maxHeap.peek()) {
            maxHeap.add(num);
        } else {
            minHeap.add(num);
        }

        // Balance the heaps
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.add(maxHeap.poll());
        } else if (minHeap.size() > maxHeap.size()) {
            maxHeap.add(minHeap.poll());
        }
    }

    public double findMedian() {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        } else {
            return maxHeap.peek();
        }
    }

    public static void main(String[] args) {
        MedianFinder medianFinder = new MedianFinder();
        medianFinder.addNum(1);
        medianFinder.addNum(2);
        System.out.println("Median is: " + medianFinder.findMedian()); // Output: 1.5
        medianFinder.addNum(3);
        System.out.println("Median is: " + medianFinder.findMedian()); // Output: 2.0
    }
}
```

This code does the following:
1. Uses two priority queues (max-heap and min-heap) to maintain the lower and upper halves of the numbers.
2. Adds numbers to the appropriate heap and balances the heaps to ensure the size difference is at most one.
3. Calculates the median based on the sizes of the heaps.

You can run this code to find the median from a data stream. If you have any questions or need further assistance, feel free to ask!

## Find K Pairs with Smallest Sums

Sure! Here's a Java implementation to find the K pairs with the smallest sums:

```java
import java.util.*;

public class KSmallestPairs {
    public List<int[]> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        List<int[]> result = new ArrayList<>();
        if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0 || k <= 0) {
            return result;
        }

        PriorityQueue<int[]> minHeap = new PriorityQueue<>(Comparator.comparingInt(a -> a[0] + a[1]));
        for (int i = 0; i < Math.min(k, nums1.length); i++) {
            minHeap.offer(new int[]{nums1[i], nums2[0], 0});
        }

        while (k-- > 0 && !minHeap.isEmpty()) {
            int[] curr = minHeap.poll();
            result.add(new int[]{curr[0], curr[1]});
            if (curr[2] + 1 < nums2.length) {
                minHeap.offer(new int[]{curr[0], nums2[curr[2] + 1], curr[2] + 1});
            }
        }

        return result;
    }

    public static void main(String[] args) {
        KSmallestPairs solution = new KSmallestPairs();
        int[] nums1 = {1, 7, 11};
        int[] nums2 = {2, 4, 6};
        int k = 3;
        List<int[]> result = solution.kSmallestPairs(nums1, nums2, k);
        for (int[] pair : result) {
            System.out.println(Arrays.toString(pair));
        }
    }
}
```

This code uses a priority queue (min-heap) to keep track of the smallest pairs. It initializes the heap with the smallest possible sums and iteratively extracts the smallest pairs while pushing the next possible pairs into the heap.

Feel free to ask if you have any questions or need further assistance!

## Create Single Linked List
Sure! Here's an implementation of a singly linked list in Java with head and tail pointers, including methods for inserting and deleting nodes at both the head and tail, reversing the list, and finding the middle element:

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    Node head;
    Node tail;

    // Method to insert a node at the head
    public void insertHead(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = tail = newNode;
        } else {
            newNode.next = head;
            head = newNode;
        }
    }

    // Method to insert a node at the tail
    public void insertTail(int data) {
        Node newNode = new Node(data);
        if (tail == null) {
            head = tail = newNode;
        } else {
            tail.next = newNode;
            tail = newNode;
        }
    }

    // Method to delete the head node
    public void deleteHead() {
        if (head == null) {
            return;
        }
        head = head.next;
        if (head == null) {
            tail = null;
        }
    }

    // Method to delete the tail node
    public void deleteTail() {
        if (head == null) {
            return;
        }
        if (head == tail) {
            head = tail = null;
            return;
        }
        Node current = head;
        while (current.next != tail) {
            current = current.next;
        }
        current.next = null;
        tail = current;
    }

    // Method to reverse the linked list
    public void reverse() {
        Node prev = null;
        Node current = head;
        Node next = null;
        tail = head;
        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        head = prev;
    }

    // Method to find the middle element of the linked list
    public Node findMiddle() {
        if (head == null) {
            return null;
        }
        Node slow = head;
        Node fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    // Method to print the linked list
    public void printList() {
        Node currentNode = head;
        while (currentNode != null) {
            System.out.print(currentNode.data + " -> ");
            currentNode = currentNode.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        LinkedList ll = new LinkedList();
        ll.insertHead(1);
        ll.insertTail(2);
        ll.insertTail(3);
        ll.insertTail(4);
        ll.insertTail(5);
        ll.printList(); // Output: 1 -> 2 -> 3 -> 4 -> 5 -> null

        ll.reverse();
        ll.printList(); // Output: 5 -> 4 -> 3 -> 2 -> 1 -> null

        Node middle = ll.findMiddle();
        System.out.println("Middle element: " + (middle != null ? middle.data : "null")); // Output: Middle element: 3

        ll.deleteHead();
        ll.printList(); // Output: 4 -> 3 -> 2 -> 1 -> null

        ll.deleteTail();
        ll.printList(); // Output: 4 -> 3 -> 2 -> null
    }
}
```

This code includes methods to insert and delete nodes at both the head and tail, reverse the linked list, and find the middle element. The `reverse` method reverses the linked list, and the `findMiddle` method uses the two-pointer technique to find the middle element.

Feel free to ask if you have any questions or need further modifications!

## Create Doubly Linked List

Sure! Here's an implementation of a doubly linked list in Java with head and tail pointers, including methods for inserting and deleting nodes at both the head and tail, reversing the list, and finding the middle element:

```java
class Node {
    int data;
    Node next;
    Node prev;

    Node(int data) {
        this.data = data;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
    Node head;
    Node tail;

    // Method to insert a node at the head
    public void insertHead(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = tail = newNode;
        } else {
            newNode.next = head;
            head.prev = newNode;
            head = newNode;
        }
    }

    // Method to insert a node at the tail
    public void insertTail(int data) {
        Node newNode = new Node(data);
        if (tail == null) {
            head = tail = newNode;
        } else {
            tail.next = newNode;
            newNode.prev = tail;
            tail = newNode;
        }
    }

    // Method to delete the head node
    public void deleteHead() {
        if (head == null) {
            return;
        }
        if (head == tail) {
            head = tail = null;
        } else {
            head = head.next;
            head.prev = null;
        }
    }

    // Method to delete the tail node
    public void deleteTail() {
        if (tail == null) {
            return;
        }
        if (head == tail) {
            head = tail = null;
        } else {
            tail = tail.prev;
            tail.next = null;
        }
    }

    // Method to reverse the doubly linked list
    public void reverse() {
        Node current = head;
        Node temp = null;
        while (current != null) {
            temp = current.prev;
            current.prev = current.next;
            current.next = temp;
            current = current.prev;
        }
           }

    // Method to find the middle element of the doubly linked list
    public Node findMiddle() {
        if (head == null) {
            return null;
        }
        Node slow = head;
        Node fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    // Method to print the doubly linked list
    public void printList() {
        Node currentNode = head;
        while (currentNode != null) {
            System.out.print(currentNode.data + " <-> ");
            currentNode = currentNode.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        DoublyLinkedList dll = new DoublyLinkedList();
        dll.insertHead(1);
        dll.insertTail(2);
        dll.insertTail(3);
        dll.insertTail(4);
        dll.insertTail(5);
        dll.printList(); // Output: 1 <-> 2 <-> 3 <-> 4 <-> 5 <-> null

        dll.reverse();
        dll.printList(); // Output: 5 <-> 4 <-> 3 <-> 2 <-> 1 <-> null

        Node middle = dll.findMiddle();
        System.out.println("Middle element: " + (middle != null ? middle.data : "null")); // Output: Middle element: 3

        dll.deleteHead();
        dll.printList(); // Output: 4 <-> 3 <-> 2 <-> 1 <-> null

        dll.deleteTail();
        dll.printList(); // Output: 4 <-> 3 <-> 2 <-> null
    }
}
```

This code defines a `Node` class and a `DoublyLinkedList` class with head and tail pointers. The `DoublyLinkedList` class includes methods to insert and delete nodes at both the head and tail, reverse the list, and find the middle element. The `printList` method prints the elements of the list in both directions.

Feel free to ask if you have any questions or need further modifications!

## Sort List

Sure! Here's a simple example of how you can sort a linked list in Java using the merge sort algorithm. Merge sort is efficient for linked lists because it doesn't require random access to elements.

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class LinkedList {
    Node head;

    // Function to merge two sorted linked lists
    Node sortedMerge(Node a, Node b) {
        if (a == null) return b;
        if (b == null) return a;

        Node result;
        if (a.data <= b.data) {
            result = a;
            result.next = sortedMerge(a.next, b);
        } else {
            result = b;
            result.next = sortedMerge(a, b.next);
        }
        return result;
    }

    // Function to split the linked list into two halves
    Node getMiddle(Node head) {
        if (head == null) return head;

        Node slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    // Function to sort the linked list using merge sort
    Node mergeSort(Node head) {
        if (head == null || head.next == null) return head;

        Node middle = getMiddle(head);
        Node nextOfMiddle = middle.next;
        middle.next = null;

        Node left = mergeSort(head);
        Node right = mergeSort(nextOfMiddle);

        return sortedMerge(left, right);
    }

    // Function to print the linked list
    void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " ");
            head = head.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.head = new Node(4);
        list.head.next = new Node(2);
        list.head.next.next = new Node(1);
        list.head.next.next.next = new Node(3);

        System.out.println("Unsorted Linked List:");
        list.printList(list.head);

        list.head = list.mergeSort(list.head);

        System.out.println("Sorted Linked List:");
        list.printList(list.head);
    }
}
```

This code defines a linked list and sorts it using the merge sort algorithm. You can run this code to see how the linked list is sorted. If you have any questions or need further assistance, feel free to ask!



## Detect cycle in Linked List

To detect a cycle in a linked list, you can use Floyd's Cycle-Finding Algorithm, also known as the Tortoise and Hare algorithm. This algorithm uses two pointers, a slow pointer (tortoise) and a fast pointer (hare). The slow pointer moves one step at a time, while the fast pointer moves two steps at a time. If there is a cycle, the fast pointer will eventually meet the slow pointer.

Here's how you can implement this in Java:

```java
class Node {
    int data;
    Node next;
    Node prev;

    Node(int data) {
        this.data = data;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
    Node head;
    Node tail;

    // Method to insert a node at the head
    public void insertHead(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = tail = newNode;
        } else {
            newNode.next = head;
            head.prev = newNode;
            head = newNode;
        }
    }

    // Method to insert a node at the tail
    public void insertTail(int data) {
        Node newNode = new Node(data);
        if (tail == null) {
            head = tail = newNode;
        } else {
            tail.next = newNode;
            newNode.prev = tail;
            tail = newNode;
        }
    }

    // Method to detect a cycle in the linked list
    public boolean hasCycle() {
        if (head == null) {
            return false;
        }
        Node slow = head;
        Node fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
    }

    // Method to print the doubly linked list
    public void printList() {
        Node currentNode = head;
        while (currentNode != null) {
            System.out.print(currentNode.data + " <-> ");
            currentNode = currentNode.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        DoublyLinkedList dll = new DoublyLinkedList();
        dll.insertHead(1);
        dll.insertTail(2);
        dll.insertTail(3);
        dll.insertTail(4);
        dll.insertTail(5);

        // Creating a cycle for testing
        dll.tail.next = dll.head.next; // 5 -> 2

        System.out.println("Cycle detected: " + dll.hasCycle()); // Output: Cycle detected: true
    }
}
```

This code adds a `hasCycle` method to the `DoublyLinkedList` class, which uses Floyd's Cycle-Finding Algorithm to detect if there is a cycle in the linked list. The `main` method includes a test case where a cycle is manually created to demonstrate the detection.

Feel free to ask if you have any questions or need further modifications!
## Find intersection of Linked List
## Print Even and Odd number in Linked List


## LRU cache

Sure! Here's an implementation of an LRU (Least Recently Used) cache in Java using a combination of a `HashMap` and a doubly linked list:

```java
import java.util.HashMap;

class Node {
    int key;
    int value;
    Node prev;
    Node next;

    Node(int key, int value) {
        this.key = key;
        this.value = value;
        this.prev = null;
        this.next = null;
    }
}

class LRUCache {
    private final int capacity;
    private final HashMap<Integer, Node> map;
    private Node head;
    private Node tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new HashMap<>();
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        if (map.containsKey(key)) {
            Node node = map.get(key);
            remove(node);
            insert(node);
            return node.value;
        }
        return -1; // Return -1 if the key is not found
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) {
            remove(map.get(key));
        }
        if (map.size() == capacity) {
            remove(tail.prev);
        }
        insert(new Node(key, value));
    }

    private void remove(Node node) {
        map.remove(node.key);
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void insert(Node node) {
        map.put(node.key, node);
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }

    public static void main(String[] args) {
        LRUCache cache = new LRUCache(2);
        cache.put(1, 1);
        cache.put(2, 2);
        System.out.println(cache.get(1)); // Output: 1
        cache.put(3, 3); // Evicts key 2
        System.out.println(cache.get(2)); // Output: -1 (not found)
        cache.put(4, 4); // Evicts key 1
        System.out.println(cache.get(1)); // Output: -1 (not found)
        System.out.println(cache.get(3)); // Output: 3
        System.out.println(cache.get(4)); // Output: 4
    }
}
```

This implementation uses a `HashMap` to store the keys and their corresponding nodes, and a doubly linked list to maintain the order of usage. The `get` method retrieves the value of the key if it exists and moves the node to the front of the list. The `put` method inserts a new key-value pair and, if necessary, evicts the least recently used item.

Feel free to ask if you have any questions or need further modifications!

## Postfix expression

Evaluating a postfix expression (Reverse Polish Notation) involves using a stack to process the operands and operators. Let's walk through an example and the corresponding Java code to evaluate a postfix expression.

### Example Postfix Expression:
```
5 1 2 + 4 * + 3 -
```
This expression corresponds to the infix expression: \(5 + ((1 + 2) * 4) - 3\).

### Steps to Evaluate:
1. **Push 5 onto the stack.**
2. **Push 1 onto the stack.**
3. **Push 2 onto the stack.**
4. **Encounter '+':** Pop 2 and 1, compute \(1 + 2 = 3\), push 3 onto the stack.
5. **Push 4 onto the stack.**
6. **Encounter '*':** Pop 4 and 3, compute \(3 * 4 = 12\), push 12 onto the stack.
7. **Encounter '+':** Pop 12 and 5, compute \(5 + 12 = 17\), push 17 onto the stack.
8. **Push 3 onto the stack.**
9. **Encounter '-':** Pop 3 and 17, compute \(17 - 3 = 14\), push 14 onto the stack.

The final result is 14.

### Java Code:

```java
import java.util.Stack;

public class PostfixEvaluator {
    public static void main(String[] args) {
        String postfix = "5 1 2 + 4 * + 3 -"; // Example postfix expression
        int result = evaluatePostfix(postfix);
        System.out.println("The result of the postfix expression is: " + result);
    }

    public static int evaluatePostfix(String expression) {
        Stack<Integer> stack = new Stack<>();
        String[] tokens = expression.split(" ");

        for (String token : tokens) {
            if (isOperator(token)) {
                int operand2 = stack.pop();
                int operand1 = stack.pop();
                int result = performOperation(token, operand1, operand2);
                stack.push(result);
            } else {
                stack.push(Integer.parseInt(token));
            }
        }

        return stack.pop();
    }

    private static boolean isOperator(String token) {
        return token.equals("+") || token.equals("-") || token.equals("*") || token.equals("/");
    }

    private static int performOperation(String operator, int operand1, int operand2) {
        switch (operator) {
            case "+":
                return operand1 + operand2;
            case "-":
                return operand1 - operand2;
            case "*":
                return operand1 * operand2;
            case "/":
                if (operand2 == 0) {
                    throw new IllegalArgumentException("Division by zero");
                }
                return operand1 / operand2;
            default:
                throw new IllegalArgumentException("Invalid operator");
        }
    }
}
```

### Explanation:
1. **Main Method:**
   - Defines an example postfix expression.
   - Calls the `evaluatePostfix` method to evaluate the expression.
   - Prints the result.

2. **evaluatePostfix Method:**
   - **Initialize Stack:** Uses a stack to store operands.
   - **Split Tokens:** Splits the postfix expression into tokens.
   - **Process Tokens:** Iterates through each token:
     - If the token is an operator, pops two operands from the stack, performs the operation, and pushes the result back onto the stack.
     - If the token is an operand, parses it as an integer and pushes it onto the stack.
   - **Return Result:** The final result is the only element left in the stack.

3. **isOperator Method:** Checks if a token is an operator.
4. **performOperation Method:** Performs the specified operation on two operands.

This code efficiently evaluates a postfix expression using a stack. Feel free to test it with different expressions and let me know if you have any questions or need further assistance!

## Prefix Expression

Sure! Let's walk through an example of evaluating a prefix expression in Java. We'll use the prefix expression:

```
- + 5 * 1 2 3
```

This expression corresponds to the infix expression: \((5 + (1 * 2)) - 3\).

### Steps to Evaluate:
1. **Initialize a Stack:** Use a stack to store operands.
2. **Iterate Through Tokens in Reverse:** For each token in the prefix expression (starting from the end):
   - If the token is an operand, push it onto the stack.
   - If the token is an operator, pop the required number of operands from the stack, perform the operation, and push the result back onto the stack.
3. **Final Result:** The final result will be the only element left in the stack.

### Java Code Example:

```java
import java.util.Stack;

public class PrefixEvaluator {
    public static void main(String[] args) {
        String prefix = "- + 5 * 1 2 3"; // Example prefix expression
        int result = evaluatePrefix(prefix);
        System.out.println("The result of the prefix expression is: " + result);
    }

    public static int evaluatePrefix(String expression) {
        Stack<Integer> stack = new Stack<>();
        String[] tokens = expression.split(" ");

        // Process tokens in reverse order
        for (int i = tokens.length - 1; i >= 0; i--) {
            String token = tokens[i];
            if (isOperator(token)) {
                int operand1 = stack.pop();
                int operand2 = stack.pop();
                int result = performOperation(token, operand1, operand2);
                stack.push(result);
            } else {
                stack.push(Integer.parseInt(token));
            }
        }

        return stack.pop();
    }

    private static boolean isOperator(String token) {
        return token.equals("+") || token.equals("-") || token.equals("*") || token.equals("/");
    }

    private static int performOperation(String operator, int operand1, int operand2) {
        switch (operator) {
            case "+":
                return operand1 + operand2;
            case "-":
                return operand1 - operand2;
            case "*":
                return operand1 * operand2;
            case "/":
                if (operand2 == 0) {
                    throw new IllegalArgumentException("Division by zero");
                }
                return operand1 / operand2;
            default:
                throw new IllegalArgumentException("Invalid operator");
        }
    }
}
```

### Explanation:
1. **Main Method:**
   - Defines an example prefix expression.
   - Calls the `evaluatePrefix` method to evaluate the expression.
   - Prints the result.

2. **evaluatePrefix Method:**
   - **Initialize Stack:** Uses a stack to store operands.
   - **Split Tokens:** Splits the prefix expression into tokens.
   - **Process Tokens in Reverse:** Iterates through each token in reverse order:
     - If the token is an operator, pops two operands from the stack, performs the operation, and pushes the result back onto the stack.
     - If the token is an operand, parses it as an integer and pushes it onto the stack.
   - **Return Result:** The final result is the only element left in the stack.

3. **isOperator Method:** Checks if a token is an operator.
4. **performOperation Method:** Performs the specified operation on two operands.

This code efficiently evaluates a prefix expression using a stack. Feel free to test it with different expressions and let me know if you have any questions or need further assistance!

## Valid Parenthesis
Sure! The "Valid Parenthesis" problem typically involves checking if a string containing parentheses is valid. A string is considered valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Here's a simple Java solution using a stack to solve this problem:

```java
import java.util.Stack;

public class ValidParenthesis {
    public static boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;
                char top = stack.pop();
                if ((c == ')' && top != '(') || 
                    (c == '}' && top != '{') || 
                    (c == ']' && top != '[')) {
                    return false;
                }
            }
        }
        
        return stack.isEmpty();
    }

    public static void main(String[] args) {
        String test = "({[]})";
        System.out.println(isValid(test)); // Output: true
    }
}
```

This code defines a method `isValid` that checks if the input string `s` has valid parentheses. It uses a stack to keep track of the opening brackets and ensures they are properly closed in the correct order.

Feel free to ask if you have any questions or need further assistance with this code!
## Min Stack
A Min Stack is a special type of stack that, in addition to the usual stack operations, can also return the minimum element in constant time. Here's how you can implement a Min Stack in Java:

```java
import java.util.Stack;

public class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty() || x <= minStack.peek()) {
            minStack.push(x);
        }
    }

    public void pop() {
        if (stack.isEmpty()) return;
        int popped = stack.pop();
        if (popped == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        if (stack.isEmpty()) throw new RuntimeException("Stack is empty");
        return stack.peek();
    }

    public int getMin() {
        if (minStack.isEmpty()) throw new RuntimeException("Min stack is empty");
       .peek();
    }

    public static void main(String[] args) {
        MinStack minStack = new MinStack();
        minStack.push(3);
        minStack.push(5);
        System.out.println(minStack.getMin()); // Output: 3
        minStack.push(2);
        minStack.push(1);
        System.out.println(minStack.getMin()); // Output: 1
        minStack.pop();
        System.out.println(minStack.getMin()); // Output: 2
        minStack.pop();
        System.out.println(minStack.top());    // Output: 5
    }
}
```

### Explanation:
- **Stack**: The main stack to store all elements.
- **MinStack**: A secondary stack to keep track of the minimum elements.

**Operations**:
- **push(int x)**: Pushes an element onto the main stack and updates the min stack if necessary.
- **pop()**: Removes the top element from the main stack and updates the min stack if the popped element was the minimum.
- **top()**: Returns the top element of the main stack.
- **getMin()**: Returns the minimum element in the stack.

This implementation ensures that all operations (push, pop, top, and getMin) run in constant time, O(1).

Feel free to ask if you have any questions or need further assistance!
## Decode String
The "Decode String" problem typically involves decoding a string that follows a specific encoding rule: `k[encoded_string]`, where the `encoded_string` inside the square brackets is repeated exactly `k` times. Here's a Java solution to decode such a string:

```java
import java.util.Stack;

public class DecodeString {
    public static String decodeString(String s) {
        Stack<Integer> countStack = new Stack<>();
        Stack<String> stringStack = new Stack<>();
        String currentString = "";
        int k = 0;

        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                k = k * 10 + (c - '0');
            } else if (c == '[') {
                countStack.push(k);
                stringStack.push(currentString);
                k = 0;
                currentString = "";
            } else if (c == ']') {
                StringBuilder decodedString = new StringBuilder(stringStack.pop());
                int currentK = countStack.pop();
                for (int i = 0; i < currentK; i++) {
                    decodedString.append(currentString);
                }
                currentString = decodedString.toString();
            } else {
                currentString += c;
            }
        }

        return currentString;
    }

    public static void main(String[] args) {
        String encodedString = "3[a2[c]]";
        System.out.println(decodeString(encodedString)); // Output: accaccacc
    }
}
```

### Explanation:
- **countStack**: Keeps track of the number of times the current string should be repeated.
- **stringStack**: Keeps track of the strings formed so far.
- **currentString**: Holds the current string being processed.
- **k**: Holds the current multiplier value.

**Operations**:
- When encountering a digit, update `k`.
- When encountering `[`, push the current `k` and `currentString` onto their respective stacks and reset them.
- When encountering `]`, pop from both stacks and build the decoded string.
- For other characters, append them to `currentString`.

This solution ensures that the string is decoded correctly by using stacks to manage nested structures.

Feel free to ask if you have any questions or need further assistance!

## Letter Combinations of a Phone Number
Sure! Here's a Java solution to generate all possible letter combinations of a phone number using a recursive approach:

```java
import java.util.ArrayList;
import java.util.List;

public class PhoneNumberCombinations {
    private static final String[] KEYPAD = {
        "",     // 0
        "",     // 1
        "abc",  // 2
        "def",  // 3
        "ghi",  // 4
        "jkl",  // 5
        "mno",  // 6
        "pqrs", // 7
        "tuv",  // 8
        "wxyz"  // 9
    };

    public static List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return result;
        }
        backtrack(result, new StringBuilder(), digits, 0);
        return result;
    }

    private static void backtrack(List<String> result, StringBuilder current, String digits, int index) {
        if (index == digits.length()) {
            result.add(current.toString());
            return;
        KEYPAD[digits.charAt(index) - '0'];
        for (char letter : letters.toCharArray()) {
            current.append(letter);
            backtrack(result, current, digits, index + 1);
            current.deleteCharAt(current.length() - 1);
        }
    }

    public static void main(String[] args) {
        String digits = "23";
        List<String> combinations = letterCombinations(digits);
        System.out.println(combinations);
    }
}
```

This code defines a `PhoneNumberCombinations` class with a method `letterCombinations` that generates all possible letter combinations for a given phone number string. The `backtrack` method is used to explore all possible combinations recursively.

Feel free to ask if you have any questions or need further assistance!

## Generate Parentheses

Sure! Here's a Java solution to generate all combinations of well-formed parentheses using a recursive approach:

```java
import java.util.ArrayList;
import java.util.List;

public class GenerateParentheses {
    public static List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, new StringBuilder(), 0, 0, n);
        return result;
    }

    private static void backtrack(List<String> result, StringBuilder current, int open, int close, int max) {
        if (current.length() == max * 2) {
            result.add(current.toString());
            return;
        }

        if (open < max) {
            current.append('(');
            backtrack(result, current, open + 1, close, max);
            current.deleteCharAt(current.length() - 1);
        }
        if (close < open) {
            current.append(')');
            backtrack(result, current, open, close + 1, max);
            current.deleteCharAt(current.length() - 1);
        }
    }

    public static void main(String[] args) {
        int n = 3;
        List<String> combinations = generateParenthesis(n);
        System.out.println(combinations);
    }
}
```

This code defines a `GenerateParentheses` class with a method `generateParenthesis` that generates all combinations of well-formed parentheses for a given number `n`. The `backtrack` method is used to explore all possible combinations recursively.

If you have any questions or need further assistance, feel free to ask!

##  Permutations

Sure! Here's a Java solution to generate all permutations of a given list of numbers using a recursive approach:

```java
import java.util.ArrayList;
import java.util.List;

public class Permutations {
    public static List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), nums);
        return result;
    }

    private static void backtrack(List<List<Integer>> result, List<Integer> current, int[] nums) {
        if (current.size() == nums.length) {
            result.add(new ArrayList<>(current));
            return;
        }

        for (int num : nums) {
            if (current.contains(num)) continue; // Skip already used numbers
            current.add(num);
            backtrack(result, current, nums);
            current.remove(current.size() - 1);
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        List<List<Integer>> permutations = permute(nums);
        System.out.println(permutations);
    }
}
```

This code defines a `Permutations` class with a method `permute` that generates all permutations of a given array of numbers. The `backtrack` method is used to explore all possible permutations recursively.

If you have any questions or need further assistance, feel free to ask!

## N-Queen 
Sure! Here's a Java solution to solve the N-Queens problem using a backtracking approach:

```java
import java.util.ArrayList;
import java.util.List;

public class NQueens {
    public static List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = '.';
            }
        }
        backtrack(result, board, 0);
        return result;
    }

    private static void backtrack(List<List<String>> result, char[][] board, int row) {
        if (row == board.length) {
            result.add(construct(board));
            return;
        }

        for (int col = 0; col < board.length; col++) {
            if (isValid(board, row, col)) {
                board[row][col] = 'Q';
                backtrack(result, board, row + 1);
                board[row][col] = '.';
            }
        }
    }

    private static boolean isValid(char[][] board, int row, int col) {
        for (int i = 0; i < row; i++) {
            if (board[i][col] == 'Q') {
                return false;
            }
        }
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }
        for (int i = row - 1, j = col + 1; i >= 0 && j < board.length; i--, j++) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }
        return true;
    }

    private static List<String> construct(char[][] board) {
        List<String> path = new ArrayList<>();
        for (int i = 0; i < board.length; i++) {
            path.add(new String(board[i]));
        }
        return path;
    }

    public static void main(String[] args) {
        int n = 4;
        List<List<String>> solutions = solveNQueens(n);
        for (List<String> solution : solutions) {
            for (String row : solution) {
                System.out.println(row);
            }
            System.out.println();
        }
    }
}
```

This code defines an `NQueens` class with a method `solveNQueens` that generates all possible solutions for the N-Queens problem. The `backtrack` method is used to explore all possible placements of queens on the board, ensuring that no two queens threaten each other.

If you have any questions or need further assistance, feel free to ask!

## Combinational Sums
The "Combination Sum" problem involves finding all unique combinations of numbers from a given array that add up to a specific target. Each number in the array can be used multiple times. Here's a Java solution using backtracking to solve this problem:

```java
import java.util.ArrayList;
import java.util.List;

public class CombinationSum {
    public static List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), candidates, target, 0);
        return result;
    }

    private static void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] candidates, int remain, int start) {
        if (remain < 0) return; // if remain is less than 0, no valid combination
        else if (remain == 0) result.add(new ArrayList<>(tempList)); // if remain is 0, we found a valid combination
        else {
            for (int i = start; i < candidates.length; i++) {
                tempList.add(candidates[i]);
                backtrack(result, tempList, candidates, remain - candidates[i], i); // not i + 1 because we can reuse same elements
                tempList.remove(tempList.size() - 1); // remove last element to backtrack
            }
        }
    }

    public static void main(String[] args) {
        int[] candidates = {2, 3, 6, 7};
        int target = 7;
        List<List<Integer>> combinations = combinationSum(candidates, target);
        {
            System.out.println(combination);
        }
    }
}
```

### Explanation:
- **combinationSum**: This method initializes the result list and starts the backtracking process.
- **backtrack**: This helper method performs the backtracking. It explores all possible combinations by adding elements to the temporary list (`tempList`) and recursively calling itself with the updated remaining target (`remain`).

**Steps**:
1. If `remain` is less than 0, it means the current combination is invalid, so return.
2. If `remain` is 0, it means a valid combination is found, so add it to the result list.
3. Otherwise, iterate through the candidates starting from the current index, add the candidate to the temporary list, and recursively call the backtrack method with the updated remaining target.
4. After the recursive call, remove the last element from the temporary list to backtrack and explore other combinations.

This approach ensures that all unique combinations are found and allows the same element to be used multiple times.

Feel free to ask if you have any questions or need further assistance!
## Print all combination of string
To print all combinations of a string in Java, you can use a recursive approach. Here's a simple example to help you get started:

```java
import java.util.ArrayList;
import java.util.List;

public class StringCombinations {
    public static void main(String[] args) {
        String str = "ABC";
        List<String> combinations = new ArrayList<>();
        generateCombinations("", str, combinations);
        for (String combination : combinations) {
            System.out.println(combination);
        }
    }

    private static void generateCombinations(String prefix, String str, List<String> combinations) {
        if (str.length() == 0) {
            combinations.add(prefix);
        } else {
            for (int i = 0; i < str.length(); i++) {
                generateCombinations(prefix + str.charAt(i), str.substring(0, i) + str.substring(i + 1), combinations);
            }
        }
    }
}
```

### Explanation:
- **generateCombinations**: This method generates all possible combinations of the given string.
  - **prefix**: The current combination being built.
  - **str**: The remaining characters to be used.
  - **combinations**: A list to store all the combinations.

**Steps**:
1. If the remaining string (`str`) is empty, add the current combination (`prefix`) to the list of combinations.
2. Otherwise, iterate through each character in the string, add it to the current combination (`prefix`), and recursively call the method with the remaining characters.

This approach ensures that all possible combinations of the string are generated and printed.

Feel free to ask if you have any questions or need further assistance!
## Word Search
The "Word Search" problem involves finding if a given word exists in a grid of letters. The word can be constructed from letters of sequentially adjacent cells, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

Here's a Java solution using backtracking to solve this problem:

```java
public class WordSearch {
    public boolean exist(char[][] board, String word) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[i].length; j++) {
                if (board[i][j] == word.charAt(0) && search(board, word, i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean search(char[][] board, String word, int i, int j, int index) {
        if (index == word.length()) {
            return true;
        }
        if (i < 0 || i >= board.length || j < 0 || j >= board[i].length || board[i][j] != word.charAt(index)) {
            return false;
        }

        char temp = board[i][j];
        board[i][j] = ' '; // mark as visited

        boolean found = search(board, word, i + 1, j, index + 1) ||
                        search(board, word, i - 1, j, index + 1) ||
                        search(board, word, i, j + 1, index + 1) ||
                        search(board, word, i, j - 1, index + 1);

        board[i][j] = temp; // unmark

        return found;
    }

    public static void main(String[] args) {
        WordSearch ws = new WordSearch();
        char[][] board = {
            {'A', 'B', 'C', 'E'},
            {'S', 'F', 'C', 'S'},
            {'A', 'D', 'E', 'E'}
        };
        String word = "ABCCED";
        System.out.println(ws.exist(board, word)); // Output: true
    }
}
```

### Explanation:
- **exist**: This method iterates through each cell in the grid and starts the search if the first character matches.
- **search**: This helper method performs the backtracking search.
  - It checks if the current index matches the length of the word, indicating the word has been found.
  - It ensures the current cell is within bounds and matches the current character of the word.
  - It marks the current cell as visited by temporarily changing its value.
  - It recursively searches in all four possible directions (up, down, left, right).
  - It unmarks the cell after the search.

This approach ensures that all possible paths are explored to find the word in the grid.

Feel free to ask if you have any questions or need further assistance!
## Palindrome Partitioning
Palindrome Partitioning involves splitting a string into all possible palindromic substrings. Here's a Java solution using backtracking to find all possible palindrome partitions of a given string:

```java
import java.util.ArrayList;
import java.util.List;

public class PalindromePartitioning {
    public static List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), s, 0);
        return result;
    }

    private static void backtrack(List<List<String>> result, List<String> tempList, String s, int start) {
        if (start == s.length()) {
            result.add(new ArrayList<>(tempList));
        } else {
            for (int i = start; i < s.length(); i++) {
                if (isPalindrome(s, start, i)) {
                    tempList.add(s.substring(start, i + 1));
                    backtrack(result, tempList, s, i + 1);
                    tempList.remove(tempList.size() - 1);
                }
            }
        }
    }

    private static boolean isPalindrome(String s, int low, int high) {
        while (low < high) {
            if (s.charAt(low++) != s.charAt(high--)) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        String s = "aab";
        List<List<String>> partitions = partition(s);
        for (List<String> partition : partitions) {
            System.out.println(partition);
        }
    }
}
```

### Explanation:
- **partition**: This method initializes the result list and starts the backtracking process.
- **backtrack**: This helper method performs the backtracking. It explores all possible partitions by adding palindromic substrings to the temporary list (`tempList`) and recursively calling itself with the updated start index.
- **isPalindrome**: This helper method checks if a substring is a palindrome.

**Steps**:
1. If the start index equals the length of the string, add the current partition (`tempList`) to the result list.
2. Otherwise, iterate through the string, checking for palindromic substrings.
3. If a palindromic substring is found, add it to the temporary list and recursively call the backtrack method with the updated start index.
4. After the recursive call, remove the last element from the temporary list to backtrack and explore other partitions.

This approach ensures that all possible palindromic partitions of the string are found.

Feel free to ask if you have any questions or need further assistance!
## Generate Parenthesis

Generating all combinations of well-formed parentheses is a common problem that can be solved using backtracking. Here's a Java solution to generate all valid combinations of `n` pairs of parentheses:

```java
import java.util.ArrayList;
import java.util.List;

public class GenerateParenthesis {
    public static List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, "", 0, 0, n);
        return result;
    }

    private static void backtrack(List<String> result, String current, int open, int close, int max) {
        if (current.length() == max * 2) {
            result.add(current);
            return;
        }

        if (open < max) {
            backtrack(result, current + "(", open + 1, close, max);
        }
 for (String combination : combinations) {
            System.out.println(combination);
        }
    }
}
```

### Explanation:
- **generateParenthesis**: This method initializes the result list and starts the backtracking process.
- **backtrack**: This helper method performs the backtracking. It builds the current string (`current`) by adding open and close parentheses while ensuring the parentheses are well-formed.
  - If the length of the current string equals `max * 2`, it means a valid combination is found, so add it to the result list.
  - If the number of open parentheses is less than `max`, add an open parenthesis and recursively call the backtrack method.
  - If the number of close parentheses is less than the number of open parentheses, add a close parenthesis and recursively call the backtrack method.

This approach ensures that all valid combinations of `n` pairs of parentheses are generated.

Feel free to ask if you have any questions or need further assistance!

## Implement Stack Using Queue
Implementing a stack using queues can be done in a couple of ways, but one common approach is to use two queues. Here's a Java implementation of a stack using two queues:

```java
import java.util.LinkedList;
import java.util.Queue;

public class StackUsingQueues {
    private Queue<Integer> queue1;
    private Queue<Integer> queue2;

    public StackUsingQueues() {
        queue1 = new LinkedList<>();
        queue2 = new LinkedList<>();
    }

    public void push(int x) {
        queue2.add(x);
        while (!queue1.isEmpty()) {
            queue2.add(queue1.remove());
        }
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;
    }

    public int pop() {
        if (queue1.isEmpty()) {
            throw new RuntimeException("Stack is empty");
        }
        return queue1.remove();
    }

    public int top() {
        if (queue1.isEmpty()) {
            throw new RuntimeException("Stack is empty");
        }
        return queue1.peek();
    }

    public boolean isEmpty() {
        return queue1.isEmpty();
    }

    public static void main(String[] args) {
        StackUsingQueues stack = new StackUsingQueues();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        System.out.println(stack.top()); // Output: 3
        System.out.println(stack.pop()); // Output: 3
        System.out.println(stack.top()); // Output: 2
        System.out.println(stack.isEmpty()); // Output: false
    }
}
```

### Explanation:
- **push(int x)**: Adds an element to the stack. It first adds the element to `queue2`, then moves all elements from `queue1` to `queue2`, and finally swaps the references of `queue1` and `queue2`.
- **pop()**: Removes the top element from the stack, which is the front element of `queue1`.
- **top()**: Returns the top element of the stack, which is the front element of `queue1`.
- **isEmpty()**: Checks if the stack is empty by checking if `queue1` is empty.

This approach ensures that the stack operations are implemented using the queue operations, maintaining the LIFO (Last In, First Out) property of the stack.

Feel free to ask if you have any questions or need further assistance!
## Implement Queue Using Stack
Implementing a queue using stacks can be done using two stacks. Here's a Java implementation of a queue using two stacks:

```java
import java.util.Stack;

public class QueueUsingStacks {
    private Stack<Integer> stack1;
    private Stack<Integer> stack2;

    public QueueUsingStacks() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }

    public void enqueue(int x) {
        stack1.push(x);
    }

    public int dequeue() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        if (stack2.isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        return stack2.pop();
    }

    public int peek() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        if (stack2.isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }

    public boolean isEmpty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }

    public static void main(String[] args) {
        QueueUsingStacks queue = new QueueUsingStacks();
        queue.enqueue(1);
        queue.enqueue(2);
        queue.enqueue(3);
        System.out.println(queue.dequeue()); // Output: 1
        System.out.println(queue.peek());    // Output: 2
        System.out.println(queue.dequeue()); // Output: 2
        System.out.println(queue.isEmpty()); // Output: false
    }
}
```

### Explanation:
- **enqueue(int x)**: Adds an element to the queue by pushing it onto `stack1`.
- **dequeue()**: Removes the front element from the queue. If `stack2` is empty, it moves all elements from `stack1` to `stack2` and then pops the top element from `stack2`.
- **peek()**: Returns the front element of the queue without removing it. If `stack2` is empty, it moves all elements from `stack1` to `stack2` and then returns the top element from `stack2`.
- **isEmpty()**: Checks if the queue is empty by checking if both `stack1` and `stack2` are empty.

This approach ensures that the queue operations are implemented using the stack operations, maintaining the FIFO (First In, First Out) property of the queue.

Feel free to ask if you have any questions or need further assistance!
## Implement HashMap
Implementing a basic HashMap in Java involves creating a data structure that uses an array of linked lists (or buckets) to handle collisions. Here's a simple implementation:

```java
import java.util.LinkedList;

class HashMap<K, V> {
    private class Entry<K, V> {
        K key;
        V value;
        Entry<K, V> next;

        Entry(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }

    private final int SIZE = 16;
    private LinkedList<Entry<K, V>>[] table;

    public HashMap() {
        table = new LinkedList[SIZE];
        for (int i = 0; i < SIZE; i++) {
            table[i] = new LinkedList<>();
        }
    }

    private int hash(K key) {
        return Math.abs(key.hashCode() % SIZE);
    }

    public void put(K key, V value) {
        int hash = hash(key);
        for (Entry<K, V> entry : table[hash]) {
            if (entry.key.equals(key)) {
                entry.value = value;
                return;
            }
        }
        table[hash].add(new Entry<>(key, value));
    }

    public V get(K key) {
        int hash = hash(key);
        for (Entry<K, V> entry : table[hash]) {
            if (entry.key.equals(key)) {
                return entry.value;
            }
        }
        return null;
    }

    public void remove(K key) {
        int hash = hash(key);
        Entry<K, V> toRemove = null;
        for (Entry<K, V> entry : table[hash]) {
            if (entry.key.equals(key)) {
                toRemove = entry;
                break;
            }
        }
        if (toRemove != null) {
            table[hash].remove(toRemove);
        }
    }

    public boolean containsKey(K key) {
        int hash = hash(key);
        for (Entry<K, V> entry : table[hash]) {
            if (entry.key.equals(key)) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("one", 1);
        map.put("two", 2);
        map.put("three", 3);

        System.out.println(map.get("one"));   // Output: 1
        System.out.println(map.get("four"));  // Output: null
        System.out.println(map.containsKey("two")); // Output: true

        map.remove("two");
        System.out.println(map.containsKey("two")); // Output: false
    }
}
```

### Explanation:
- **Entry<K, V>**: A nested class representing a key-value pair.
- **SIZE**: The size of the hash table (number of buckets).
- **table**: An array of linked lists to handle collisions.
- **hash(K key)**: A method to compute the hash code for a given key.
- **put(K key, V value)**: Adds a key-value pair to the hash map. If the key already exists, it updates the value.
- **get(K key)**: Retrieves the value associated with the given key.
- **remove(K key)**: Removes the key-value pair from the hash map.
- **containsKey(K key)**: Checks if the hash map contains the given key.

This implementation provides a basic understanding of how a hash map works internally. Feel free to ask if you have any questions or need further assistance!
## Implement All One 
The "All One" data structure is a complex problem that involves designing a data structure to support the following operations in O(1) time:

1. **inc(key)**: Increments the count of the key. If the key does not exist, add it with a count of 1.
2. **dec(key)**: Decrements the count of the key. If the key's count is 1, remove it from the data structure.
3. **getMaxKey()**: Returns one of the keys with the highest count.
4. **getMinKey()**: Returns one of the keys with the lowest count.

Here's a Java implementation using a combination of a HashMap and a doubly linked list:

```java
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedHashSet;

public class AllOne {
    private class Node {
        int count;
        LinkedHashSet<String> keys;
        Node prev, next;

        Node(int count) {
            this.count = count;
            keys = new LinkedHashSet<>();
        }
    }

    private HashMap<String, Node> keyNodeMap;
    private Node head, tail;

    public AllOne() {
        keyNodeMap = new HashMap<>();
        head = new Node(Integer.MIN_VALUE);
        tail = new Node(Integer.MAX_VALUE);
        head.next = tail;
        tail.prev = head;
    }

    public void inc(String key) {
        if (keyNodeMap.containsKey(key)) {
            Node node = keyNodeMap.get(key);
            node.keys.remove(key);
            if (node.next.count == node.count + 1) {
                node.next.keys.add(key);
                keyNodeMap.put(key, node.next);
            } else {
                Node newNode = new Node(node.count + 1);
                newNode.keys.add(key);
                insertAfter(node, newNode);
                keyNodeMap.put(key, newNode);
            }
            if (node.keys.isEmpty()) remove(node);
        } else {
            if (head.next.count == 1) {
                head.next.keys.add(key);
                keyNodeMap.put(key, head.next);
            } else {
                Node newNode = new Node(1);
                newNode.keys.add(key);
                insertAfter(head, newNode);
                keyNodeMap.put(key, newNode);
            }
        }
    }

    public void dec(String key) {
        if (!keyNodeMap.containsKey(key)) return;
        Node node = keyNodeMap.get(key);
        node.keys.remove(key);
        if (node.count == 1) {
            keyNodeMap.remove(key);
        } else {
            if (node.prev.count == node.count - 1) {
                node.prev.keys.add(key);
                keyNodeMap.put(key, node.prev);
            } else {
                Node newNode = new Node(node.count - 1);
                newNode.keys.add(key);
                insertAfter(node.prev, newNode);
                keyNodeMap.put(key, newNode);
            }
        }
        if (node.keys.isEmpty()) remove(node);
    }

    public String getMaxKey() {
        return tail.prev == head ? "" : tail.prev.keys.iterator().next();
    }

    public String getMinKey() {
        return head.next == tail ? "" : head.next.keys.iterator().next();
    }

    private void insertAfter(Node node, Node newNode) {
        newNode.prev = node;
        newNode.next = node.next;
        node.next.prev = newNode;
        node.next = newNode;
    }

    private void remove(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    public static void main(String[] args) {
        AllOne allOne = new AllOne();
        allOne.inc("hello");
        allOne.inc("world");
        allOne.inc("hello");
        System.out.println(allOne.getMaxKey()); // Output: "hello"
        System.out.println(allOne.getMinKey()); // Output: "world"
        allOne.dec("hello");
        System.out.println(allOne.getMaxKey()); // Output: "hello"
        System.out.println(allOne.getMinKey()); // Output: "hello"
    }
}
```

### Explanation:
- **Node**: A class representing a node in the doubly linked list, containing a count and a set of keys with that count.
- **keyNodeMap**: A HashMap mapping keys to their corresponding nodes.
- **head, tail**: Dummy nodes representing the start and end of the doubly linked list.

**Operations**:
- **inc(String key)**: Increments the count of the key, updating the linked list and HashMap accordingly.
- **dec(String key)**: Decrements the count of the key, updating the linked list and HashMap accordingly.
- **getMaxKey()**: Returns one of the keys with the highest count.
- **getMinKey()**: Returns one of the keys with the lowest count.
- **insertAfter(Node node, Node newNode)**: Inserts a new node after a given node in the linked list.
- **remove(Node node)**: Removes a node from the linked list.

This implementation ensures that all operations run in O(1) time.

Feel free to ask if you have any questions or need further assistance!
## Implement tries
A Trie (pronounced "try") is a tree-like data structure used to efficiently store and retrieve keys in a dataset of strings. Here's a basic implementation of a Trie in Java:

```java
import java.util.HashMap;
import java.util.Map;

class TrieNode {
    Map<Character, TrieNode> children;
    boolean isEndOfWord;

    public TrieNode() {
        children = new HashMap<>();
        isEndOfWord = false;
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Insert a word into the trie
    public void insert(String word) {
        TrieNode current = root;
        for (char c : word.toCharArray()) {
            current = current.children.computeIfAbsent(c, k -> new TrieNode());
        }
        current.isEndOfWord = true;
    }

    // Search for a word in the trie
    public boolean search(String word) {
        TrieNode current = root;
        for (char c : word.toCharArray()) {
            current = current.children.get(c);
            if (current == null) {
                return false;
            }
        }
        return current.isEndOfWord;
    }

    // Check if there is any word in the trie that starts with the given prefix
    public boolean startsWith(String prefix) {
        TrieNode current = root;
        for (char c : prefix.toCharArray()) {
            current = current.children.get(c);
            if (current == null) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        Trie trie = new Trie();
        trie.insert("apple");
        System.out.println(trie.search("apple"));   // Output: true
        System.out.println(trie.search("app"));     // Output: false
        System.out.println(trie.startsWith("app")); // Output: true
        trie.insert("app");
        System.out.println(trie.search("app"));     // Output: true
    }
}
```

### Explanation:
- **TrieNode**: A class representing a node in the Trie. Each node contains a map of its children and a boolean flag indicating if it is the end of a word.
- **Trie**: The main class containing the root node and methods to insert, search, and check prefixes.

**Operations**:
- **insert(String word)**: Inserts a word into the Trie by iterating through its characters and creating new nodes as needed.
- **search(String word)**: Searches for a word in the Trie by traversing through its characters. Returns `true` if the word is found and is marked as the end of a word.
- **startsWith(String prefix)**: Checks if there is any word in the Trie that starts with the given prefix by traversing through its characters.

This implementation provides a basic understanding of how a Trie works and how it can be used to store and retrieve strings efficiently.

Feel free to ask if you have any questions or need further assistance!
## Implement min Heap
A Min Heap is a binary tree where the parent node is always less than or equal to its child nodes. Here's a basic implementation of a Min Heap in Java using an array:

```java
public class MinHeap {
    private int[] heap;
    private int size;
    private int capacity;

    public MinHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.heap = new int[capacity + 1];
        this.heap[0] = Integer.MIN_VALUE; // Sentinel value for easier comparisons
    }

    private int parent(int pos) {
        return pos / 2;
    }

    private int leftChild(int pos) {
        return 2 * pos;
    }

    private int rightChild(int pos) {
        return 2 * pos + 1;
    }

    private boolean isLeaf(int pos) {
        return pos > size / 2 && pos <= size;
    }

    private void swap(int fpos, int spos) {
        int tmp = heap[fpos];
        heap[fpos] = heap[spos];
        heap[spos] = tmp;
    }

    private void heapifyDown(int pos) {
        if (!isLeaf(pos)) {
            int left = leftChild(pos);
            int right = rightChild(pos);
            int smallest = pos;

            if (left <= size && heap[left] < heap[smallest]) {
                smallest = left;
            }
            if (right <= size && heap[right] < heap[smallest]) {
                smallest = right;
            }
            if (smallest != pos) {
                swap(pos, smallest);
                heapifyDown(smallest);
            }
        }
    }

    private void heapifyUp(int pos) {
        while (heap[current] < heap[parent(current)]) {
            swap(current, parent(current));
            current = parent(current);
        }
    }

    public void insert(int element) {
        if (size >= capacity) {
            throw new RuntimeException("Heap is full");
        }
        heap[++size] = element;
        heapifyUp(size);
    }

    public int remove() {
        if (size == 0) {
            throw new RuntimeException("Heap is empty");
        }
        int popped = heap[1];
        heap[1] = heap[size--];
        heapifyDown(1);
        return popped;
    }

    public int getMin() {
        if (size == 0) {
            throw new RuntimeException("Heap is empty");
        }
        return heap[1];
    }

    public static void main(String[] args) {
        MinHeap minHeap = new MinHeap(10);
        minHeap.insert(3);
        minHeap.insert(2);
        minHeap.insert(15);
        minHeap.insert(5);
        minHeap.insert(4);
        minHeap.insert(45);

        System.out.println("Min value: " + minHeap.getMin()); // Output: 2
        System.out.println("Removed value: " + minHeap.remove()); // Output: 2
        System.out.println("Min value: " + minHeap.getMin()); // Output: 3
    }
}
```

### Explanation:
- **MinHeap(int capacity)**: Constructor to initialize the heap with a given capacity.
- **parent(int pos)**, **leftChild(int pos)**, **rightChild(int pos)**: Helper methods to get the parent, left child, and right child positions.
- **isLeaf(int pos)**: Checks if a node is a leaf node.
- **swap(int fpos, int spos)**: Swaps two elements in the heap.
- **heapifyDown(int pos)**: Ensures the heap property is maintained from the given position downwards.
- **heapifyUp(int pos)**: Ensures the heap property is maintained from the given position upwards.
- **insert(int element)**: Inserts a new element into the heap and maintains the heap property.
- **remove()**: Removes and returns the minimum element from the heap and maintains the heap property.
- **getMin()**: Returns the minimum element from the heap without removing it.

This implementation provides a basic understanding of how a Min Heap works and how to perform common operations on it.

Feel free to ask if you have any questions or need further assistance!

## Graph DFS traversal
Depth-First Search (DFS) is a graph traversal algorithm that explores as far as possible along each branch before backtracking. Here's a Java implementation of DFS for a graph represented using an adjacency list:

```java
import java.util.*;

public class Graph {
    private int vertices; // Number of vertices
    private LinkedList<Integer>[] adjList; // Adjacency list

    // Constructor
    public Graph(int vertices) {
        this.vertices = vertices;
        adjList = new LinkedList[vertices];
        for (int i = 0; i < vertices; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    // Add an edge to the graph
    public void addEdge(int v, int w) {
        adjList[v].add(w); // Add w to v's list
    }

    // DFS traversal from a given source vertex
    public void DFS(int v) {
        boolean[] visited = new boolean[vertices];
        DFSUtil(v, visited);
    }

    // Utility function for DFS
    private void DFSUtil(int v, boolean[] visited) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int n : adjList[v]) {
            if (!visited[n]) {
                DFSUtil(n, visited);
            }
        }
    }

    public static void main(String[] args) {
        Graph g = new Graph(4);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 0);
       2); // Output: 2 0 1 3
    }
}
```

### Explanation:
- **Graph(int vertices)**: Constructor to initialize the graph with a given number of vertices.
- **addEdge(int v, int w)**: Adds an edge from vertex `v` to vertex `w`.
- **DFS(int v)**: Initiates the DFS traversal from the given source vertex `v`.
- **DFSUtil(int v, boolean[] visited)**: A utility function that performs the DFS traversal. It marks the current node as visited, prints it, and recursively visits all its adjacent vertices that haven't been visited yet.

This implementation provides a basic understanding of how DFS works and how to perform it on a graph represented using an adjacency list.

Feel free to ask if you have any questions or need further assistance!
## Graph BFS traversal
Breadth-First Search (BFS) is a graph traversal algorithm that explores all the vertices at the present depth level before moving on to the vertices at the next depth level. Here's a Java implementation of BFS for a graph represented using an adjacency list:

```java
import java.util.*;

public class Graph {
    private int vertices; // Number of vertices
    private LinkedList<Integer>[] adjList; // Adjacency list

    // Constructor
    public Graph(int vertices) {
        this.vertices = vertices;
        adjList = new LinkedList[vertices];
        for (int i = 0; i < vertices; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    // Add an edge to the graph
    public void addEdge(int v, int w) {
        adjList[v].add(w); // Add w to v's list
    }

    // BFS traversal from a given source vertex
    public void BFS(int s) {
        boolean[] visited = new boolean[vertices];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (!queue.isEmpty()) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int n : adjList[s]) {
                if (!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    }

    public static void main(String[] args) {
        Graph g = new Graph(4);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 0);
        g.addEdge(2, 3);
        g.addEdge(3, 3);

        System.out.println("Breadth First Traversal starting from vertex 2:");
        g.BFS(2); // Output: 2 0 3 1
    }
}
```

### Explanation:
- **Graph(int vertices)**: Constructor to initialize the graph with a given number of vertices.
- **addEdge(int v, int w)**: Adds an edge from vertex `v` to vertex `w`.
- **BFS(int s)**: Initiates the BFS traversal from the given source vertex `s`.
  - It uses a boolean array `visited` to keep track of visited vertices.
  - A queue is used to manage the order of traversal.
  - The source vertex is marked as visited and enqueued.
  - While the queue is not empty, the vertex at the front of the queue is dequeued, printed, and all its adjacent vertices that haven't been visited are marked as visited and enqueued.

This implementation provides a basic understanding of how BFS works and how to perform it on a graph represented using an adjacency list.

Feel free to ask if you have any questions or need further assistance!
## Clone Graph
Cloning a graph involves creating a deep copy of the graph, where each node and its connections are duplicated. Here's a Java implementation to clone an undirected graph using Depth-First Search (DFS):

```java
import java.util.*;

class Node {
    public int val;
    public List<Node> neighbors;

    public Node() {
        val = 0;
        neighbors = new ArrayList<>();
    }

    public Node(int val) {
        this.val = val;
        neighbors = new ArrayList<>();
    }

    public Node(int val, ArrayList<Node> neighbors) {
        this.val = val;
        this.neighbors = neighbors;
    }
}

public class CloneGraph {
    private Map<Node, Node> visited = new HashMap<>();

    public Node cloneGraph(Node node) {
        if (node == null) {
            return null;
        }

        if (visited.containsKey(node)) {
            return visited.get(node);
        }

        Node cloneNode = new Node(node.val, new ArrayList<>());
        visited.put(node, cloneNode);

        for (Node neighbor : node.neighbors) {
            cloneNode.neighbors.add(cloneGraph(neighbor));
        }

        return cloneNode;
    }

    public static void main(String[] args) {
        // Example usage:
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(4);

        node1.neighbors.add(node2);
        node1.neighbors.add(node4);
        node2.neighbors.add(node1);
        node2.neighbors.add(node3);
        node3.neighbors.add(node2);
        node3.neighbors.add(node4);
        node4.neighbors.add(node1);
        node4.neighbors.add(node3);

        CloneGraph cg = new CloneGraph();
        Node clonedGraph = cg.cloneGraph(node1);

        // Output the cloned graph (for demonstration purposes)
        System.out.println("Cloned Node 1 neighbors: " + clonedGraph.neighbors.size()); // Should output 2
    }
}
```

### Explanation:
- **Node**: A class representing a node in the graph, containing a value and a list of neighbors.
- **cloneGraph(Node node)**: The main method to clone the graph. It uses a HashMap to keep track of visited nodes and their clones.
  - If the node is `null`, it returns `null`.
  - If the node has already been visited, it returns the cloned node from the map.
  - Otherwise, it creates a new node, adds it to the map, and recursively clones all its neighbors.

This implementation ensures that each node and its connections are duplicated, creating a deep copy of the graph.

Feel free to ask if you have any questions or need further assistance!
## Number of Island

The "Number of Islands" problem involves finding the number of islands in a given 2D grid. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. Here's a Java solution using Depth-First Search (DFS) to solve this problem:

```java
public class NumberOfIslands {
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }

        int numIslands = 0;
        int rows = grid.length;
        int cols = grid[0].length;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == '1') {
                    numIslands += dfs(grid, i, j);
                }
            }
        }

        return numIslands;
    }

    private int dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == '0') {
            return 0;
        }

        grid[i][j] = '0'; // Mark the cell as visited

        // Explore all four directions
        dfs(grid, i + 1, j);
        dfs(grid, i - 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i, j - 1);

        return 1;
    }

    public static void main(String[] args) {
        NumberOfIslands solution = new NumberOfIslands();
        char[][] grid = {
            {'1', '1', '0', '0', '0'},
            {'1', '1', '0', '0', '0'},
            {'0', '0', '1', '0', '0'},
            {'0', '0', '0', '1', '1'}
        };
        System.out.println("Number of islands: " + solution.numIslands(grid)); // Output: 3
    }
}
```

### Explanation:
- **numIslands(char[][] grid)**: This method iterates through each cell in the grid. When it finds a '1' (land), it starts a DFS to mark all connected lands and increments the island count.
- **dfs(char[][] grid, int i, int j)**: This helper method performs the DFS. It marks the current cell as visited by setting it to '0' and recursively explores all four possible directions (up, down, left, right).

This approach ensures that all connected lands are marked as visited, and the number of islands is correctly counted.

Feel free to ask if you have any questions or need further assistance!

## Counting Sort 

Counting Sort is a non-comparative sorting algorithm that sorts integers by counting the occurrences of each unique value. It works efficiently when the range of input values is not significantly larger than the number of elements to be sorted.

### Steps for Counting Sort:
1. **Find the Range:** Determine the range of the input values.
2. **Count Occurrences:** Create a count array to store the count of each unique value.
3. **Accumulate Counts:** Modify the count array such that each element at each index stores the sum of previous counts.
4. **Place Elements:** Build the output array by placing elements at their correct positions.

### Code Example:

```java
import java.util.Arrays;

public class CountingSort {
    public static void main(String[] args) {
        int[] arr = {4, 2, 2, 8, 3, 3, 1};
        countingSort(arr);
        System.out.println("Sorted array: " + Arrays.toString(arr));
    }

    public static void countingSort(int[] arr) {
        int max = Arrays.stream(arr).max().getAsInt();
        int min = Arrays.stream(arr).min().getAsInt();
        int range = max - min + 1;

        int[] count = new int[range];
        int[] output = new int[arr.length];

        // Count occurrences of each value
        for (int i : arr) {
            count[i - min]++;
        }

        // Accumulate counts
        for (int i = 1; i < count.length; i++) {
            count[i] += count[i - 1];
        }

        // Place elements in the output array
        for (int i = arr.length - 1; i >= 0; i--) {
            output[count[arr[i] - min] - 1] = arr[i];
            count[arr[i] - min]--;
        }

        // Copy the sorted elements back to the original array
        System.arraycopy(output, 0, arr, 0, arr.length);
    }
}
```

### Explanation:
1. **Main Method:** Initializes an array and calls the `countingSort` method.
2. **countingSort Method:**
   - **Find Range:** Determines the minimum and maximum values in the array to calculate the range.
   - **Count Array:** Initializes a count array to store the frequency of each value.
   - **Count Occurrences:** Iterates through the input array to count the occurrences of each value.
   - **Accumulate Counts:** Modifies the count array to store the cumulative count of elements.
   - **Place Elements:** Places each element in its correct position in the output array based on the cumulative counts.
   - **Copy Back:** Copies the sorted elements from the output array back to the original array.

This implementation ensures that the array is sorted in linear time, making Counting Sort efficient for specific types of input.

Feel free to test this code and let me know if you have any questions or need further assistance!

## Merge Sorting

Merge Sort is a classic divide-and-conquer algorithm that divides the input array into two halves, recursively sorts them, and then merges the sorted halves. Here's a Java implementation of Merge Sort:

```java
public class MergeSort {
    public static void mergeSort(int[] array) {
        if (array.length < 2) {
            return;
        }
        int mid = array.length / 2;
        int[] left = new int[mid];
        int[] right = new int[array.length - mid];

        System.arraycopy(array, 0, left, 0, mid);
        System.arraycopy(array, mid, right, 0, array.length - mid);

        mergeSort(left);
        mergeSort(right);

        merge(array, left, right);
    }

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
        int[] array = {12, 11, 13, 5, 6, 7};
        System.out.println("Given Array:");
        for (int num : array) {
            System.out.print(num + " ");
        }
        System.out.println();

        mergeSort(array);

        System.out.println("Sorted Array:");
        array) {
            System.out.print(num + " ");
        }
    }
}
```

### Explanation:
- **mergeSort(int[] array)**: This method recursively divides the array into two halves until the base case (array length < 2) is reached. It then calls the `merge` method to combine the sorted halves.
- **merge(int[] array, int[] left, int[] right)**: This helper method merges two sorted arrays (`left` and `right`) into the original array. It uses three pointers to track the current index of the `left`, `right`, and merged arrays.

**Steps**:
1. **Divide**: Split the array into two halves.
2. **Conquer**: Recursively sort each half.
3. **Combine**: Merge the sorted halves to produce the sorted array.

This implementation ensures that the array is sorted in O(n log n) time complexity.

Feel free to ask if you have any questions or need further assistance!


## Partition Sort / Quick Sort
Quick Sort is an efficient, in-place sorting algorithm that uses the divide-and-conquer strategy. Here's a Java implementation of Quick Sort:

```java
public class QuickSort {
    public static void quickSort(int[] array, int low, int high) {
        if (low < high) {
            int pi = partition(array, low, high);
            quickSort(array, low, pi - 1);
            quickSort(array, pi + 1, high);
        }
    }

    private static int partition(int[] array, int low, int high) {
        int pivot = array[high];
        int i = (low - 1);
        for (int j = low; j < high; j++) {
            if (array[j] <= pivot) {
                i++;
                int temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }
        }
        int temp = array[i + 1];
        array[i + 1] = array[high];
        array[high] = temp;
        return i + 1;
    }

    public static void main(String[] args) {
        int[] array = {10, 7, 8, 9, 1, 5};
        int n = array.length;
        System.out.println("Given Array:");
        for (int num : array) {
            System.out.print(num + " ");
        }
        System.out.println();

        quickSort(array, 0, n - 1);

        System.out.println("Sorted Array:");
        for (int num : array) {
            System.out.print(num + " ");
        }
    }
}
```

### Explanation:
- **quickSort(int[] array, int low, int high)**: This method recursively sorts the array. It calls the `partition` method to find the pivot element and then recursively sorts the subarrays before and after the pivot.
- **partition(int[] array, int low, int high)**: This helper method partitions the array around the pivot element. It places the pivot element in its correct position and ensures that all elements less than the pivot are on its left, and all elements greater than the pivot are on its right.

**Steps**:
1. **Choose a Pivot**: Select an element as the pivot (commonly the last element).
2. **Partition**: Rearrange the array so that elements less than the pivot are on the left, and elements greater than the pivot are on the right.
3. **Recursively Sort**: Apply the same process to the subarrays on the left and right of the pivot.

This implementation ensures that the array is sorted in O(n log n) time complexity on average.

Feel free to ask if you have any questions or need further assistance!
## Bubble Sort
Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. Here's a Java implementation of Bubble Sort:

```java
public class BubbleSort {
    public static void bubbleSort(int[] array) {
        int n = array.length;
        boolean swapped;
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 0; j < n - 1 - i; j++) {
                if (array[j] > array[j + 1]) {
                    // Swap array[j] and array[j + 1]
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                    swapped = true;
                }
            }
            // If no two elements were swapped in the inner loop, then the array is already sorted
            if (!swapped) break;
        }
    }

    public static void main(String[] args) {
        int[] array = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Given Array:");
        for (int num : array) {
            System.out.print(num + " ");
        }
        System.out.println();

        bubbleSort(array);

        System.out.println("Sorted Array:");
        for (int num : array) {
            System.out.print(num + " ");
        }
    }
}
```

### Explanation:
- **bubbleSort(int[] array)**: This method sorts the array using the Bubble Sort algorithm.
  - It iterates through the array multiple times.
  - In each iteration, it compares adjacent elements and swaps them if they are in the wrong order.
  - The process is repeated until no more swaps are needed, indicating that the array is sorted.

**Steps**:
1. **Outer Loop**: Runs from the start to the second-to-last element.
2. **Inner Loop**: Compares each pair of adjacent elements and swaps them if necessary.
3. **Swapped Flag**: If no elements were swapped during an iteration, the array is already sorted, and the algorithm can terminate early.

This implementation ensures that the array is sorted in O(n^2) time complexity in the worst case.

Feel free to ask if you have any questions or need further assistance!


## Merge Interval
Merging intervals involves combining overlapping intervals into a single interval. Here's a Java implementation to merge overlapping intervals:

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class MergeIntervals {
    public static int[][] merge(int[][] intervals) {
        if (intervals.length <= 1) {
            return intervals;
        }

        // Sort intervals by starting time
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        List<int[]> merged = new ArrayList<>();
        int[] currentInterval = intervals[0];
        merged.add(currentInterval);

        for (int[] interval : intervals) {
            int currentEnd = currentInterval[1];
            int nextStart = interval[0];
            int nextEnd = interval[1];

            if (currentEnd >= nextStart) { // Overlapping intervals, merge them
                currentInterval[1] = Math.max(currentEnd, nextEnd);
            } else { // Non-overlapping interval, add to the list
                currentInterval = interval;
                merged.add(currentInterval);
            }
        }

        return merged.toArray(new int[merged.size()][]);
    }

    public static void main(String[] args) {
        int[][] intervals = {{1, 3}, {2, 6}, {8, 10}, {15, 18}};
        int[][] mergedIntervals = merge(intervals);

        System.out.println("Merged Intervals:");
        for (int[] interval : mergedIntervals) {
            System.out.println(Arrays.toString(interval));
        }
    }
}
```

### Explanation:
- **merge(int[][] intervals)**: This method merges overlapping intervals.
  - It first sorts the intervals based on their starting times.
  - It then iterates through the sorted intervals, merging overlapping intervals and adding non-overlapping intervals to the result list.
- **main(String[] args)**: This method demonstrates the usage of the `merge` method with a sample input.

**Steps**:
1. **Sort Intervals**: Sort the intervals based on their starting times.
2. **Merge Intervals**: Iterate through the sorted intervals and merge overlapping intervals.
3. **Add Non-Overlapping Intervals**: Add non-overlapping intervals to the result list.

This implementation ensures that the intervals are merged correctly and efficiently.

Feel free to ask if you have any questions or need further assistance!

## Course Schedule
The "Course Schedule" problem involves determining if you can finish all courses given their prerequisites. This problem can be represented as a Directed Acyclic Graph (DAG) and solved using topological sorting. Here's a Java solution using Depth-First Search (DFS) to detect cycles in the graph:

```java
import java.util.ArrayList;
import java.util.List;

public class CourseSchedule {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            graph.add(new ArrayList<>());
        }
        for (int[] prerequisite : prerequisites) {
            graph.get(prerequisite[1]).add(prerequisite[0]);
        }

        boolean[] visited = new boolean[numCourses];
        boolean[] recStack = new boolean[numCourses];

        for (int i = 0; i < numCourses; i++) {
            if (isCyclic(i, graph, visited, recStack)) {
                return false;
            }
        }

    private boolean isCyclic(int node, List<List<Integer>> graph, boolean[] visited, boolean[] recStack) {
        if (recStack[node]) {
            return true;
        }
        if (visited[node]) {
            return false;
        }

        visited[node] = true;
        recStack[node] = true;

        for (int neighbor : graph.get(node)) {
            if (isCyclic(neighbor, graph, visited, recStack)) {
                false;
        return false;
    }

    public static void main(String[] args) {
        CourseSchedule cs = new CourseSchedule();
        int numCourses = 4;
        int[][] prerequisites = {{1, 0}, {2, 1}, {3, 2}};
        System.out.println(cs.canFinish(numCourses, prerequisites)); // Output: true
    }
}
```

### Explanation:
- **canFinish(int numCourses, int[][] prerequisites)**: This method initializes the graph and checks for cycles using DFS.
  - It creates an adjacency list to represent the graph.
  - It uses two boolean arrays, `visited` and `recStack`, to keep track of visited nodes and the recursion stack, respectively.
  - It iterates through each course and checks for cycles using the `isCyclic` method.
- **isCyclic(int node, List<List<Integer>> graph, boolean[] visited, boolean[] recStack)**: This helper method performs DFS to detect cycles.
  - It returns `true` if a cycle is detected, otherwise `false`.

This approach ensures that you can determine if all courses can be finished by checking for cycles in the graph.

Feel free to ask if you have any questions or need further assistance!
## Job Schedule

The "Job Scheduling" problem can refer to various scenarios, such as scheduling jobs on a single machine to minimize completion time, scheduling jobs on multiple machines, or scheduling jobs with deadlines and profits. Here's a basic example of scheduling jobs with deadlines and profits using a greedy algorithm:

### Problem Statement:
Given a set of jobs where each job has a deadline and a profit, schedule the jobs to maximize the total profit. Each job takes one unit of time to complete.

### Java Implementation:

```java
import java.util.Arrays;

class Job {
    int id, deadline, profit;

    public Job(int id, int deadline, int profit) {
        this.id = id;
        this.deadline = deadline;
        this.profit = profit;
    }
}

public class JobScheduling {
    public static int[] scheduleJobs(Job[] jobs, int maxDeadline) {
        // Sort jobs by profit in descending order
        Arrays.sort(jobs, (a, b) -> b.profit - a.profit);

        // Array to keep track of free time slots
        boolean[] timeSlots = new boolean[maxDeadline];
        // Array to store the result (sequence of jobs)
        int[] result = new int[maxDeadline];

        // Initialize result array
        Arrays.fill(result, -1);

        // Iterate through all given jobs
        for (Job job : jobs) {
            // Find a free time slot for this job (starting from the last possible slot)
            for (int j = Math.min(maxDeadline - 1, job.deadline - 1); j >= 0; j--) {
                if (!timeSlots[j]) {
                    timeSlots[j] = true;
                    result[j] = job.id;
                    break;
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        Job[] jobs = {
            new Job(1, 2, 100),
            new Job(2, 1, 19),
            new Job(3, 2, 27),
            new Job(4, 1, 25),
            new Job(5, 3, 15)
        };

        int maxDeadline = 3; // Maximum deadline among all jobs
        int[] scheduledJobs = scheduleJobs(jobs, maxDeadline);

        System.out.println("Scheduled Jobs:");
        for (int jobId : scheduledJobs) {
            if (jobId != -1) {
                System.out.print("Job " + jobId + " ");
            }
        }
    }
}
```

### Explanation:
- **Job Class**: Represents a job with an ID, deadline, and profit.
- **scheduleJobs(Job[] jobs, int maxDeadline)**: This method schedules the jobs to maximize profit.
  - It sorts the jobs by profit in descending order.
  - It uses a boolean array `timeSlots` to keep track of free time slots.
  - It iterates through the jobs and assigns each job to the latest possible free time slot before its deadline.
- **main(String[] args)**: Demonstrates the usage of the `scheduleJobs` method with a sample input.

This implementation ensures that the jobs are scheduled to maximize the total profit while respecting their deadlines.

Feel free to ask if you have any questions or need further assistance!

## CPU Scheduling

Sure! Let's implement a simple CPU scheduling algorithm in Java. We'll start with the First Come First Serve (FCFS) algorithm, which is one of the simplest scheduling algorithms.

### First Come First Serve (FCFS) Scheduling

Here's a basic implementation of FCFS scheduling in Java:

```java
import java.util.LinkedList;
import java.util.Queue;

class Process {
    int pid; // Process ID
    int burstTime; // Burst Time

    public Process(int pid, int burstTime) {
        this.pid = pid;
        this.burstTime = burstTime;
    }
}

public class FCFS {
    public static void main(String[] args) {
        Queue<Process> processQueue = new LinkedList<>();
        processQueue.add(new Process(1, 5));
        processQueue.add(new Process(2, 3));
        processQueue.add(new Process(3, 8));
        processQueue.add(new Process(4, 6));

        int currentTime = 0;
        int totalWaitingTime = 0;
        int totalTurnaroundTime = 0;

        System.out.println("Process ID | Burst Time | Waiting Time | Turnaround Time");

        while (!processQueue.isEmpty()) {
            Process currentProcess = processQueue.poll();
            int waitingTime = currentTime;
            int turnaroundTime = waitingTime + currentProcess.burstTime;

            totalWaitingTime += waitingTime;
            totalTurnaroundTime += turnaroundTime;

            System.out.println(currentProcess.pid + "          | " + currentProcess.burstTime + "         | " + waitingTime + "           | " + turnaroundTime);

            currentTime += currentProcess.burstTime;
        }

        int numProcesses = 4;
        System.out.println("Average Waiting Time: " + (double) totalWaitingTime / numProcesses);
        System.out.println("Average Turnaround Time: " + (double) totalTurnaroundTime / numProcesses);
    }
}
```

### Explanation:
- **Process Class**: Represents a process with a process ID and burst time.
- **FCFS Class**: Implements the FCFS scheduling algorithm.
  - **processQueue**: A queue to hold the processes in the order they arrive.
  - **currentTime**: Keeps track of the current time.
  - **totalWaitingTime** and **totalTurnaroundTime**: Keep track of the total waiting and turnaround times for calculating averages.
  - **while loop**: Processes each process in the queue, calculates waiting and turnaround times, and updates the current time.

### Output:
The program will print the process ID, burst time, waiting time, and turnaround time for each process, along with the average waiting and turnaround times.

Feel free to ask if you have any questions or need further assistance with other scheduling algorithms like SJF, Priority Scheduling, or Round Robin!




## Bitwise most asked question

Bit manipulation is a powerful technique in programming that allows you to perform operations at the bit level. Here are some top bit manipulation problems in Java along with their solutions:

### 1. Check if a Number is a Power of Two
A number is a power of two if it has exactly one bit set in its binary representation.

```java
public class PowerOfTwo {
    public static void main(String[] args) {
        int num = 16;
        System.out.println(num + " is power of two: " + isPowerOfTwo(num));
    }

    public static boolean isPowerOfTwo(int num) {
        return num > 0 && (num & (num - 1)) == 0;
    }
}
```

### 2. Count the Number of 1 Bits (Hamming Weight)
Count the number of set bits (1s) in the binary representation of an integer.

```java
public class HammingWeight {
    public static void main(String[] args) {
        int num = 29; // Binary: 11101
        System.out.println("Number of 1 bits: " + countBits(num));
    }

    public static int countBits(int num) {
        int count = 0;
        while (num != 0) {
            count += num & 1;
            num >>= 1;
        }
        return count;
    }
}
```

### 3. Reverse Bits of an Integer
Reverse the bits of a given 32-bit unsigned integer.

```java
public class ReverseBits {
    public static void main(String[] args) {
        int num = 43261596; // Binary: 00000010100101000001111010011100
        System.out.println("Reversed bits: " + reverseBits(num));
    }

    public static int reverseBits(int num) {
        int result = 0;
        for (int i = 0; i < 32; i++) {
            result <<= 1;
            result |= (num & 1);
            num >>= 1;
        }
        return result;
    }
}
```

### 4. Find the Single Number in an Array
Given an array where every element appears twice except for one, find that single one using XOR.

```java
public class SingleNumber {
    public static void main(String[] args) {
        int[] arr = {4, 1, 2, 1, 2};
        System.out.println("Single number: " + findSingleNumber(arr));
    }

    public static int findSingleNumber(int[] arr) {
        int result = 0;
        for (int num : arr) {
            result ^= num;
        }
        return result;
    }
}
```

### 5. Find the Missing Number in an Array
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the missing number using XOR.

```java
public class MissingNumber {
    public static void main(String[] args) {
        int[] arr = {3, 0, 1};
        System.out.println("Missing number: " + findMissingNumber(arr));
    }

    public static int findMissingNumber(int[] arr) {
        int n = arr.length;
        int xor = 0;
        for (int i = 0; i < n; i++) {
            xor ^= arr[i];
        }
        for (int i = 0; i <= n; i++) {
            xor ^= i;
        }
        return xor;
    }
}
```

### 6. Swap Two Numbers Without Using a Third Variable
Using the XOR bitwise operator, you can swap two numbers without a temporary variable.

```java
public class SwapNumbers {
    public static void main(String[] args) {
        int a = 5, b = 3;
        System.out.println("Before swap: a = " + a + ", b = " + b);
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;
        System.out.println("After swap: a = " + a + ", b = " + b);
    }
}
```

These problems cover a range of bit manipulation techniques and demonstrate their utility in solving various tasks efficiently. Feel free to try them out and let me know if you have any questions or need further assistance!


## Top most Ascii based questions

ASCII-based questions often involve manipulating and working with characters and their ASCII values. Here are some top ASCII-based questions in Java along with their solutions:

### 1. Convert Character to ASCII Value
Write a program to convert a character to its ASCII value.

```java
public class CharToASCII {
    public static void main(String[] args) {
        char ch = 'A';
        int asciiValue = (int) ch;
        System.out.println("The ASCII value of " + ch + " is: " + asciiValue);
    }
}
```

### 2. Convert ASCII Value to Character
Write a program to convert an ASCII value to its corresponding character.

```java
public class ASCIIToChar {
    public static void main(String[] args) {
        int asciiValue = 65;
        char ch = (char) asciiValue;
        System.out.println("The character for ASCII value " + asciiValue + " is: " + ch);
    }
}
```

### 3. Check if a Character is a Digit
Write a program to check if a given character is a digit.

```java
public class CheckDigit {
    public static void main(String[] args) {
        char ch = '5';
        if (ch >= '0' && ch <= '9') {
            System.out.println(ch + " is a digit.");
        } else {
            System.out.println(ch + " is not a digit.");
        }
    }
}
```

### 4. Check if a Character is an Alphabet
Write a program to check if a given character is an alphabet (either uppercase or lowercase).

```java
public class CheckAlphabet {
    public static void main(String[] args) {
        char ch = 'A';
        if ((ch >= 'A' && ch <= 'Z') || (ch >= 'a' && ch <= 'z')) {
            System.out.println(ch + " is an alphabet.");
        } else {
            System.out.println(ch + " is not an alphabet.");
        }
    }
}
```

### 5. Convert Lowercase to Uppercase
Write a program to convert a lowercase character to uppercase using ASCII values.

```java
public class LowerToUpper {
    public static void main(String[] args) {
        char ch = 'a';
        char upperCh = (char) (ch - 32);
        System.out.println("The uppercase of " + ch + " is: " + upperCh);
    }
}
```

### 6. Convert Uppercase to Lowercase
Write a program to convert an uppercase character to lowercase using ASCII values.

```java
public class UpperToLower {
    public static void main(String[] args) {
        char ch = 'A';
        char lowerCh = (char) (ch + 32);
        System.out.println("The lowercase of " + ch + " is: " + lowerCh);
    }
}
```

### 7. Print ASCII Values of All Characters
Write a program to print the ASCII values of all characters from 0 to 127.

```java
public class PrintASCIIValues {
    public static void main(String[] args) {
        for (int i = 0; i <= 127; i++) {
            System.out.println("ASCII value of " + (char) i + " is: " + i);
        }
    }
}
```

These questions cover a range of basic operations involving ASCII values and characters. They are great for understanding how characters are represented and manipulated in Java. Feel free to try them out and let me know if you have any questions or need further assistance!