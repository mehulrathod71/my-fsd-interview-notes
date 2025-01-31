# Coding Question Pattern

LeetCode coding questions often follow specific patterns that can help you identify the right approach to solve them. Here are some of the most common patterns:

1. **Sliding Window**: Used for problems involving subarrays or substrings within a certain window size. Example: Finding the longest substring without repeating characters.

2. **Two Pointers**: Useful for problems involving pairs in a sorted array or linked list. Example: Finding two numbers that add up to a specific target.

3. **Fast and Slow Pointers**: Also known as the Hare and Tortoise algorithm, used for detecting cycles in linked lists. Example: Detecting a cycle in a linked list.

4. **Merge Intervals**: Deals with overlapping intervals. Example: Merging overlapping intervals.

5. **Cyclic Sort**: Used for problems involving arrays with numbers in a given range. Example: Finding the missing number in an array.

6. **In-place Reversal of a Linked List**: Used for problems requiring the reversal of a linked list or a part of it. Example: Reversing a sublist within a linked list.

7. **Tree Depth-First Search (DFS)**: Used for tree traversal problems. Example: Finding all paths for a sum in a binary tree.

8. **Tree Breadth-First Search (BFS)**: Used for level order traversal of a tree. Example: Finding the minimum depth of a binary tree.

9. **Binary Search**: Used for searching in a sorted array. Example: Finding the position of a target value in a sorted array.

10. **Dynamic Programming**: Used for optimization problems. Example: Finding the longest increasing subsequence.

11. **Greedy Algorithms**: Used for optimization problems where local optimal choices lead to a global optimal solution. Example: Activity selection problem.

12. **Backtracking**: Used for problems involving permutations, combinations, and subsets. Example: Solving the N-Queens problem.

13. **Graph Depth-First Search (DFS)**: Used for graph traversal problems. Example: Finding connected components in a graph.

14. **Graph Breadth-First Search (BFS)**: Used for shortest path problems in unweighted graphs. Example: Finding the shortest path in a maze.
15. **Divide and Conquer** 

These patterns can help you approach and solve a wide range of coding problems on LeetCode[1](https://leetcode.com/discuss/study-guide/4039411/14-Patterns-to-Ace-Any-Coding-Interview-Question)[2](https://www.teamblind.com/blog/top-leetcode-patterns-coding-interview-questions/)[3](https://seanprashad.com/leetcode-patterns/).

Would you like more details on any specific pattern or an example problem?

[1](https://leetcode.com/discuss/study-guide/4039411/14-Patterns-to-Ace-Any-Coding-Interview-Question): [14 Patterns to Ace Any Coding Interview Question](https://leetcode.com/discuss/study-guide/4039411/14-Patterns-to-Ace-Any-Coding-Interview-Question)
[2](https://www.teamblind.com/blog/top-leetcode-patterns-coding-interview-questions/): [The 14 Patterns You Should Know to Ace Coding Interview Questions](https://www.teamblind.com/blog/top-leetcode-patterns-coding-interview-questions/)
[3](https://seanprashad.com/leetcode-patterns/): [Leetcode Patterns - Sean Prashad](https://seanprashad.com/leetcode-patterns/)


# Patterns

## Prefix Sum

A **prefix sum**, also known as a cumulative sum, is a technique used to efficiently calculate the sum of elements in an array up to a certain index. It is particularly useful for range sum queries and dynamic programming problems.

### How Prefix Sum Works
The prefix sum of an array is a new array where each element at index `i` is the sum of all elements from the start of the original array up to index `i`.

#### Example:
Given an array `a = [1, 2, 3, 4, 5]`, the prefix sum array `pref` would be `[1, 3, 6, 10, 15]`. This can be calculated as follows:
- `pref[0] = a[0]`
- `pref[1] = a[0] + a[1]`
- `pref[2] = a[0] + a[1] + a[2]`
- `pref[3] = a[0] + a[1] + a[2] + a[3]`
- `pref[4] = a[0] + a[1] + a[2] + a[3] + a[4]`

### Example in Java

Here's a simple example of how to calculate the prefix sum of an array in Java:

```java
import java.util.Arrays;

public class PrefixSumExample {
    public static void main(String[] args) {
        int[] originalArray = {1, 2, 3, 4, 5};
        int[] prefixSumArray = new int[originalArray.length];

        // The first element of the prefix sum array is the same as the original array
        prefixSumArray[0] = originalArray[0];

        // Calculate the prefix sum
        for (int i = 1; i < originalArray.length; i++) {
            prefixSumArray[i] = prefixSumArray[i - 1] + originalArray[i];
        }

        // Print the original and prefix sum arrays
        System.out.println("Original Array: " + Arrays.toString(originalArray));
        System.out.println("Prefix Sum Array: " + Arrays.toString(prefixSumArray));
    }
}
```

### Explanation
1. **Initialization**: We initialize the `prefixSumArray` with the same length as the `originalArray`.
2. **First Element**: The first element of the `prefixSumArray` is set to the first element of the `originalArray`.
3. **Loop**: We loop through the `originalArray` starting from the second element, and for each element, we add the current element of the `originalArray` to the previous element of the `prefixSumArray`.
4. **Output**: Finally, we print both the original and the prefix sum arrays.

#### Output:
```
Original Array: [1, 2, 3, 4, 5]
Prefix Sum Array: [1, 3, 6, 10, 15]
```

This example demonstrates how to compute the prefix sum in Java, which can be useful for various computational problems[1](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Solve-the-prefix-sum-problem).

Would you like more examples or details on how to use prefix sums in specific problems?

[1](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Solve-the-prefix-sum-problem): [The prefix sum array problem - TheServerSide](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Solve-the-prefix-sum-problem)


## Sliding Window

The **Sliding Window** technique is an efficient way to solve problems involving subarrays or substrings within a certain window size. It reduces the need for nested loops by maintaining a window that slides over the data structure, updating the result incrementally.

### Example: Finding the Maximum Sum of a Subarray of Fixed Size

Here's how you can implement the Sliding Window technique in Java to find the maximum sum of a subarray of a fixed size `k`:

```java
public class SlidingWindow {
    public static int maxSumSubarray(int[] nums, int k) {
        int n = nums.length;
        if (n < k) {
            throw new IllegalArgumentException("Array length must be greater than or equal to k");
        }

        // Compute the sum of the first window
        int maxSum = 0;
        for (int i = 0; i < k; i++) {
            maxSum += nums[i];
        }

        int windowSum = maxSum;
        for (int i = k; i < n; i++) {
            windowSum += nums[i] - nums[i - k];
            maxSum = Math.max(maxSum, windowSum);
        }

        return maxSum;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int k = 3;
        System.out.println("Maximum sum of subarray of size " + k + " is " + maxSumSubarray(nums, k)); // Output: 27
    }
}
```

### Explanation

1. **Initialization**: The `maxSumSubarray` method initializes the sum of the first window of size `k`.
2. **Sliding the Window**: The window slides from the start to the end of the array. For each new position of the window, the sum is updated by subtracting the element that is left out of the window and adding the new element that enters the window.
3. **Updating the Maximum Sum**: The maximum sum is updated at each step if the current window sum is greater than the previous maximum sum.

### Example Output

For the input array `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]` and `k = 3`, the output will be:
```
Maximum sum of subarray of size 3 is 27
```

This approach ensures that the solution is efficient, with a time complexity of \(O(n)\), where \(n\) is the number of elements in the array[1](https://examples.javacodegeeks.com/sliding-window-algorithm-in-java/)[2](https://www.javatpoint.com/sliding-window-algorithm).

Would you like to see another example or have any questions about this implementation?

[1](https://examples.javacodegeeks.com/sliding-window-algorithm-in-java/): [Sliding Window Algorithm - Javatpoint](https://www.javatpoint.com/sliding-window-algorithm)
[2](https://www.javatpoint.com/sliding-window-algorithm): [Sliding Window Algorithm in Java - Examples Java Code Geeks](https://examples.javacodegeeks.com/sliding-window-algorithm-in-java/)


## Two Pointers

The **Two Pointers** technique is a powerful algorithmic approach used to solve problems involving arrays or linked lists. It involves using two pointers to traverse the data structure simultaneously, often starting from different ends or moving at different speeds. This technique is particularly useful for finding pairs, subarrays, or sequences that meet specific criteria.

### Example: Finding Two Numbers that Add Up to a Target

Here's how you can implement the Two Pointers technique in Java to find two numbers in a sorted array that add up to a specific target:

```java
public class TwoPointersExample {
    public static boolean twoSum(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) {
                return true;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }

        return false;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 6, 8, 9};
        int target = 10;
        System.out.println("Two numbers add up to " + target + ": " + twoSum(nums, target)); // Output: true
    }
}
```

### Explanation

1. **Initialization**: The `twoSum` method initializes two pointers, `left` at the start of the array and `right` at the end.
2. **Traversing the Array**: The pointers move towards each other:
   - If the sum of the elements at the two pointers equals the target, return `true`.
   - If the sum is less than the target, increment the `left` pointer to increase the sum.
   - If the sum is greater than the target, decrement the `right` pointer to decrease the sum.
3. **Result**: If the pointers meet without finding a pair that adds up to the target, return `false`.

### Example Output

For the input array `[1, 2, 3, 4, 6, 8, 9]` and target `10`, the output will be:
```
Two numbers add up to 10: true
```

This approach ensures that the solution is efficient, with a time complexity of \(O(n)\), where \(n\) is the number of elements in the array[1](https://www.baeldung.com/java-two-pointer-technique)[2](https://www.javatpoint.com/two-pointers-technique).

Would you like to see another example or have any questions about this implementation?

[1](https://www.baeldung.com/java-two-pointer-technique): [Java Two Pointer Technique - Baeldung](https://www.baeldung.com/java-two-pointer-technique)
[2](https://www.javatpoint.com/two-pointers-technique): [Two Pointers Technique - Javatpoint](https://www.javatpoint.com/two-pointers-technique)

# How Fast and Slow Pointers works and explain with example in java

The **Fast and Slow Pointers** technique, also known as the Tortoise and Hare algorithm, is used to detect cycles in linked lists or arrays. This technique involves using two pointers that move at different speeds. The fast pointer moves two steps at a time, while the slow pointer moves one step at a time. If there is a cycle, the fast pointer will eventually meet the slow pointer.

### Example: Detecting a Cycle in a Linked List

Here's how you can implement the Fast and Slow Pointers technique in Java to detect a cycle in a linked list:

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class LinkedListCycle {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {
                return true; // Cycle detected
            }
        }

        return false; // No cycle
    }

    public static void main(String[] args) {
        LinkedListCycle cycleDetector = new LinkedListCycle();

        // Creating a linked list with a cycle
        ListNode head = new ListNode(3);
        head.next = new ListNode(2);
        head.next.next = new ListNode(0);
        head.next.next.next = new ListNode(-4);
        head.next.next.next.next = head.next; // Creating a cycle

        System.out.println("Cycle detected: " + cycleDetector.hasCycle(head)); // Output: true
    }
}
```

### Explanation

1. **Initialization**: The `hasCycle` method initializes two pointers, `slow` and `fast`, both starting at the head of the linked list.
2. **Traversal**: The `while` loop continues as long as the `fast` pointer and its next node are not null. Inside the loop:
   - The `slow` pointer moves one step at a time.
   - The `fast` pointer moves two steps at a time.
3. **Cycle Detection**: If the `slow` pointer meets the `fast` pointer, a cycle is detected, and the method returns `true`.
4. **No Cycle**: If the loop exits without the pointers meeting, the method returns `false`, indicating no cycle.

### Example Output

For the given linked list with nodes `[3, 2, 0, -4]` and a cycle created by connecting the last node to the second node, the output will be:
```
Cycle detected: true
```

This approach ensures that the solution is efficient, with a time complexity of \(O(n)\), where \(n\) is the number of nodes in the linked list[1](https://emre.me/coding-patterns/fast-slow-pointers/)[2](https://iq.opengenus.org/fast-and-slow-pointer-technique/).

Would you like to see another example or have any questions about this implementation?

[1](https://emre.me/coding-patterns/fast-slow-pointers/): [Coding Patterns: Fast & Slow Pointers - emre.me](https://emre.me/coding-patterns/fast-slow-pointers/)
[2](https://iq.opengenus.org/fast-and-slow-pointer-technique/): [Fast and slow pointer technique in Linked List - OpenGenus IQ](https://iq.opengenus.org/fast-and-slow-pointer-technique/)

## Merge Intervals

The **Merge Intervals** problem involves combining overlapping intervals into a single interval. This is useful in various applications such as scheduling, data analysis, and computational geometry.

### Example: Merging Overlapping Intervals

Here's how you can implement the Merge Intervals algorithm in Java:

```java
import java.util.*;

class Interval {
    int start;
    int end;

    Interval(int start, int end) {
        this.start = start;
        this.end = end;
    }
}

public class MergeIntervals {
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() == 0) {
            return new ArrayList<>();
        }

        // Sort intervals based on the start time
        intervals.sort(Comparator.comparingInt(i -> i.start));

        List<Interval> merged = new ArrayList<>();
        Interval current = intervals.get(0);

        for (int i = 1; i < intervals.size(); i++) {
            Interval next = intervals.get(i);

            if (current.end >= next.start) {
                // Overlapping intervals, merge them
                current.end = Math.max(current.end, next.end);
            } else {
                // Non-overlapping interval, add the current interval to the list
                merged.add(current);
                current = next;
            }
        }

        // Add the last interval
        merged.add(current);

        return merged;
    }

    public static void main(String[] args) {
        MergeIntervals merger = new MergeIntervals();
        List<Interval> intervals = Arrays.asList(
            new Interval(1, 3),
            new Interval(2, 6),
            new Interval(8, 10),
            new Interval(15, 18)
        );

        List<Interval> result = merger.merge(intervals);
        System.out.println("Merged intervals:");
        for (Interval interval : result) {
            System.out.println("[" + interval.start + ", " + interval.end + "]");
        }
    }
}
```

### Explanation

1. **Initialization**: The `merge` method initializes by sorting the intervals based on their start times. This ensures that overlapping intervals are adjacent in the sorted list.
2. **Merging Process**: The algorithm iterates through the sorted intervals:
   - If the current interval overlaps with the next interval (i.e., the end of the current interval is greater than or equal to the start of the next interval), they are merged by updating the end of the current interval to the maximum end of both intervals.
   - If the current interval does not overlap with the next interval, the current interval is added to the merged list, and the next interval becomes the current interval.
3. **Final Step**: After the loop, the last interval is added to the merged list.

### Example Output

For the input intervals `[(1, 3), (2, 6), (8, 10), (15, 18)]`, the output will be:
```
Merged intervals:
[1, 6]
[8, 10]
[15, 18]
```

This approach ensures that the solution is efficient, with a time complexity of \(O(n \log n)\) due to the sorting step, where \(n\) is the number of intervals[1](https://www.baeldung.com/java-collection-merge-overlapping-intervals)[2](https://www.javatpoint.com/merge-overlapping-intervals).

Would you like to see another example or have any questions about this implementation?

[1](https://www.baeldung.com/java-collection-merge-overlapping-intervals): [Merge Overlapping Intervals in a Java Collection - Baeldung](https://www.baeldung.com/java-collection-merge-overlapping-intervals)
[2](https://www.javatpoint.com/merge-overlapping-intervals): [Merge Overlapping Intervals - Javatpoint](https://www.javatpoint.com/merge-overlapping-intervals)

## Cyclic Sort

**Cyclic Sort** is a comparison sorting algorithm that is theoretically optimal in terms of the number of writes to the original array. It works by placing each element at its correct position in the array. This algorithm is particularly useful when dealing with arrays containing elements in a given range, such as 1 to \( n \).

### How Cyclic Sort Works

1. **Cycle Detection**: For each element, determine its correct position by counting the number of elements smaller than it.
2. **Placement**: If the element is not already at its correct position, place it there. This may displace another element, which needs to be placed in its correct position.
3. **Repeat**: Continue this process until all elements are placed at their correct positions.

### Example in Java

Here's how you can implement Cyclic Sort in Java:

```java
public class CyclicSort {
    public static void cyclicSort(int[] nums) {
        int i = 0;
        while (i < nums.length) {
            int correctIndex = nums[i] - 1;
            if (nums[i] != nums[correctIndex]) {
                swap(nums, i, correctIndex);
            } else {
                i++;
            }
        }
    }

    private static void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    public static void main(String[] args) {
        int[] nums = {3, 1, 5, 4, 2};
        cyclicSort(nums);
        System.out.println("Sorted array: " + Arrays.toString(nums)); // Output: [1, 2, 3, 4, 5]
    }
}
```

### Explanation

1. **Initialization**: The `cyclicSort` method initializes a pointer `i` to traverse the array.
2. **Correct Position Check**: For each element, calculate its correct position (`correctIndex`). If the element is not at its correct position, swap it with the element at its correct position.
3. **Swap and Continue**: If the element is already at its correct position, move to the next element. The `swap` method is used to exchange elements in the array.
4. **Result**: The array is sorted in-place with minimal writes.

### Example Output

For the input array `[3, 1, 5, 4, 2]`, the output will be:
```
Sorted array: [1, 2, 3, 4, 5]
```

This approach ensures that the solution is efficient, with a time complexity of \(O(n)\) and a space complexity of \(O(1)\), making it optimal for sorting arrays with elements in a given range[1](https://www.javatpoint.com/cycle-sort)[2](https://algodaily.com/lessons/cycling-through-cycle-sort).

Would you like to see another example or have any questions about this implementation?

[1](https://www.javatpoint.com/cycle-sort): [Cycle Sort - Javatpoint](https://www.javatpoint.com/cycle-sort)
[2](https://algodaily.com/lessons/cycling-through-cycle-sort): [Cycling Through Cycle Sort - AlgoDaily](https://algodaily.com/lessons/cycling-through-cycle-sort)

## In-place Reversal

In-place reversal of a linked list involves reversing the direction of the pointers in the list so that the last node becomes the first node, the second-to-last node becomes the second node, and so on. This can be done iteratively or recursively. Here, I'll explain the iterative approach.

### Iterative Approach

The iterative approach uses three pointers to reverse the linked list: `previous`, `current`, and `next`.

1. **Initialization**: Set `previous` to `null`, `current` to the head of the list, and `next` to `null`.
2. **Traversal and Reversal**: Iterate through the list, reversing the pointers as you go:
   - Save the next node (`next = current.next`).
   - Reverse the current node's pointer (`current.next = previous`).
   - Move the `previous` and `current` pointers one step forward (`previous = current`, `current = next`).
3. **Completion**: When `current` becomes `null`, the list is fully reversed, and `previous` will be the new head of the list.

### Example in Java

Here's how you can implement the in-place reversal of a linked list in Java:

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class ReverseLinkedList {
    public ListNode reverseList(ListNode head) {
        ListNode previous = null;
        ListNode current = head;
        ListNode next = null;

        while (current != null) {
            next = current.next; // Save the next node
            current.next = previous; // Reverse the current node's pointer
            previous = current; // Move previous to current
            current = next; // Move current to next
        }

        return previous; // New head of the reversed list
    }

    public static void main(String[] args) {
        ReverseLinkedList list = new ReverseLinkedList();

        // Creating a linked list: 1 -> 2 -> 3 -> 4 -> 5
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        System.out.println("Original list:");
        printList(head);

        // Reversing the linked list
        ListNode reversedHead = list.reverseList(head);

        System.out.println("Reversed list:");
        printList(reversedHead);
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }
}
```

### Explanation

1. **Initialization**: The `reverseList` method initializes three pointers: `previous`, `current`, and `next`.
2. **Reversal Process**: The `while` loop iterates through the list, reversing the pointers:
   - `next` saves the next node.
   - `current.next` is set to `previous` to reverse the pointer.
   - `previous` and `current` are moved one step forward.
3. **Result**: The method returns `previous`, which is the new head of the reversed list.

### Example Output

For the input linked list `1 -> 2 -> 3 -> 4 -> 5`, the output will be:
```
Original list:
1 2 3 4 5 
Reversed list:
5 4 3 2 1 
```

This approach ensures that the linked list is reversed in-place with a time complexity of \(O(n)\) and a space complexity of \(O(1)\) since no additional space is used[1](https://www.javatpoint.com/how-to-reverse-linked-list-in-java)[2](https://www.baeldung.com/java-reverse-linked-list).

Would you like to see another example or have any questions about this implementation?

[1](https://www.javatpoint.com/how-to-reverse-linked-list-in-java): [How to Reverse Linked List in Java - Javatpoint](https://www.javatpoint.com/how-to-reverse-linked-list-in-java)
[2](https://www.baeldung.com/java-reverse-linked-list): [Reversing a Linked List in Java - Baeldung](https://www.baeldung.com/java-reverse-linked-list)

## Tree Depth-First Search (DFS)

Tree Depth-First Search (DFS) is a traversal algorithm used to explore nodes and edges of a tree data structure. DFS starts at the root node and explores as far as possible along each branch before backtracking. There are three common orders for DFS traversal in trees:

1. **Preorder Traversal**: Visit the root node first, then recursively visit the left subtree, followed by the right subtree.
2. **Inorder Traversal**: Recursively visit the left subtree first, then visit the root node, and finally the right subtree.
3. **Postorder Traversal**: Recursively visit the left subtree, then the right subtree, and finally the root node.

Here's an example of how to implement these traversals in Java:

### Preorder Traversal
```java
class Node {
    int value;
    Node left, right;

    Node(int item) {
        value = item;
        left = right = null;
    }
}

public class BinaryTree {
    Node root;

    void traversePreOrder(Node node) {
        if (node != null) {
            System.out.print(node.value + " ");
            traversePreOrder(node.left);
            traversePreOrder(node.right);
        }
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        System.out.println("Preorder traversal of binary tree is ");
        tree.traversePreOrder(tree.root);
    }
}
```

### Inorder Traversal
```java
void traverseInOrder(Node node) {
    if (node != null) {
        traverseInOrder(node.left);
        System.out.print(node.value + " ");
        traverseInOrder(node.right);
    }
}
```

### Postorder Traversal
```java
void traversePostOrder(Node node) {
    if (node != null) {
        traversePostOrder(node.left);
        traversePostOrder(node.right);
        System.out.print(node.value + " ");
    }
}
```

In the example above, the `BinaryTree` class defines a simple binary tree structure and methods for each type of DFS traversal. The `main` method demonstrates how to create a binary tree and perform a preorder traversal on it.

Would you like more details on any specific traversal or another example?



## Tree Breadth-First Search (BFS)

**Tree Breadth-First Search (BFS)** is a traversal algorithm that explores nodes level by level, starting from the root node and moving to the next level of nodes. It uses a queue to keep track of the nodes to be explored next. BFS is particularly useful for finding the shortest path in an unweighted tree or graph.

### How BFS Works

1. **Initialization**: Start by enqueuing the root node and marking it as visited.
2. **Traversal**: Dequeue a node from the front of the queue, process it, and enqueue all its unvisited children.
3. **Repeat**: Continue this process until the queue is empty.

### Example in Java

Here's how you can implement BFS for a binary tree in Java:

```java
import java.util.LinkedList;
import java.util.Queue;

class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) {
        this.val = val;
        this.left = this.right = null;
    }
}

public class BinaryTreeBFS {
    TreeNode root;

    void bfs(TreeNode node) {
        if (node == null) {
            return;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(node);

        while (!queue.isEmpty()) {
            TreeNode current = queue.poll();
            System.out.print(current.val + " ");

            if (current.left != null) {
                queue.add(current.left);
            }

            if (current.right != null) {
                queue.add(current.right);
            }
        }
    }

    public static void main(String[] args) {
        BinaryTreeBFS tree = new BinaryTreeBFS();
        tree.root = new TreeNode(1);
        tree.root.left = new TreeNode(2);
        tree.root.right = new TreeNode(3);
        tree.root.left.left = new TreeNode(4);
        tree.root.left.right = new TreeNode(5);

        System.out.println("Breadth-First Search traversal of binary tree is:");
        tree.bfs(tree.root);
    }
}
```

### Explanation

1. **Initialization**: The `bfs` method initializes a queue and enqueues the root node.
2. **Traversal**: The `while` loop continues until the queue is empty. In each iteration:
   - Dequeue the front node and process it (print its value).
   - Enqueue the left and right children of the current node if they exist.
3. **Result**: The nodes are processed level by level, starting from the root.

### Example Output

For the given binary tree:
```
    1
   / \
  2   3
 / \
4   5
```
The output will be:
```
Breadth-First Search traversal of binary tree is:
1 2 3 4 5
```

This approach ensures that all nodes are visited level by level, making it suitable for finding the shortest path in unweighted trees or graphs[1](https://www.guru99.com/breadth-first-search-bfs-graph-example.html)[2](https://www.javatpoint.com/bfs-algorithm-in-java).

Would you like to see another example or have any questions about this implementation?

[1](https://www.guru99.com/breadth-first-search-bfs-graph-example.html): [Breadth First Search (BFS) Algorithm with Example - Guru99](https://www.guru99.com/breadth-first-search-bfs-graph-example.html)
[2](https://www.javatpoint.com/bfs-algorithm-in-java): [BFS Algorithm in Java - Javatpoint](https://www.javatpoint.com/bfs-algorithm-in-java)

## Binary Search

**Binary Search** is an efficient algorithm for finding an element in a sorted array. It works by repeatedly dividing the search interval in half and comparing the target value with the middle element. If the target value is equal to the middle element, the search is successful. If the target value is less than the middle element, the search continues in the left half; otherwise, it continues in the right half.

### How Binary Search Works

1. **Initialization**: Start with two pointers, `low` (beginning of the array) and `high` (end of the array).
2. **Middle Element**: Calculate the middle element using `mid = low + (high - low) / 2`.
3. **Comparison**:
   - If the target value matches the middle element, return its index.
   - If the target value is smaller than the middle element, search the left half (`high = mid - 1`).
   - If the target value is larger than the middle element, search the right half (`low = mid + 1`).
4. **Repeat**: Continue this process until `low` exceeds `high` or the target value is found.
5. **Result**: If the target value is not found, return `-1`.

### Example in Java

Here's a simple implementation of Binary Search in Java:

```java
public class BinarySearch {
    public static int binarySearch(int[] array, int key) {
        int low = 0;
        int high = array.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2; // Calculate mid to prevent overflow
            if (array[mid] == key) {
                return mid; // Key found, return index
            } else if (array[mid] < key) {
                low = mid + 1; // Search in the right half
            } else {
                high = mid - 1; // Search in the left half
            }
        }

        return -1; // Key not found
    }

    public static void main(String[] args) {
        int[] numbers = {10, 20, 30, 40, 50};
        int key = 30;
        int result = binarySearch(numbers, key);
        if (result != -1) {
            System.out.println("Element found at index: " + result);
        } else {
            System.out.println("Element not found.");
        }
    }
}
```

### Explanation

1. **Initialization**: The `binarySearch` method initializes `low` and `high` pointers to the start and end of the array, respectively.
2. **Middle Element Calculation**: The middle index `mid` is calculated to avoid overflow.
3. **Comparison and Search**: The target value is compared with the middle element:
   - If equal, the index is returned.
   - If the target is greater, the search continues in the right half.
   - If the target is less, the search continues in the left half.
4. **Result**: If the loop ends without finding the target, `-1` is returned.

### Example Output

For the input array `[10, 20, 30, 40, 50]` and target `30`, the output will be:
```
Element found at index: 2
```

This approach ensures that the search is efficient, with a time complexity of \(O(\log n)\), where \(n\) is the number of elements in the array[1](https://javacodepoint.com/logical-programs/binary-search-in-java-examples/)[2](https://www.javatpoint.com/binary-search-in-java).

Would you like to see another example or have any questions about this implementation?

[1](https://javacodepoint.com/logical-programs/binary-search-in-java-examples/): [Binary Search in Java - Javatpoint](https://www.javatpoint.com/binary-search-in-java)
[2](https://www.javatpoint.com/binary-search-in-java): [Binary Search in Java with Examples - Javacodepoint](https://javacodepoint.com/logical-programs/binary-search-in-java-examples/)

## Dynamic Programming

**Dynamic Programming (DP)** is a method for solving complex problems by breaking them down into simpler subproblems, solving each subproblem just once, and storing their solutions. This approach avoids redundant calculations and optimizes the overall solution. DP is particularly useful for optimization problems where you need to find the minimum or maximum solution.

### Key Concepts of Dynamic Programming

1. **Optimal Substructure**: A problem has an optimal substructure if an optimal solution can be constructed from optimal solutions of its subproblems.
2. **Overlapping Subproblems**: A problem has overlapping subproblems if the same subproblems are solved multiple times.

### Example: Fibonacci Sequence

The Fibonacci sequence is a classic example of a problem that can be efficiently solved using dynamic programming. The sequence is defined as:
$$
F(n) = F(n-1) + F(n-2)
$$
with base cases \( F(0) = 0 \) and \( F(1) = 1 \).

#### Recursive Approach (Inefficient)

```java
public class FibonacciRecursive {
    public static int fibonacci(int n) {
        if (n <= 1) {
            return n;
        }
        return fibonacci(n - 1) + fibonacci(n - 2);
    }

    public static void main(String[] args) {
        int n = 10; // Example: Find the 10th Fibonacci number
        System.out.println("Fibonacci number at position " + n + " is " + fibonacci(n));
    }
}
```

This approach is inefficient because it recalculates the same subproblems multiple times, leading to an exponential time complexity.

#### Dynamic Programming Approach (Efficient)

```java
public class FibonacciDP {
    public static int fibonacci(int n) {
        if (n <= 1) {
            return n;
        }

        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }

    public static void main(String[] args) {
        int n = 10; // Example: Find the 10th Fibonacci number
        System.out.println("Fibonacci number at position " + n + " is " + fibonacci(n));
    }
}
```

### Explanation

1. **Initialization**: The `fibonacci` method initializes an array `dp` to store the Fibonacci numbers up to `n`.
2. **Base Cases**: The base cases \( F(0) = 0 \) and \( F(1) = 1 \) are set.
3. **Filling the DP Table**: The loop fills the `dp` array by summing the previous two values for each position.
4. **Result**: The method returns `dp[n]`, which contains the \( n \)-th Fibonacci number.

### Example Output

For \( n = 10 \), the output will be:
```
Fibonacci number at position 10 is 55
```

This approach ensures that each subproblem is solved only once, resulting in a time complexity of \( O(n) \) and a space complexity of \( O(n) \) due to the array used for storing intermediate results[1](https://www.javatpoint.com/dynamic-programming)[2](https://www.freecodecamp.org/news/learn-dynamic-programming-in-java/).

Would you like to see another example or have any questions about this implementation?

[1](https://www.javatpoint.com/dynamic-programming): [Dynamic Programming - Javatpoint](https://www.javatpoint.com/dynamic-programming)
[2](https://www.freecodecamp.org/news/learn-dynamic-programming-in-java/): [Learn Dynamic Programming Techniques in Java - freeCodeCamp.org](https://www.freecodecamp.org/news/learn-dynamic-programming-in-java/)


## Greedy Algorithms

**Greedy Algorithms** are a class of algorithms that make a series of choices, each of which looks best at the moment, with the hope of finding a global optimum. The key idea is to make the locally optimal choice at each step with the hope that these local solutions will lead to a global solution.

### Key Concepts of Greedy Algorithms

1. **Greedy Choice Property**: A global optimum can be arrived at by selecting the local optimums.
2. **Optimal Substructure**: An optimal solution to the problem contains an optimal solution to subproblems.

### Example: Coin Change Problem

The Coin Change problem is a classic example of a greedy algorithm. The goal is to make change for a given amount using the fewest number of coins from a given set of denominations.

#### Problem Statement

Given a set of coin denominations and a total amount, find the minimum number of coins needed to make the total amount.

### Example in Java

Here's how you can implement the Coin Change problem using a greedy algorithm in Java:

```java
import java.util.Arrays;

public class CoinChange {
    public static int minCoins(int[] coins, int amount) {
        Arrays.sort(coins); // Sort the coin denominations in ascending order
        int count = 0;

        for (int i = coins.length - 1; i >= 0; i--) {
            while (amount >= coins[i]) {
                amount -= coins[i];
                count++;
            }
        }

        return count;
    }

    public static void main(String[] args) {
        int[] coins = {1, 2, 5, 10, 20, 50, 100};
        int amount = 93;
        System.out.println("Minimum coins needed: " + minCoins(coins, amount)); // Output: 5
    }
}
```

### Explanation

1. **Initialization**: The `minCoins` method initializes by sorting the coin denominations in ascending order.
2. **Greedy Choice**: The algorithm iterates through the sorted coin denominations starting from the largest. For each coin, it subtracts the coin's value from the amount as many times as possible and increments the coin count.
3. **Result**: The method returns the total count of coins used to make the amount.

### Example Output

For the input coin denominations `[1, 2, 5, 10, 20, 50, 100]` and amount `93`, the output will be:
```
Minimum coins needed: 5
```
The coins used will be `[50, 20, 20, 2, 1]`.

This approach ensures that the solution is efficient, with a time complexity of \(O(n \log n)\) due to the sorting step, where \(n\) is the number of coin denominations[1](https://www.baeldung.com/java-greedy-algorithms)[2](https://www.javatpoint.com/greedy-algorithms).

Would you like to see another example or have any questions about this implementation?

[1](https://www.baeldung.com/java-greedy-algorithms): [Introduction to Greedy Algorithms with Java - Baeldung](https://www.baeldung.com/java-greedy-algorithms)
[2](https://www.javatpoint.com/greedy-algorithms): [Greedy Algorithms Introduction - Javatpoint](https://www.javatpoint.com/greedy-algorithms)


## Backtracking

**Backtracking** is an algorithmic technique used to solve problems recursively by trying to build a solution incrementally, one piece at a time, and removing those solutions that fail to satisfy the constraints of the problem at any point. It is particularly useful for solving problems with multiple solutions, such as puzzles, permutations, and combinations.

### Key Concepts of Backtracking

1. **Decision Problem**: Search for a feasible solution.
2. **Optimization Problem**: Search for the best solution.
3. **Enumeration Problem**: Find all feasible solutions.

### How Backtracking Works

1. **Incremental Construction**: Start with an empty solution and add elements to it incrementally.
2. **Constraint Checking**: At each step, check if the current solution satisfies the problem's constraints.
3. **Backtrack**: If the current solution does not satisfy the constraints, remove the last added element and try another possibility.
4. **Repeat**: Continue this process until all possible solutions are explored.

### Example: N-Queens Problem

The N-Queens problem is a classic example of backtracking. The goal is to place N queens on an N×N chessboard such that no two queens threaten each other.

#### Java Implementation

Here's how you can implement the N-Queens problem using backtracking in Java:

```java
import java.util.ArrayList;
import java.util.List;

public class NQueens {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> solutions = new ArrayList<>();
        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = '.';
            }
        }
        backtrack(solutions, board, 0);
        return solutions;
    }

    private void backtrack(List<List<String>> solutions, char[][] board, int row) {
        if (row == board.length) {
            solutions.add(construct(board));
            return;
        }

        for (int col = 0; col < board.length; col++) {
            if (isValid(board, row, col)) {
                board[row][col] = 'Q';
                backtrack(solutions, board, row + 1);
                board[row][col] = '.'; // Backtrack
            }
        }
    }

    private boolean isValid(char[][] board, int row, int col) {
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

    private List<String> construct(char[][] board) {
        List<String> path = new ArrayList<>();
        for (int i = 0; i < board.length; i++) {
            path.add(new String(board[i]));
        }
        return path;
    }

    public static void main(String[] args) {
        NQueens nQueens = new NQueens();
        List<List<String>> solutions = nQueens.solveNQueens(4);
        for (List<String> solution : solutions) {
            for (String row : solution) {
                System.out.println(row);
            }
            System.out.println();
        }
    }
}
```

### Explanation

1. **Initialization**: The `solveNQueens` method initializes the board and calls the `backtrack` method.
2. **Backtracking**: The `backtrack` method tries to place a queen in each column of the current row. If a valid position is found, it places the queen and recursively tries to place queens in the next row. If no valid position is found, it backtracks by removing the queen and trying the next column.
3. **Constraint Checking**: The `isValid` method checks if placing a queen at the given position is valid by ensuring no other queens are in the same column, or on the same diagonal.
4. **Constructing Solutions**: The `construct` method converts the board configuration into a list of strings representing the solution.

### Example Output

For \( n = 4 \), the output will be:
```
..Q.
Q...
...Q
.Q..

.Q..
...Q
Q...
..Q.
```

This approach ensures that all possible solutions are explored, making it suitable for problems with multiple solutions[1](https://www.javatpoint.com/backtracking-in-java)[2](https://examples.javacodegeeks.com/backtracking-algorithm/)[3](https://www.programiz.com/dsa/backtracking-algorithm).

Would you like to see another example or have any questions about this implementation?

[1](https://www.javatpoint.com/backtracking-in-java): [Backtracking in Java - Javatpoint](https://www.javatpoint.com/backtracking-in-java)
[2](https://examples.javacodegeeks.com/backtracking-algorithm/): [Backtracking Algorithm - Java Code Geeks](https://examples.javacodegeeks.com/backtracking-algorithm/)
[3](https://www.programiz.com/dsa/backtracking-algorithm): [Backtracking Algorithm - Programiz](https://www.programiz.com/dsa/backtracking-algorithm)

## Graph Depth-First Search (DFS)

**Graph Depth-First Search (DFS)** is a traversal algorithm used to explore nodes and edges of a graph. It starts at a given node (often called the root) and explores as far as possible along each branch before backtracking. DFS can be implemented using either recursion or an explicit stack.

### How DFS Works

1. **Initialization**: Start with a stack (or use recursion) and push the starting node onto the stack.
2. **Traversal**: Pop a node from the stack, mark it as visited, and push all its unvisited adjacent nodes onto the stack.
3. **Repeat**: Continue this process until the stack is empty.

### Example in Java

Here's how you can implement DFS for a graph in Java using an iterative approach with a stack:

```java
import java.util.*;

class Graph {
    private int vertices; // Number of vertices
    private LinkedList<Integer>[] adjacencyList; // Adjacency list

    // Constructor
    Graph(int vertices) {
        this.vertices = vertices;
        adjacencyList = new LinkedList[vertices];
        for (int i = 0; i < vertices; i++) {
            adjacencyList[i] = new LinkedList<>();
        }
    }

    // Add an edge to the graph
    void addEdge(int v, int w) {
        adjacencyList[v].add(w);
    }

    // DFS traversal from a given source
    void DFS(int start) {
        boolean[] visited = new boolean[vertices];
        Stack<Integer> stack = new Stack<>();

        stack.push(start);

        while (!stack.isEmpty()) {
            int node = stack.pop();

            if (!visited[node]) {
                System.out.print(node + " ");
                visited[node] = true;
            }

            for (int neighbor : adjacencyList[node]) {
                if (!visited[neighbor]) {
                    stack.push(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Graph graph = new Graph(5);

        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 2);
        graph.addEdge(2, 0);
        graph.addEdge(2, 3);
        graph.addEdge(3, 3);
        graph.addEdge(3, 4);

        System.out.println("Depth-First Search starting from node 2:");
        graph.DFS(2);
    }
}
```

### Explanation

1. **Graph Representation**: The `Graph` class uses an adjacency list to represent the graph. The constructor initializes the adjacency list for each vertex.
2. **Adding Edges**: The `addEdge` method adds an edge from vertex `v` to vertex `w`.
3. **DFS Traversal**: The `DFS` method performs the DFS traversal:
   - Initialize a `visited` array to keep track of visited nodes.
   - Use a stack to manage the nodes to be explored.
   - Pop a node from the stack, mark it as visited, and push its unvisited neighbors onto the stack.
4. **Main Method**: The `main` method creates a graph, adds edges, and starts the DFS traversal from node 2.

### Example Output

For the given graph:
```
0 -> 1, 2
1 -> 2
2 -> 0, 3
3 -> 3, 4
4 -> 
```
The output will be:
```
Depth-First Search starting from node 2:
2 3 4 0 1
```

This approach ensures that all nodes reachable from the starting node are visited, making it suitable for exploring connected components in a graph[1](https://www.programiz.com/dsa/graph-dfs)[2](https://www.javatpoint.com/depth-first-search-algorithm).

Would you like to see another example or have any questions about this implementation?

[1](https://www.programiz.com/dsa/graph-dfs): [Depth First Search (DFS) Algorithm - Programiz](https://www.programiz.com/dsa/graph-dfs)
[2](https://www.javatpoint.com/depth-first-search-algorithm): [DFS (Depth First Search) algorithm - Javatpoint](https://www.javatpoint.com/depth-first-search-algorithm)


## Graph Breadth-First Search (BFS)

**Graph Breadth-First Search (BFS)** is a traversal algorithm that explores nodes level by level, starting from the root node and moving to the next level of nodes. It uses a queue to keep track of the nodes to be explored next. BFS is particularly useful for finding the shortest path in an unweighted graph.

### How BFS Works

1. **Initialization**: Start by enqueuing the root node and marking it as visited.
2. **Traversal**: Dequeue a node from the front of the queue, process it, and enqueue all its unvisited adjacent nodes.
3. **Repeat**: Continue this process until the queue is empty.

### Example in Java

Here's how you can implement BFS for a graph in Java:

```java
import java.util.*;

class Graph {
    private int vertices; // Number of vertices
    private LinkedList<Integer>[] adjacencyList; // Adjacency list

    // Constructor
    Graph(int vertices) {
        this.vertices = vertices;
        adjacencyList = new LinkedList[vertices];
        for (int i = 0; i++) {
            adjacencyList[i] = new LinkedList<>();
        }
    }

    // Add an edge to the graph
    void addEdge(int v, int w) {
        adjacencyList[v].add(w);
    }

    // BFS traversal from a given source
    void BFS(int start) {
        boolean[] visited = new boolean[vertices];
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.add(start);

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            for (int neighbor : adjacencyList[node]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Graph graph = new Graph(5);

        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 2);
        graph.addEdge(2, 0);
        graph.addEdge(2, 3);
        graph.addEdge(3, 3);
        graph.addEdge(3, 4);

        System.out.println("Breadth-First Search starting from node 2:");
        graph.BFS(2);
    }
}
```

### Explanation

1. **Graph Representation**: The `Graph` class uses an adjacency list to represent the graph. The constructor initializes the adjacency list for each vertex.
2. **Adding Edges**: The `addEdge` method adds an edge from vertex `v` to vertex `w`.
3. **BFS Traversal**: The `BFS` method performs the BFS traversal:
   - Initialize a `visited` array to keep track of visited nodes.
   - Use a queue to manage the nodes to be explored.
   - Enqueue the starting node and mark it as visited.
   - Dequeue a node, process it, and enqueue its unvisited neighbors.
4. **Main Method**: The `main` method creates a graph, adds edges, and starts the BFS traversal from node 2.

### Example Output

For the given graph:
```
0 -> 1, 2
1 -> 2
2 -> 0, 3
3 -> 3, 4
4 -> 
```
The output will be:
```
Breadth-First Search starting from node 2:
2 0 3 1 4
```

This approach ensures that all nodes reachable from the starting node are visited level by level, making it suitable for exploring connected components in a graph[1](https://www.guru99.com/breadth-first-search-bfs-graph-example.html)[2](https://www.javatpoint.com/breadth-first-search-algorithm)[3](https://www.programiz.com/dsa/graph-bfs).

Would you like to see another example or have any questions about this implementation?

[1](https://www.guru99.com/breadth-first-search-bfs-graph-example.html): [Breadth First Search (BFS) Algorithm with Example - Guru99](https://www.guru99.com/breadth-first-search-bfs-graph-example.html)
[2](https://www.javatpoint.com/breadth-first-search-algorithm): [BFS Algorithm - Javatpoint](https://www.javatpoint.com/breadth-first-search-algorithm)
[3](https://www.programiz.com/dsa/graph-bfs): [BFS Graph Algorithm - Programiz](https://www.programiz.com/dsa/graph-bfs)

## Topological Sort

**Topological Sort** is a linear ordering of vertices in a directed acyclic graph (DAG) such that for every directed edge \( u \rightarrow v \), vertex \( u \) comes before vertex \( v \) in the ordering. This is particularly useful in scenarios like task scheduling, where certain tasks must be completed before others.

### How Topological Sort Works

1. **Initialization**: Start with a graph represented using an adjacency list.
2. **Indegree Calculation**: Calculate the indegree (number of incoming edges) for each vertex.
3. **Queue Initialization**: Initialize a queue and enqueue all vertices with an indegree of 0.
4. **Processing Vertices**: Dequeue a vertex from the queue, add it to the topological order, and decrease the indegree of its adjacent vertices. If an adjacent vertex's indegree becomes 0, enqueue it.
5. **Repeat**: Continue this process until the queue is empty.

### Example in Java

Here's how you can implement Topological Sort using Kahn's algorithm in Java:

```java
import java.util.*;

class Graph {
    private int vertices; // Number of vertices
    private LinkedList<Integer>[] adjacencyList; // Adjacency list

    // Constructor
    Graph(int vertices) {
        this.vertices = vertices;
        adjacencyList = new LinkedList[vertices];
        for (int i = 0; i < vertices; i++) {
            adjacencyList[i] = new LinkedList<>();
        }
    }

    // Add an edge to the graph
    void addEdge(int v, int w) {
        adjacencyList[v].add(w);
    }

    // Topological Sort using Kahn's Algorithm
    void topologicalSort() {
        int[] indegree = new int[vertices];
        for (int i = 0; i < vertices; i++) {
            for (int neighbor : adjacencyList[i]) {
                indegree[neighbor]++;
            }
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < vertices; i++) {
            if (indegree[i] == 0) {
                queue.add(i);
            }
        }

        int count = 0;
        List<Integer> topOrder = new ArrayList<>();
        while (!queue.isEmpty()) {
            int node = queue.poll();
            topOrder.add(node);

            for (int neighbor : adjacencyList[node]) {
                if (--indegree[neighbor] == 0) {
                    queue.add(neighbor);
                }
            }
            count++;
        }

        if (count != vertices) {
            System.out.println("There exists a cycle in the graph");
            return;
        }

        System.out.println("Topological Sort:");
        for (int node : topOrder) {
            System.out.print(node + " ");
        }
    }

    public static void main(String[] args) {
        Graph graph = new Graph(6);
        graph.addEdge(5, 2);
        graph.addEdge(5, 0);
        graph.addEdge(4, 0);
        graph.addEdge(4, 1);
        graph.addEdge(2, 3);
        graph.addEdge(3, 1);

        System.out.println("Topological Sort of the given graph:");
        graph.topologicalSort();
    }
}
```

### Explanation

1. **Graph Representation**: The `Graph` class uses an adjacency list to represent the graph. The constructor initializes the adjacency list for each vertex.
2. **Adding Edges**: The `addEdge` method adds a directed edge from vertex `v` to vertex `w`.
3. **Topological Sort**: The `topologicalSort` method performs the topological sorting using Kahn's algorithm:
   - Calculate the indegree of each vertex.
   - Initialize a queue with all vertices having an indegree of 0.
   - Process each vertex by adding it to the topological order and reducing the indegree of its neighbors. Enqueue neighbors with an indegree of 0.
   - Check for cycles by ensuring the count of processed vertices equals the number of vertices.
4. **Main Method**: The `main` method creates a graph, adds edges, and performs the topological sort.

### Example Output

For the given graph:
```
5 -> 2
5 -> 0
4 -> 0
4 -> 1
2 -> 3
3 -> 1
```
The output will be:
```
Topological Sort of the given graph:
5 4 2 3 1 0
```

This approach ensures that the vertices are printed in a topologically sorted order, respecting the dependencies represented by the directed edges[1](https://www.javatpoint.com/topological-sorting)[2](https://www.javatpoint.com/kahns-algorithm-for-topological-sorting-in-java)[3](https://examples.javacodegeeks.com/topological-sort-java-example/).

Would you like to see another example or have any questions about this implementation?

[1](https://www.javatpoint.com/topological-sorting): [Topological Sorting - Javatpoint](https://www.javatpoint.com/topological-sorting)
[2](https://www.javatpoint.com/kahns-algorithm-for-topological-sorting-in-java): [Kahn's Algorithm for Topological Sorting - Javatpoint](https://www.javatpoint.com/kahns-algorithm-for-topological-sorting-in-java)
[3](https://examples.javacodegeeks.com/topological-sort-java-example/): [Topological Sort Java Example - Java Code Geeks](https://examples.javacodegeeks.com/topological-sort-java-example/)

## Scheduling Pattern

The **Scheduling Pattern** is a design pattern used to manage the execution of tasks or jobs at specific intervals or based on certain conditions. This pattern is particularly useful for automating repetitive tasks, handling background processes, and ensuring timely execution of critical operations.

### Key Components of a Job Scheduler

1. **Job**: The unit of work or task that needs to be executed. This can be a simple Java class with an `execute()` method.
2. **Trigger**: Defines when a job should be executed. Triggers can be time-based (e.g., run every hour) or event-based (e.g., trigger when a specific condition is met).
3. **Scheduler**: The core component responsible for managing and executing jobs based on their triggers.

### Example: Simple Job Scheduler in Java

Here's how you can implement a simple job scheduler in Java:

#### Job Interface
```java
interface Job {
    void execute();
}
```

#### Example Job
```java
class ExampleJob implements Job {
    @Override
    public void execute() {
        System.out.println("Executing ExampleJob at " + System.currentTimeMillis());
    }
}
```

#### Trigger Interface
```java
interface Trigger {
    boolean shouldRun();
}
```

#### Time-Based Trigger
```java
class TimeBasedTrigger implements Trigger {
    private long interval;
    private long lastRunTime;

    public TimeBasedTrigger(long interval) {
        this.interval = interval;
        this.lastRunTime = System.currentTimeMillis();
    }

    @Override
    public boolean shouldRun() {
        long currentTime = System.currentTimeMillis();
        if (currentTime - lastRunTime >= interval) {
            lastRunTime = currentTime;
            return true;
        }
        return false;
    }
}
```

#### Scheduler
```java
class Scheduler {
    private List<Job> jobs = new ArrayList<>();
    private List<Trigger> triggers = new ArrayList<>();

    public void addJob(Job job, Trigger trigger) {
        jobs.add(job);
        triggers.add(trigger);
    }

    public void start() {
        while (true) {
            for (int i = 0; i < jobs.size(); i++) {
                if (triggers.get(i).shouldRun()) {
                    jobs.get(i).execute();
                }
            }
            try {
                Thread.sleep(1000); // Check triggers every second
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### Main Method
```java
public class JobSchedulerExample {
    public static void main(String[] args) {
        Scheduler scheduler = new Scheduler();
        Job exampleJob = new ExampleJob();
        Trigger timeBasedTrigger = new TimeBasedTrigger(5000); // Run every 5 seconds

        scheduler.addJob(exampleJob, timeBasedTrigger);
        scheduler.start();
    }
}
```

### Explanation

1. **Job Interface**: Defines a simple interface with an `execute()` method that any job class must implement.
2. **Example Job**: Implements the `Job` interface and defines the task to be executed.
3. **Trigger Interface**: Defines an interface with a `shouldRun()` method to determine when a job should run.
4. **Time-Based Trigger**: Implements the `Trigger` interface and checks if the specified interval has passed since the last run.
5. **Scheduler**: Manages jobs and their triggers. It continuously checks the triggers and executes the corresponding jobs when their triggers indicate they should run.
6. **Main Method**: Creates a scheduler, adds a job with a time-based trigger, and starts the scheduler.

### Example Output

The output will be:
```
Executing ExampleJob at 1643236504884
Executing ExampleJob at 1643236510001
Executing ExampleJob at 1643236515001
Executing ExampleJob at 1643236520001
```

This approach ensures that jobs are executed at specified intervals, making it suitable for automating repetitive tasks[1](https://www.javatpoint.com/design-a-job-scheduler-in-java)[2](https://examples.javacodegeeks.com/java-scheduling-example/).

Would you like to see another example or have any questions about this implementation?

[1](https://www.javatpoint.com/design-a-job-scheduler-in-java): [Design a Job Scheduler in Java - Javatpoint](https://www.javatpoint.com/design-a-job-scheduler-in-java)
[2](https://examples.javacodegeeks.com/java-scheduling-example/): [Java Scheduling Example - Java Code Geeks](https://examples.javacodegeeks.com/java-scheduling-example/)


## Divide and Conquer

The Divide and Conquer approach is a powerful algorithmic technique used to solve complex problems by breaking them down into smaller, more manageable subproblems. Here's a detailed explanation along with some examples in Java:

### Steps of Divide and Conquer
1. **Divide**: Break the problem into smaller subproblems of the same type.
2. **Conquer**: Solve the subproblems recursively. If the subproblems are small enough, solve them directly.
3. **Combine**: Combine the solutions of the subproblems to solve the original problem.

### Example 1: Merge Sort
Merge Sort is a classic example of the Divide and Conquer approach. It divides the array into two halves, recursively sorts them, and then merges the sorted halves.

```java
public class MergeSort {
    public static void mergeSort(int[] array, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            mergeSort(array, left, mid);
            mergeSort(array, mid + 1, right);
            merge(array, left, mid, right);
        }
    }

    private static void merge(int[] array, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        int[] leftArray = new int[n1];
        int[] rightArray = new int[n2];

        for (int i = 0; i < n1; i++) {
            leftArray[i] = array[left + i];
        }
        for (int i = 0; i < n2; i++) {
            rightArray[i] = array[mid + 1 + i];
        }

        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (leftArray[i] <= rightArray[j]) {
                array[k] = leftArray[i];
                i++;
            } else {
                array[k] = rightArray[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            array[k] = leftArray[i];
            i++;
            k++;
        }

        while (j < n2) {
            array[k] = rightArray[j];
            j++;
            k++;
        }
    }

    public static void main(String[] args) {
        int[] array = {12, 11, 13, 5, 6, 7};
        mergeSort(array, 0, array.length - 1);
        System.out.println("Sorted array: " + Arrays.toString(array));
    }
}
```

### Example 2: Quick Sort
Quick Sort is another example where the array is partitioned into two subarrays around a pivot element, and then each subarray is sorted recursively.

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
        quickSort(array, 0, array.length - 1);
        System.out.println("Sorted array: " + Arrays.toString(array));
    }
}
```

### Example 3: Binary Search
Binary Search is a classic example of Divide and Conquer where the array is divided into halves to find the target element.

```java
public class BinarySearch {
    public static int binarySearch(int[] array, int target) {
        return binarySearch(array, target, 0, array.length - 1);
    }

    private static int binarySearch(int[] array, int target, int left, int right) {
        if (left <= right) {
            int mid = left + (right - left) / 2;
            if (array[mid] == target) {
                return mid;
            }
            if (array[mid] > target) {
                return binarySearch(array, target, left, mid - 1);
            } else {
                return binarySearch(array, target, mid + 1, right);
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] array = {2, 3, 4, 10, 40};
        int target = 10;
        int result = binarySearch(array, target);
        System.out.println("Element found at index: " + result);
    }
}
```

These examples illustrate how the Divide and Conquer approach can be applied to different problems in Java. This technique is powerful for solving problems efficiently by breaking them down into smaller, more manageable subproblems[1](https://www.javatpoint.com/divide-and-conquer-introduction)[2](https://www.programiz.com/dsa/divide-and-conquer).

Would you like more details on any specific example or another problem solved using Divide and Conquer?
[1](https://www.javatpoint.com/divide-and-conquer-introduction): [1](https://www.javatpoint.com/divide-and-conquer-introduction)
[2](https://www.programiz.com/dsa/divide-and-conquer): [2](https://www.programiz.com/dsa/divide-and-conquer)


# List of Data structures in DSA

Here's a list of some essential data structures commonly used in Data Structures and Algorithms (DSA):

### Linear Data Structures
1. **Arrays**: A collection of elements identified by index or key.
2. **Linked Lists**: A sequence of nodes where each node points to the next node.
3. **Stacks**: A collection of elements with Last In First Out (LIFO) access.
4. **Queues**: A collection of elements with First In First Out (FIFO) access.
5. **Deques (Double-ended Queues)**: A collection of elements that allows insertion and deletion at both ends.

### Non-Linear Data Structures
1. **Trees**: A hierarchical structure with a root node and child nodes.
   - **Binary Trees**
   - **Binary Search Trees (BST)**
   - **AVL Trees**
   - **Red-Black Trees**
   - **Heaps**
   - **Tries**
2. **Graphs**: A collection of nodes (vertices) and edges connecting them.
   - **Directed Graphs**
   - **Undirected Graphs**
   - **Weighted Graphs**
   - **Unweighted Graphs**

### Hash-Based Structures
1. **Hash Tables**: A collection of key-value pairs with efficient lookup.
2. **Hash Maps**: Similar to hash tables but often used in different contexts.

### Specialized Data Structures
1. **Heaps**: A specialized tree-based structure that satisfies the heap property.
2. **Tries (Prefix Trees)**: A tree-like data structure used to store dynamic sets of strings.
3. **Segment Trees**: A tree used for storing intervals or segments.
4. **Fenwick Trees (Binary Indexed Trees)**: A data structure that provides efficient methods for calculation and manipulation of the prefix sums of a table of values.
5. **Disjoint Set Union (Union-Find)**: A data structure that keeps track of a partition of a set into disjoint (non-overlapping) subsets.

### Abstract Data Types
1. **Lists**: An ordered collection of elements.
2. **Sets**: A collection of unique elements.
3. **Maps**: A collection of key-value pairs.
4. **Multimaps**: A map that allows multiple values for a single key.
5. **Multisets (Bags)**: A set that allows multiple occurrences of the same element.

These data structures form the foundation of many algorithms and are crucial for solving complex problems efficiently[1](https://en.wikipedia.org/wiki/List_of_data_structures)[2](https://dev.to/iuliagroza/complete-introduction-to-the-30-most-essential-data-structures-algorithms-43kd)[3](https://www.almabetter.com/bytes/cheat-sheet/dsa).

Would you like more details on any specific data structure or an example implementation in Java?

[1](https://en.wikipedia.org/wiki/List_of_data_structures): [List of data structures - Wikipedia](https://en.wikipedia.org/wiki/List_of_data_structures)
[2](https://dev.to/iuliagroza/complete-introduction-to-the-30-most-essential-data-structures-algorithms-43kd): [Complete Introduction to the 30 Most Essential Data Structures & Algorithms - DEV Community](https://dev.to/iuliagroza/complete-introduction-to-the-30-most-essential-data-structures-algorithms-43kd)
[3](https://www.almabetter.com/bytes/cheat-sheet/dsa): [DSA Cheat Sheet - AlmaBetter](https://www.almabetter.com/bytes/cheat-sheet/dsa)


## Big(O) Cheat sheet
![ds-cheatseet.png](ds-cheatseet.png)

## Array

In Java, arrays are a fundamental data structure that store elements of the same data type in contiguous memory locations. Here's a deeper look at how arrays work internally:

1. **Memory Allocation**: When you declare an array, memory is allocated based on the specified size and data type. This memory allocation happens in the heap, which is the region of memory reserved for dynamic memory allocation in Java[1](https://dev.to/_bhupeshk_/arrays-and-arraylist-in-java-1jc2).

2. **Contiguous Storage**: Array elements are stored consecutively in memory, ensuring efficient access. This means that elements can be accessed directly using their indices[1](https://dev.to/_bhupeshk_/arrays-and-arraylist-in-java-1jc2).

3. **Indexing**: Each element in the array is assigned an index starting from 0. When you access an element using its index, the Java runtime calculates the memory address of the element based on its index and the size of the data type[1](https://dev.to/_bhupeshk_/arrays-and-arraylist-in-java-1jc2).

4. **Element Access**: Accessing elements by index is very efficient, typically taking constant time, O(1). The runtime retrieves the value stored at the calculated memory address and returns it to the program[1](https://dev.to/_bhupeshk_/arrays-and-arraylist-in-java-1jc2).

5. **Fixed Size**: Arrays in Java have a fixed size, meaning their size cannot be changed after they are created. If you need to store more elements than the array allows, you would need to create a new array with a larger size and copy the elements from the old array to the new one[1](https://dev.to/_bhupeshk_/arrays-and-arraylist-in-java-1jc2).

6. **Primitive vs. Reference Types**: Arrays can hold elements of primitive data types (such as `int`, `float`, `char`) or reference types (such as objects). When an array holds elements of reference types, it actually holds references (memory addresses) to the objects rather than the objects themselves[1](https://dev.to/_bhupeshk_/arrays-and-arraylist-in-java-1jc2).

Would you like to know more about a specific aspect of arrays in Java?

## Linked List

In Java, the `LinkedList` class is part of the Java Collections Framework and implements the `List` and `Deque` interfaces using a doubly linked list. Here's a detailed look at how it works internally:

### Structure
The `LinkedList` class uses a private static inner class called `Node` to represent each element in the list. Each `Node` contains three fields:
- `item`: The value of the node.
- `next`: A reference to the next node in the list.
- `prev`: A reference to the previous node in the list.

Here's a simplified version of the `Node` class:

```java
private static class Node<E> {
    E item;
    Node<E> next;
    Node<E> prev;

    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}
```

### Key Operations
1. **Adding Elements**:
   - **At the Beginning**: The `linkFirst` method adds a new node at the beginning of the list.
   ```java
   private void linkFirst(E e) {
       final Node<E> f = first;
       final Node<E> newNode = new Node<>(null, e, f);
       first = newNode;
       if (f == null)
           last = newNode;
       else
           f.prev = newNode;
       size++;
       modCount++;
   }
   ```
   - **At the End**: The `linkLast` method adds a new node at the end of the list.
   ```java
   void linkLast(E e) {
       final Node<E> l = last;
       final Node<E> newNode = new Node<>(l, e, null);
       last = newNode;
       if (l == null)
           first = newNode;
       else
           l.next = newNode;
       size++;
       modCount++;
   }
   ```

2. **Removing Elements**:
   - **From the Beginning**: The `unlinkFirst` method removes the first node.
   ```java
   private E unlinkFirst(Node<E> f) {
       final E element = f.item;
       final Node<E> next = f.next;
       f.item = null;
       f.next = null; // help GC
       first = next;
       if (next == null)
           last = null;
       else
           next.prev = null;
       size--;
       modCount++;
       return element;
   }
   ```
   - **From the End**: The `unlinkLast` method removes the last node.
   ```java
   private E unlinkLast(Node<E> l) {
       final E element = l.item;
       final Node<E> prev = l.prev;
       l.item = null;
       l.prev = null; // help GC
       last = prev;
       if (prev == null)
           first = null;
       else
           prev.next = null;
       size--;
       modCount++;
       return element;
   }
   ```

### Advantages
- **Dynamic Size**: Unlike arrays, linked lists can grow and shrink dynamically.
- **Efficient Insertions/Deletions**: Adding or removing elements at the beginning or end of the list is efficient (O(1)).

### Disadvantages
- **Memory Overhead**: Each node requires extra memory for storing references to the next and previous nodes.
- **Sequential Access**: Accessing elements by index requires traversing the list from the beginning or end, making it less efficient (O(n)) compared to arrays.

Would you like to explore any specific operations or concepts related to linked lists in Java?

The `LinkedList` class in Java provides a variety of methods to manipulate and interact with the list. Here are some of the key methods:

### Basic Operations
- **add(E e)**: Appends the specified element to the end of the list.
- **add(int index, E element)**: Inserts the specified element at the specified position in the list.
- **addFirst(E e)**: Inserts the specified element at the beginning of the list.
- **addLast(E e)**: Appends the specified element to the end of the list.

### Removal Operations
- **remove()**: Retrieves and removes the head (first element) of the list.
- **remove(int index)**: Removes the element at the specified position in the list.
- **remove(Object o)**: Removes the first occurrence of the specified element from the list.
- **removeFirst()**: Removes and returns the first element from the list.
- **removeLast()**: Removes and returns the last element from the list.

### Access Operations
- **get(int index)**: Returns the element at the specified position in the list.
- **getFirst()**: Returns the first element in the list.
- **getLast()**: Returns the last element in the list.

### Search Operations
- **contains(Object o)**: Returns `true` if the list contains the specified element.
- **indexOf(Object o)**: Returns the index of the first occurrence of the specified element in the list.
- **lastIndexOf(Object o)**: Returns the index of the last occurrence of the specified element in the list.

### Queue Operations
- **offer(E e)**: Adds the specified element as the tail (last element) of the list.
- **poll()**: Retrieves and removes the head (first element) of the list.
- **peek()**: Retrieves, but does not remove, the head (first element) of the list.

### Deque Operations
- **offerFirst(E e)**: Inserts the specified element at the front of the list.
- **offerLast(E e)**: Inserts the specified element at the end of the list.
- **pollFirst()**: Retrieves and removes the first element of the list.
- **pollLast()**: Retrieves and removes the last element of the list.
- **peekFirst()**: Retrieves, but does not remove, the first element of the list.
- **peekLast()**: Retrieves, but does not remove, the last element of the list.

### Iteration
- **iterator()**: Returns an iterator over the elements in the list in proper sequence.
- **listIterator()**: Returns a list iterator over the elements in the list (in proper sequence).

### Miscellaneous
- **size()**: Returns the number of elements in the list.
- **clear()**: Removes all elements from the list.
- **toArray()**: Converts the list to an array.

These methods provide a comprehensive set of operations to manage and manipulate the elements in a `LinkedList`[1](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)[2](https://www.javatpoint.com/java-linkedlist)[3](https://www.w3schools.com/java/java_linkedlist.asp).

Is there a specific method or operation you'd like to explore further?

## Vector

In Java, the `Vector` class is part of the Java Collections Framework and implements a growable array of objects. It is synchronized, making it thread-safe, but this can also lead to performance overhead in multi-threaded environments. Here's a detailed look at how it works internally:

### Internal Working
1. **Dynamic Array**: The `Vector` class is essentially a dynamic array that can grow or shrink as needed. It maintains an array internally to store the elements. When the array becomes full, a new, larger array is created, and the elements are copied over.

2. **Capacity and Capacity Increment**: The `Vector` class keeps track of its capacity (the size of the internal array) and the capacity increment (the amount by which the capacity increases when the array becomes full). If the capacity increment is not specified, the capacity is doubled each time the array needs to grow.
   ```java
   newLength = capacityIncrement == 0 ? currentSize * 2 : currentSize + capacityIncrement;
   ```

3. **Synchronized Methods**: All methods in the `Vector` class are synchronized, which means they are thread-safe. This ensures that only one thread can access a method at a time, preventing concurrent modification issues.

4. **Fail-Fast Iterators**: The iterators provided by the `Vector` class are fail-fast. This means that if the vector is structurally modified at any time after the iterator is created, the iterator will throw a `ConcurrentModificationException`.

### Key Methods
1. **add(E e)**: Adds the specified element to the end of the vector.
   ```java
   public synchronized boolean add(E e) {
       modCount++;
       ensureCapacityHelper(elementCount + 1);
       elementData[elementCount++] = e;
       return true;
   }
   ```

2. **remove(Object o)**: Removes the first occurrence of the specified element from the vector.
   ```java
   public synchronized boolean remove(Object o) {
       modCount++;
       if (o == null) {
           for (int index = 0; index < elementCount; index++)
               if (elementData[index] == null) {
                   fastRemove(index);
                   return true;
               }
       } else {
           for (int index = 0; index < elementCount; index++)
               if (o.equals(elementData[index])) {
                   fastRemove(index);
                   return true;
               }
       }
       return false;
   }
   ```

3. **get(int index)**: Returns the element at the specified position in the vector.
   ```java
   public synchronized E get(int index) {
       if (index >= elementCount)
           throw new ArrayIndexOutOfBoundsException(index);
       return elementData(index);
   }
   ```

4. **size()**: Returns the number of elements in the vector.
   ```java
   public synchronized int size() {
       return elementCount;
   }
   ```

5. **ensureCapacity(int minCapacity)**: Increases the capacity of the vector, if necessary, to ensure that it can hold at least the number of elements specified by the minimum capacity argument.
   ```java
   public synchronized void ensureCapacity(int minCapacity) {
       if (minCapacity > 0) {
           modCount++;
           ensureCapacityHelper(minCapacity);
       }
   }
   ```

### Example Usage
Here's a simple example demonstrating how to use the `Vector` class in Java:

```java
import java.util.Vector;

public class VectorExample {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>();

        // Add elements to the vector
        vector.add(10);
        vector.add(20);
        vector.add(30);

        // Get element at index 1
        System.out.println("Element at index 1: " + vector.get(1));

        // Remove element at index 2
        vector.remove(2);

        // Get the size of the vector
        System.out.println("Size of vector: " + vector.size());
    }
}
```

### Advantages
- **Thread-Safe**: The `Vector` class is synchronized, making it thread-safe.
- **Dynamic Size**: It can grow or shrink dynamically as needed.

### Disadvantages
- **Performance Overhead**: Synchronization can lead to performance overhead in multi-threaded environments.
- **Legacy Class**: The `Vector` class is considered a legacy class. For non-thread-safe implementations, `ArrayList` is preferred.

Would you like to explore any specific methods or concepts related to the `Vector` class in Java?

## Stack

In Java, the `Stack` class is part of the Java Collections Framework and extends the `Vector` class. It represents a last-in-first-out (LIFO) stack of objects. Here's a detailed look at how it works internally and the methods it provides:

### Internal Working
The `Stack` class in Java is essentially a subclass of `Vector`, which means it inherits all the properties and methods of the `Vector` class. However, it adds several methods that allow it to function as a stack. The key operations of a stack are `push`, `pop`, `peek`, and `search`.

### Key Methods
1. **push(E item)**: Adds an item to the top of the stack.
   ```java
   public E push(E item) {
       addElement(item);
       return item;
   }
   ```

2. **pop()**: Removes and returns the item at the top of the stack.
   ```java
   public synchronized E pop() {
       E obj;
       int len = size();
       obj = peek();
       removeElementAt(len - 1);
       return obj;
   }
   ```

3. **peek()**: Returns the item at the top of the stack without removing it.
   ```java
   public synchronized E peek() {
       int len = size();
       if (len == 0)
           throw new EmptyStackException();
       return elementAt(len - 1);
   }
   ```

4. **empty()**: Checks if the stack is empty.
   ```java
   public boolean empty() {
       return size() == 0;
   }
   ```

5. **search(Object o)**: Returns the 1-based position of the object in the stack. If the object is not found, it returns -1.
   ```java
   public synchronized int search(Object o) {
       int i = lastIndexOf(o);
       if (i >= 0) {
           return size() - i;
       }
       return -1;
   }
   ```

### Example Usage
Here's a simple example demonstrating how to use the `Stack` class in Java:

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();

        // Push elements onto the stack
        stack.push(10);
        stack.push(20);
        stack.push(30);

        // Peek at the top element
        System.out.println("Top element: " + stack.peek());

        // Pop elements from the stack
        System.out.println("Popped element: " + stack.pop());
        System.out.println("Popped element: " + stack.pop());

        // Check if the stack is empty
        System.out.println("Is stack empty? " + stack.empty());

        // Search for an element
        stack.push(40);
        stack.push(50);
        System.out.println("Position of 40: " + stack.search(40));
    }
}
```

### Advantages
- **Simple to Use**: The `Stack` class provides a straightforward way to implement stack operations.
- **Built-in Methods**: Inherits useful methods from the `Vector` class.

### Disadvantages
- **Legacy Class**: The `Stack` class is considered a legacy class and is synchronized, which can lead to performance issues in a multi-threaded environment.
- **Alternative**: For better performance and more flexibility, consider using `Deque` implementations like `ArrayDeque` for stack operations.

Would you like to explore any specific methods or concepts related to the `Stack` class in Java?

## Queues

In Java, the `Queue` interface is part of the Java Collections Framework and represents a collection designed for holding elements prior to processing. It follows the First-In-First-Out (FIFO) principle, although there are exceptions like `PriorityQueue` which orders elements based on their priority.

### Internal Working
The `Queue` interface is implemented by several classes, each with its own internal workings:

1. **LinkedList**: Implements `Queue` using a doubly linked list. Elements are added at the end and removed from the beginning.
2. **ArrayDeque**: Implements `Queue` using a resizable array. It provides better performance than `LinkedList` for most operations.
3. **PriorityQueue**: Implements `Queue` using a binary heap. Elements are ordered based on their natural ordering or by a comparator provided at queue construction time.
4. **ArrayBlockingQueue**: Implements `Queue` using a fixed-size array. It is a thread-safe implementation designed for use in concurrent programming.

### Key Methods
Here are some of the key methods provided by the `Queue` interface:

1. **offer(E e)**: Inserts the specified element into the queue if possible.
   ```java
   boolean offer(E e);
   ```

2. **poll()**: Retrieves and removes the head of the queue, or returns `null` if the queue is empty.
   ```java
   E poll();
   ```

3. **peek()**: Retrieves, but does not remove, the head of the queue, or returns `null` if the queue is empty.
   ```java
   E peek();
   ```

4. **remove()**: Retrieves and removes the head of the queue. Throws an exception if the queue is empty.
   ```java
   E remove();
   ```

5. **element()**: Retrieves, but does not remove, the head of the queue. Throws an exception if the queue is empty.
   ```java
   E element();
   ```

### Example Usage
Here's a simple example demonstrating how to use the `Queue` interface with a `LinkedList` implementation:

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();

        // Add elements to the queue
        queue.offer(10);
        queue.offer(20);
        queue.offer(30);

        // Peek at the head of the queue
        System.out.println("Head of queue: " + queue.peek());

        // Remove elements from the queue
        System.out.println("Removed from queue: " + queue.poll());
        System.out.println("Removed from queue: " + queue.poll());

        // Check the head of the queue
        System.out.println("Head of queue: " + queue.peek());
    }
}
```

### Implementations and Their Methods
Different implementations of the `Queue` interface provide additional methods specific to their functionality. For example:

- **LinkedList**: Inherits methods from `List` and `Deque` interfaces.
- **ArrayDeque**: Provides methods like `addFirst`, `addLast`, `removeFirst`, `removeLast`.
- **PriorityQueue**: Provides methods like `comparator`, `iterator`, `toArray`.

For a comprehensive list of methods and detailed explanations, you can refer to the official Java documentation[1](https://www.baeldung.com/java-queue)[2](https://codegym.cc/groups/posts/java-queue-interface-and-implementations)[3](https://www.softwaretestinghelp.com/java-queue-interface/).

Would you like to explore any specific implementation or method in more detail?

[1](https://www.baeldung.com/java-queue): [Guide to the Java Queue Interface - Baeldung](https://www.baeldung.com/java-queue)
[2](https://codegym.cc/groups/posts/java-queue-interface-and-implementations): [Java Queue Interface and its implementations - CodeGym](https://codegym.cc/groups/posts/java-queue-interface-and-implementations)
[3](https://www.softwaretestinghelp.com/java-queue-interface/): [Java Queue - Queue Methods, Queue Implementation & Example](https://www.softwaretestinghelp.com/java-queue-interface/)


## Tree 

In Java, a tree is a non-linear data structure used to represent hierarchical relationships. Trees are composed of nodes, where each node contains data and references to its child nodes. Here's a detailed look at the tree data structure and its methods:

### Components of a Tree
1. **Node**: The basic unit of a tree, containing data and references to child nodes.
2. **Root**: The topmost node in a tree, with no parent.
3. **Parent**: A node that has one or more child nodes.
4. **Child**: A node that has a parent node.
5. **Leaf**: A node with no children.
6. **Subtree**: A tree formed by a node and its descendants.
7. **Depth**: The number of edges from the root to a node.
8. **Height**: The number of edges from a node to the deepest leaf.

### Types of Trees
1. **Binary Tree**: Each node has at most two children.
2. **Binary Search Tree (BST)**: A binary tree where the left child contains values less than the parent, and the right child contains values greater than the parent.
3. **AVL Tree**: A self-balancing binary search tree.
4. **Red-Black Tree**: A self-balancing binary search tree with additional properties to ensure balance.
5. **B-Tree**: A self-balancing search tree for maintaining sorted data and allowing searches, insertions, deletions, and sequential access.

### Basic Operations
1. **Insertion**: Adding a new node to the tree.
2. **Deletion**: Removing a node from the tree.
3. **Traversal**: Visiting all the nodes in a specific order (e.g., in-order, pre-order, post-order).
4. **Searching**: Finding a node with a specific value.

### Example: Binary Search Tree (BST)
Here's a simple implementation of a Binary Search Tree in Java:

```java
class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = right = null;
    }
}

class BinarySearchTree {
    Node root;

    BinarySearchTree() {
        root = null;
    }

    void insert(int key) {
        root = insertRec(root, key);
    }

    Node insertRec(Node root, int key) {
        if (root == null) {
            root = new Node(key);
            return root;
        }
        if (key < root.data)
            root.left = insertRec(root.left, key);
        else if (key > root.data)
            root.right = insertRec(root.right, key);
        return root;
    }

    void inorder() {
        inorderRec(root);
    }

    void inorderRec(Node root) {
        if (root != null) {
            inorderRec(root.left);
            System.out.print(root.data + " ");
            inorderRec(root.right);
        }
    }

    Node search(Node root, int key) {
        if (root == null || root.data == key)
            return root;
        if (root.data > key)
            return search(root.left, key);
        return search(root.right, key);
    }
}

public class Main {
    public static void main(String[] args) {
        BinarySearchTree tree = new BinarySearchTree();

        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        System.out.println("Inorder traversal of the given tree");
        tree.inorder();

        System.out.println("\n\nSearch for 40 in the tree");
        Node result = tree.search(tree.root, 40);
        if (result != null)
            System.out.println("Node found: " + result.data);
        else
            System.out.println("Node not found");
    }
}
```

### Methods in Tree Data Structures
- **insert(int key)**: Inserts a new node with the given key.
- **inorder()**: Performs an in-order traversal of the tree.
- **search(Node root, int key)**: Searches for a node with the given key.

### Advantages
- **Hierarchical Structure**: Ideal for representing hierarchical data.
- **Efficient Searching**: Binary search trees provide efficient searching, insertion, and deletion operations.

### Disadvantages
- **Balancing**: Trees can become unbalanced, leading to inefficient operations. Self-balancing trees like AVL and Red-Black trees address this issue.

Would you like to explore any specific type of tree or operation in more detail?

# How Binary Trees internally works in Java

In Java, a binary tree is a hierarchical data structure in which each node has at most two children, referred to as the left child and the right child. Here's a detailed look at how binary trees work internally:

### Structure
A binary tree is composed of nodes, where each node contains:
- **Data**: The value stored in the node.
- **Left Child**: A reference to the left child node.
- **Right Child**: A reference to the right child node.

Here's a basic implementation of a binary tree node in Java:

```java
class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = right = null;
    }
}
```

### Binary Tree Class
The binary tree class typically contains a reference to the root node and methods to perform various operations like insertion, deletion, and traversal.

```java
public class BinaryTree {
    Node root;

    BinaryTree() {
        root = null;
    }
}
```

### Key Operations
1. **Insertion**: Adding a new node to the tree. In a binary search tree (BST), the new node is added in such a way that the left child contains values less than the parent node, and the right child contains values greater than the parent node.

```java
void insert(int key) {
    root = insertRec(root, key);
}

Node insertRec(Node root, int key) {
    if (root == null) {
        root = new Node(key);
        return root;
    }
    if (key < root.data)
        root.left = insertRec(root.left, key);
    else if (key > root.data)
        root.right = insertRec(root.right, key);
    return root;
}
```

2. **Traversal**: Visiting all the nodes in a specific order. Common traversal methods include:
   - **In-order**: Left, Root, Right
   - **Pre-order**: Root, Left, Right
   - **Post-order**: Left, Right, Root

```java
void inorder() {
    inorderRec(root);
}

void inorderRec(Node root) {
    if (root != null) {
        inorderRec(root.left);
        System.out.print(root.data + " ");
        inorderRec(root.right);
    }
}
```

3. **Searching**: Finding a node with a specific value. In a BST, this can be done efficiently by comparing the value with the current node and traversing left or right accordingly.

```java
Node search(Node root, int key) {
    if (root == null || root.data == key)
        return root;
    if (root.data > key)
        return search(root.left, key);
    return search(root.right, key);
}
```

### Example Usage
Here's how you can use the binary tree class to create a tree and perform some operations:

```java
public class Main {
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();

        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        System.out.println("In-order traversal of the given tree");
        tree.inorder();

        System.out.println("\n\nSearch for 40 in the tree");
        Node result = tree.search(tree.root, 40);
        if (result != null)
            System.out.println("Node found: " + result.data);
        else
            System.out.println("Node not found");
    }
}
```

### Advantages
- **Hierarchical Structure**: Ideal for representing hierarchical data.
- **Efficient Searching**: Binary search trees provide efficient searching, insertion, and deletion operations.

### Disadvantages
- **Balancing**: Trees can become unbalanced, leading to inefficient operations. Self-balancing trees like AVL and Red-Black trees address this issue.

For more detailed information and examples, you can refer to resources like Baeldung[1](https://www.baeldung.com/java-binary-tree) and HappyCoders[2](https://www.happycoders.eu/algorithms/binary-tree-java/).

Would you like to explore any specific type of tree or operation in more detail?

[1](https://www.baeldung.com/java-binary-tree): [Implementing a Binary Tree in Java - Baeldung](https://www.baeldung.com/java-binary-tree)
[2](https://www.happycoders.eu/algorithms/binary-tree-java/): [Binary Tree (+ Java Code Examples) - HappyCoders.eu](https://www.happycoders.eu/algorithms/binary-tree-java/)

## Binary Search Trees (BST)

In Java, a Binary Search Tree (BST) is a specialized form of a binary tree that maintains a sorted order of elements, enabling efficient search, insertion, and deletion operations. Here's a detailed look at how BSTs work internally:

### Structure
A BST is composed of nodes, where each node contains:
- **Data**: The value stored in the node.
- **Left Child**: A reference to the left child node, which contains values less than the node's value.
- **Right Child**: A reference to the right child node, which contains values greater than the node's value.

Here's a basic implementation of a BST node in Java:

```java
class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = right = null;
    }
}
```

### BST Class
The BST class typically contains a reference to the root node and methods to perform various operations like insertion, deletion, and traversal.

```java
public class BinarySearchTree {
    Node root;

    BinarySearchTree() {
        root = null;
    }
}
```

### Key Operations
1. **Insertion**: Adding a new node to the tree. The new node is added in such a way that the left child contains values less than the parent node, and the right child contains values greater than the parent node.

```java
void insert(int key) {
    root = insertRec(root, key);
}

Node insertRec(Node root, int key) {
    if (root == null) {
        root = new Node(key);
        return root;
    }
    if (key < root.data)
        root.left = insertRec(root.left, key);
    else if (key > root.data)
        root.right = insertRec(root.right, key);
    return root;
}
```

2. **Traversal**: Visiting all the nodes in a specific order. Common traversal methods include:
   - **In-order**: Left, Root, Right
   - **Pre-order**: Root, Left, Right
   - **Post-order**: Left, Right, Root

```java
void inorder() {
    inorderRec(root);
}

void inorderRec(Node root) {
    if (root != null) {
        inorderRec(root.left);
        System.out.print(root.data + " ");
        inorderRec(root.right);
    }
}
```

3. **Searching**: Finding a node with a specific value. In a BST, this can be done efficiently by comparing the value with the current node and traversing left or right accordingly.

```java
Node search(Node root, int key) {
    if (root == null || root.data == key)
        return root;
    if (root.data > key)
        return search(root.left, key);
    return search(root.right, key);
}
```

### Example Usage
Here's how you can use the BST class to create a tree and perform some operations:

```java
public class Main {
    public static void main(String[] args) {
        BinarySearchTree tree = new BinarySearchTree();

        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        System.out.println("In-order traversal of the given tree");
        tree.inorder();

        System.out.println("\n\nSearch for 40 in the tree");
        Node result = tree.search(tree.root, 40);
        if (result != null)
            System.out.println("Node found: " + result.data);
        else
            System.out.println("Node not found");
    }
}
```

### Advantages
- **Efficient Searching**: BSTs provide efficient searching, insertion, and deletion operations.
- **Sorted Order**: Elements are maintained in a sorted order, which is useful for various applications.

### Disadvantages
- **Balancing**: BSTs can become unbalanced, leading to inefficient operations. Self-balancing trees like AVL and Red-Black trees address this issue[1](https://favtutor.com/blogs/binary-search-tree-java)[2](https://geeksprogramming.com/bsts-java-comprehensive-guide/)[3](https://www.softwaretestinghelp.com/binary-search-tree-in-java/).

Would you like to explore any specific type of tree or operation in more detail?

[1](https://favtutor.com/blogs/binary-search-tree-java): [Binary Search Tree (BST) with Java Code and Examples - FavTutor](https://favtutor.com/blogs/binary-search-tree-java)
[2](https://geeksprogramming.com/bsts-java-comprehensive-guide/): [Binary Search Trees (BSTs) in Java: A Comprehensive Guide - GeeksProgramming](https://geeksprogramming.com/bsts-java-comprehensive-guide/)
[3](https://www.softwaretestinghelp.com/binary-search-tree-in-java/): [Binary Search Tree In Java – Implementation & Code Examples - SoftwareTestingHelp](https://www.softwaretestinghelp.com/binary-search-tree-in-java/)


## AVL Trees

In Java, an AVL tree is a self-balancing binary search tree (BST) named after its inventors, Adelson-Velsky and Landis. The AVL tree maintains its balance by ensuring that the difference in heights between the left and right subtrees of any node is at most one. Here's a detailed look at how AVL trees work internally:

### Structure
An AVL tree is composed of nodes, where each node contains:
- **Data**: The value stored in the node.
- **Height**: The height of the node.
- **Left Child**: A reference to the left child node.
- **Right Child**: A reference to the right child node.

Here's a basic implementation of an AVL tree node in Java:

```java
class Node {
    int data, height;
    Node left, right;

    public Node(int item) {
        data = item;
        height = 1;
        left = right = null;
    }
}
```

### AVL Tree Class
The AVL tree class typically contains a reference to the root node and methods to perform various operations like insertion, deletion, and balancing.

```java
public class AVLTree {
    private Node root;

    // Method to get the height of the node
    int height(Node N) {
        if (N == null)
            return 0;
        return N.height;
    }

    // Method to get the balance factor of the node
    int getBalance(Node N) {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
    }

    // Right rotate subtree rooted with y
    Node rightRotate(Node y) {
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
    Node leftRotate(Node x) {
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
    Node insert(Node node, int key) {
        // Perform the normal BST insertion
        if (node == null)
            return new Node(key);

        if (key < node.data)
            node.left = insert(node.left, key);
        else if (key > node.data)
            node.right = insert(node.right, key);
        else
            return node;

        // Update height of this ancestor node
        node.height = 1 + Math.max(height(node.left), height(node.right));

        // Get the balance factor of this ancestor node to check whether this node became unbalanced
        int balance = getBalance(node);

        // If this node becomes unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.data)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.data)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.data) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.data) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        // Return the (unchanged) node pointer
        return node;
    }

    // Method to perform in-order traversal
    void inorder(Node node) {
        if (node != null) {
            inorder(node.left);
            System.out.print(node.data + " ");
            inorder(node.right);
        }
    }

    // Method to insert a key
    public void insert(int key) {
        root = insert(root, key);
    }

    // Method to perform in-order traversal
    public void inorder() {
        inorder(root);
    }
}
```

### Example Usage
Here's how you can use the AVL tree class to create a tree and perform some operations:

```java
public class Main {
    public static void main(String[] args) {
        AVLTree tree = new AVLTree();

        tree.insert(10);
        tree.insert(20);
        tree.insert(30);
        tree.insert(40);
        tree.insert(50);
        tree.insert(25);

        System.out.println("In-order traversal of the constructed AVL tree is:");
        tree.inorder();
    }
}
```

### Advantages
- **Self-Balancing**: Ensures that the tree remains balanced, providing efficient search, insertion, and deletion operations.
- **Efficient Operations**: Maintains O(log n) time complexity for search, insertion, and deletion.

### Disadvantages
- **Complexity**: More complex to implement compared to simple binary search trees due to the need for balancing operations[1](https://www.baeldung.com/java-avl-trees)[2](https://www.javatpoint.com/avl-tree-program-in-java)[3](https://javadevjournal.com/data-structure/avl-tree/).

Would you like to explore any specific operations or concepts related to AVL trees in more detail?

[1](https://www.baeldung.com/java-avl-trees): [Guide to AVL Trees in Java - Baeldung](https://www.baeldung.com/java-avl-trees)
[2](https://www.javatpoint.com/avl-tree-program-in-java): [AVL Tree program in Java - Javatpoint](https://www.javatpoint.com/avl-tree-program-in-java)
[3](https://javadevjournal.com/data-structure/avl-tree/): [AVL Tree - Java Development Journal](https://javadevjournal.com/data-structure/avl-tree/)

# How Red-Black Trees works internally in Java

Red-Black Trees are a type of self-balancing binary search tree that ensures the tree remains balanced, providing efficient search, insertion, and deletion operations. Here's a detailed look at how Red-Black Trees work internally in Java:

### Structure
A Red-Black Tree is composed of nodes, where each node contains:
- **Data**: The value stored in the node.
- **Color**: Either red or black.
- **Left Child**: A reference to the left child node.
- **Right Child**: A reference to the right child node.
- **Parent**: A reference to the parent node.

### Properties
Red-Black Trees maintain the following properties to ensure balance:
1. **Each node is either red or black**.
2. **The root is always black**.
3. **All leaves (NIL nodes) are black**.
4. **If a node is red, then both its children are black** (no two red nodes can be adjacent).
5. **Every path from a node to its descendant NIL nodes has the same number of black nodes**.

### Key Operations
1. **Insertion**: When a new node is inserted, it is initially colored red. The tree is then adjusted to maintain the Red-Black properties through rotations and recoloring.
2. **Deletion**: When a node is deleted, the tree is adjusted to maintain the Red-Black properties. This may involve rotations and recoloring.
3. **Rotations**: Rotations are used to maintain the balance of the tree. There are two types of rotations:
   - **Left Rotation**: Moves a node down to the left.
   - **Right Rotation**: Moves a node down to the right.

### Example Implementation
Here's a simplified implementation of a Red-Black Tree in Java:

```java
class Node {
    int data;
    Node left, right, parent;
    boolean color; // true for red, false for black

    public Node(int data) {
        this.data = data;
        left = right = parent = null;
        this.color = true; // New nodes are red by default
    }
}

public class RedBlackTree {
    private Node root;
    private Node TNULL;

    public RedBlackTree() {
        TNULL = new Node(0);
        TNULL.color = false;
        root = TNULL;
    }

    // Preorder traversal
    public void preOrder(Node node) {
        if (node != TNULL) {
            System.out.print(node.data + " ");
            preOrder(node.left);
            preOrder(node.right);
        }
    }

    // Inorder traversal
    public void inOrder(Node node) {
        if (node != TNULL) {
            inOrder(node.left);
            System.out.print(node.data + " ");
            inOrder(node.right);
        }
    }

    // Postorder traversal
    public void postOrder(Node node) {
        if (node != TNULL) {
            postOrder(node.left);
            postOrder(node.right);
            System.out.print(node.data + " ");
        }
    }

    // Balance the tree after deletion of a node
    private void fixDelete(Node x) {
        Node s;
        while (x != root && x.color == false) {
            if (x == x.parent.left) {
                s = x.parent.right;
                if (s.color == true) {
                    s.color = false;
                    x.parent.color = true;
                    leftRotate(x.parent);
                    s = x.parent.right;
                }

                if (s.left.color == false && s.right.color == false) {
                    s.color = true;
                    x = x.parent;
                } else {
                    if (s.right.color == false) {
                        s.left.color = false;
                        s.color = true;
                        rightRotate(s);
                        s = x.parent.right;
                    }

                    s.color = x.parent.color;
                    x.parent.color = false;
                    s.right.color = false;
                    leftRotate(x.parent);
                    x = root;
                }
            } else {
                s = x.parent.left;
                if (s.color == true) {
                    s.color = false;
                    x.parent.color = true;
                    rightRotate(x.parent);
                    s = x.parent.left;
                }

                if (s.left.color == false && s.right.color == false) {
                    s.color = true;
                    x = x.parent;
                } else {
                    if (s.left.color == false) {
                        s.right.color = false;
                        s.color = true;
                        leftRotate(s);
                        s = x.parent.left;
                    }

                    s.color = x.parent.color;
                    x.parent.color = false;
                    s.left.color = false;
                    rightRotate(x.parent);
                    x = root;
                }
            }
        }
        x.color = false;
    }

    private void leftRotate(Node x) {
        Node y = x.right;
        x.right = y.left;
        if (y.left != TNULL) {
            y.left.parent = x;
        }
        y.parent = x.parent;
        if (x.parent == null) {
            this.root = y;
        } else if (x == x.parent.left) {
            x.parent.left = y;
        } else {
            x.parent.right = y;
        }
        y.left = x;
        x.parent = y;
    }

    private void rightRotate(Node x) {
        Node y = x.left;
        x.left = y.right;
        if (y.right != TNULL) {
            y.right.parent = x;
        }
        y.parent = x.parent;
        if (x.parent == null) {
            this.root = y;
        } else if (x == x.parent.right) {
            x.parent.right = y;
        } else {
            x.parent.left = y;
        }
        y.right = x;
        x.parent = y;
    }

    // Insert a node
    public void insert(int key) {
        Node node = new Node(key);
        node.parent = null;
        node.data = key;
        node.left = TNULL;
        node.right = TNULL;
        node.color = true; // New node must be red

        Node y = null;
        Node x = this.root;

        while (x != TNULL) {
            y = x;
            if (node.data < x.data) {
                x = x.left;
            } else {
                x = x.right;
            }
        }

        node.parent = y;
        if (y == null) {
            root = node;
        } else if (node.data < y.data) {
            y.left = node;
        } else {
            y.right = node;
        }

        if (node.parent == null) {
            node.color = false;
            return;
        }

        if (node.parent.parent == null) {
            return;
        }

        fixInsert(node);
    }

    private void fixInsert(Node k) {
        Node u;
        while (k.parent.color == true) {
            if (k.parent == k.parent.parent.right) {
                u = k.parent.parent.left;
                if (u.color == true) {
                    u.color = false;
                    k.parent.color = false;
                    k.parent.parent.color = true;
                    k = k.parent.parent;
                } else {
                    if (k == k.parent.left) {
                        k = k.parent;
                        rightRotate(k);
                    }
                    k.parent.color = false;
                    k.parent.parent.color = true;
                    leftRotate(k.parent.parent);
                }
            } else {
                u = k.parent.parent.right;

                if (u.color == true) {
                    u.color = false;
                    k.parent.color = false;
                    k.parent.parent.color = true;
                    k = k.parent.parent;
                } else {
                    if (k == k.parent.right) {
                        k = k.parent;
                        leftRotate(k);
                    }
                    k.parent.color = false;
                    k.parent.parent.color = true;
                    rightRotate(k.parent.parent);
                }
            }
            if (k == root) {
                break;
            }
        }
        root.color = false;
    }

    // Print the tree structure on the screen
    public void printTree() {
        printHelper(this.root, "", true);
    }

    private void printHelper(Node root, String indent, boolean last) {
        if (root != TNULL) {
            System.out.print(indent);
            if (last) {
                System.out.print("R----");
                indent += "   ";
            } else {
                System.out.print("L----");
                indent += "|  ";
            }

            String sColor = root.color ? "RED" : "BLACK";
            System.out.println(root.data + "(" + sColor + ")");
            printHelper(root.left, indent, false);
            printHelper(root.right, indent, true);
        }
    }
}
```

### Example Usage
Here's how you can use the Red-Black Tree class to create a tree and perform some operations:

```java
public class Main {
    public static void main(String[] args) {
        RedBlackTree tree = new RedBlackTree();

        tree.insert(55);
        tree.insert(40);
        tree.insert(65);
        tree.insert(60);
        tree.insert(75);
        tree.insert(57);

        System.out.println("In-order traversal of the constructed Red-Black Tree:");
        tree.inOrder(tree.root);

        System.out.println("\n\nTree structure:");
        tree.printTree();
    }
}
```

### Advantages
- **Self-Balancing**: Ensures that the tree remains balanced, providing efficient search, insertion, and deletion operations.
- **Efficient Operations**: Maintains O(log n) time complexity for search, insertion, and deletion.

### Disadvantages
- **Complexity**: More complex to implement compared to simple binary search trees due to the need for balancing operations[1](https://www.happycoders.eu/algorithms/red-black-tree-java/)[^2

## Heaps

In Java, a heap is a specialized tree-based data structure that satisfies the heap property. Heaps are commonly used to implement priority queues. There are two main types of heaps: **Min-Heaps** and **Max-Heaps**.

### Structure
A heap is typically implemented as a binary tree, but it is often represented using an array for simplicity and efficiency. Here's how the two types of heaps work:

1. **Min-Heap**: The value of each node is greater than or equal to the value of its parent, with the minimum value at the root.
2. **Max-Heap**: The value of each node is less than or equal to the value of its parent, with the maximum value at the root.

### Array Representation
Heaps are usually represented as arrays. For a node at index `i`:
- The left child is at index `2*i + 1`.
- The right child is at index `2*i + 2`.
- The parent is at index `(i - 1) / 2`.

### Key Operations
1. **Insertion**: Add the new element at the end of the heap (array) and then "heapify up" to maintain the heap property by comparing the added element with its parent and swapping if necessary until the correct position is found.
   ```java
   void insert(int key) {
       heap[size] = key;
       int current = size;
       size++;
       while (heap[current] < heap[parent(current)]) {
           swap(current, parent(current));
           current = parent(current);
       }
   }
   ```

2. **Deletion**: Remove the root element (minimum for a min-heap, maximum for a max-heap), replace it with the last element in the heap, and then "heapify down" by comparing the new root with its children and swapping if necessary until the correct position is found.
   ```java
   int extractMin() {
       int popped = heap[0];
       heap[0] = heap[--size];
       heapifyDown(0);
       return popped;
   }

   void heapifyDown(int i) {
       int smallest = i;
       int left = leftChild(i);
       int right = rightChild(i);

       if (left < size && heap[left] < heap[smallest])
           smallest = left;

       if (right < size && heap[right] < heap[smallest])
           smallest = right;

       if (smallest != i) {
           swap(i, smallest);
           heapifyDown(smallest);
       }
   }
   ```

3. **Heapify**: Adjust the heap to maintain the heap property. In heapify-up, the newly added element is compared with its parent and swapped if needed. In heapify-down, the root element is compared with its children and swapped if needed.
   ```java
   void heapifyUp(int i) {
       while (i != 0 && heap[parent(i)] > heap[i]) {
           swap(i, parent(i));
           i = parent(i);
       }
   }
   ```

### Example Implementation
Here's a simple implementation of a Min-Heap in Java:

```java
public class MinHeap {
    private int[] heap;
    private int size;
    private int maxSize;

    public MinHeap(int maxSize) {
        this.maxSize = maxSize;
        this.size = 0;
        heap = new int[this.maxSize];
    }

    private int parent(int pos) { return (pos - 1) / 2; }
    private int leftChild(int pos) { return (2 * pos) + 1; }
    private int rightChild(int pos) { return (2 * pos) + 2; }

    private void swap(int fpos, int spos) {
        int tmp;
        tmp = heap[fpos];
        heap[fpos] = heap[spos];
        heap[spos] = tmp;
    }

    public void insert(int element) {
        heap[size] = element;
        int current = size;
        size++;
        heapifyUp(current);
    }

    private void heapifyUp(int pos) {
        int temp = heap[pos];
        while (pos > 0 && temp < heap[parent(pos)]) {
            heap[pos] = heap[parent(pos)];
            pos = parent(pos);
        }
        heap[pos] = temp;
    }

    public int extractMin() {
        int popped = heap[0];
        heap[0] = heap[--size];
        heapifyDown(0);
        return popped;
    }

    private void heapifyDown(int pos) {
        int smallest = pos;
        int left = leftChild(pos);
        int right = rightChild(pos);

        if (left < size && heap[left] < heap[smallest])
            smallest = left;

        if (right < size && heap[right] < heap[smallest])
            smallest = right;

        if (smallest != pos) {
            swap(pos, smallest);
            heapifyDown(smallest);
        }
    }
}
```

### Advantages
- **Efficient Operations**: Heaps provide efficient insertion, deletion, and access to the minimum or maximum element.
- **Priority Queues**: Ideal for implementing priority queues where quick access to the highest or lowest priority element is needed.

### Disadvantages
- **Not Ordered**: Unlike binary search trees, heaps do not maintain a sorted order of elements.
- **Balancing**: Requires balancing operations (heapify) to maintain the heap property[1](https://www.javatpoint.com/heap-implementation-in-java)[2](https://www.baeldung.com/java-stack-heap)[3](https://docs.oracle.com/cd/E13150_01/jrockit_jvm/jrockit/geninfo/diagnos/garbage_collect.html).

Would you like to explore any specific operations or concepts related to heaps in more detail?

[1](https://www.javatpoint.com/heap-implementation-in-java): [Heap Implementation in Java - Javatpoint](https://www.javatpoint.com/heap-implementation-in-java)
[2](https://www.baeldung.com/java-stack-heap): [Stack Memory and Heap Space in Java - Baeldung](https://www.baeldung.com/java-stack-heap)
[3](https://docs.oracle.com/cd/E13150_01/jrockit_jvm/jrockit/geninfo/diagnos/garbage_collect.html): [Understanding Memory Management - Oracle](https://docs.oracle.com/cd/E13150_01/jrockit_jvm/jrockit/geninfo/diagnos/garbage_collect.html)


## Tries

In Java, a Trie (pronounced "try") is a tree-based data structure used for efficient retrieval of keys, typically strings. Tries are particularly useful for tasks like autocomplete and spell checking. Here's a detailed look at how Tries work internally:

### Structure
A Trie is composed of nodes, where each node contains:
- **Children**: A map or array of child nodes, each representing a character.
- **isEndOfWord**: A boolean flag indicating whether the node represents the end of a word.

Here's a basic implementation of a Trie node in Java:

```java
import java.util.HashMap;
import java.util.Map;

class TrieNode {
    Map<Character, TrieNode> children = new HashMap<>();
    boolean isEndOfWord;

    public TrieNode() {
        isEndOfWord = false;
    }
}
```

### Trie Class
The Trie class typically contains a reference to the root node and methods to perform various operations like insertion, search, and deletion.

```java
public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
}
```

### Key Operations
1. **Insertion**: Adding a new word to the Trie. The word is broken down into characters, and each character is inserted into the Trie. If a character is not already present, a new node is created.

```java
public void insert(String word) {
    TrieNode current = root;
    for (char ch : word.toCharArray()) {
        current = current.children.computeIfAbsent(ch, c -> new TrieNode());
    }
    current.isEndOfWord = true;
}
```

2. **Search**: Checking if a word is present in the Trie. The word is broken down into characters, and each character is checked in the Trie. If all characters are found and the last node's `isEndOfWord` flag is true, the word exists in the Trie.

```java
public boolean search(String word) {
    TrieNode current = root;
    for (char ch : word.toCharArray()) {
        current = current.children.get(ch);
        if (current == null) {
            return false;
        }
    }
    return current.isEndOfWord;
}
```

3. **Deletion**: Removing a word from the Trie. This involves checking if the word exists and then removing the nodes associated with the word, ensuring that no other words are affected.

```java
public void delete(String word) {
    delete(root, word, 0);
}

private boolean delete(TrieNode current, String word, int index) {
    if (index == word.length()) {
        if (!current.isEndOfWord) {
            return false;
        }
        current.isEndOfWord = false;
        return current.children.isEmpty();
    }
    char ch = word.charAt(index);
    TrieNode node = current.children.get(ch);
    if (node == null) {
        return false;
    }
    boolean shouldDeleteCurrentNode = delete(node, word, index + 1) && !node.isEndOfWord;

    if (shouldDeleteCurrentNode) {
        current.children.remove(ch);
        return current.children.isEmpty();
    }
    return false;
}
```

### Example Usage
Here's how you can use the Trie class to insert, search, and delete words:

```java
public class Main {
    public static void main(String[] args) {
        Trie trie = new Trie();

        trie.insert("hello");
        trie.insert("world");

        System.out.println("Search 'hello': " + trie.search("hello")); // true
        System.out.println("Search 'world': " + trie.search("world")); // true
        System.out.println("Search 'java': " + trie.search("java"));   // false

        trie.delete("world");
        System.out.println("Search 'world' after deletion: " + trie.search("world")); // false
    }
}
```

### Advantages
- **Efficient Retrieval**: Tries provide efficient retrieval of keys, especially for prefix-based searches.
- **Prefix Matching**: Ideal for applications like autocomplete and spell checking.

### Disadvantages
- **Memory Usage**: Tries can consume a lot of memory, especially if the alphabet size is large[1](https://www.baeldung.com/trie-java)[2](https://www.techiedelight.com/implement-trie-data-structure-java/)[3](https://dev.to/mlarocca/tries-3ddb).

Would you like to explore any specific operations or concepts related to Tries in more detail?

[1](https://www.baeldung.com/trie-java): [Trie Data Structure in Java - Baeldung](https://www.baeldung.com/trie-java)
[2](https://www.techiedelight.com/implement-trie-data-structure-java/): [Java Implementation of Trie Data Structure - Techie Delight](https://www.techiedelight.com/implement-trie-data-structure-java/)
[3](https://dev.to/mlarocca/tries-3ddb): [Implementing Tries in Java - DEV Community](https://dev.to/mlarocca/tries-3ddb)

## Graph

A graph is a versatile data structure used to represent relationships between pairs of objects. It consists of vertices (or nodes) and edges (or arcs) that connect pairs of vertices. Graphs are widely used in various applications such as social networks, transportation networks, and computer networks.

### Components of a Graph
1. **Vertex (Node)**: Represents an entity, such as a person in a social network or a city in a transportation network.
2. **Edge (Arc)**: Represents a relationship or connection between two vertices, such as a friendship or a road.

### Types of Graphs
1. **Directed Graph (Digraph)**: Edges have a direction, indicating a one-way relationship.
2. **Undirected Graph**: Edges do not have a direction, indicating a two-way relationship.
3. **Weighted Graph**: Edges have weights, representing the cost or distance between vertices.
4. **Unweighted Graph**: Edges do not have weights.

### Graph Representations
1. **Adjacency Matrix**: A 2D array where the element at row `i` and column `j` indicates the presence (and possibly the weight) of an edge between vertices `i` and `j`.
2. **Adjacency List**: An array of lists, where each list contains the neighbors of a vertex.

### Basic Operations
1. **Insertion**: Adding a vertex or an edge to the graph.
2. **Deletion**: Removing a vertex or an edge from the graph.
3. **Traversal**: Visiting all the vertices in the graph. Common traversal methods include:
   - **Depth-First Search (DFS)**: Explores as far as possible along each branch before backtracking.
   - **Breadth-First Search (BFS)**: Explores all neighbors at the present depth before moving on to nodes at the next depth level.

### Example Implementation in Java
Here's a simple implementation of an undirected, unweighted graph using an adjacency list in Java:

```java
import java.util.LinkedList;

class Graph {
    private int V; // Number of vertices
    private LinkedList<Integer> adj[]; // Adjacency lists

    // Constructor
    Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList();
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w) {
        adj[v].add(w); // Add w to v's list.
        adj[w].add(v); // Add v to w's list (since the graph is undirected).
    }

    // Method to perform DFS traversal
    void DFSUtil(int v, boolean visited[]) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int n : adj[v]) {
            if (!visited[n])
                DFSUtil(n, visited);
        }
    }

    // Method to perform DFS traversal starting from a given vertex
    void DFS(int v) {
        boolean visited[] = new boolean[V];
        DFSUtil(v, visited);
    }

    // Method to perform BFS traversal
    void BFS(int s) {
        boolean visited[] = new boolean[V];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int n : adj[s]) {
                if (!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    }
}

public class Main {
    public static void main(String args[]) {
        Graph g = new Graph(4);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 3);

        System.out.println("Depth First Traversal starting from vertex 2:");
        g.DFS(2);

        System.out.println("\nBreadth First Traversal starting from vertex 2:");
        g.BFS(2);
    }
}
```

### Advantages
- **Versatile**: Can represent various types of relationships.
- **Efficient Traversal**: Algorithms like DFS and BFS allow efficient traversal and search.

### Disadvantages
- **Complexity**: Can be complex to implement and manage, especially for large graphs.
- **Memory Usage**: Can consume a lot of memory, especially with dense graphs[1](https://www.baeldung.com/java-graphs)[2](https://www.javatpoint.com/java-graph)[3](https://www.programiz.com/java-programming/examples/graph-implementation).

Would you like to explore any specific operations or concepts related to graphs in more detail?

[1](https://www.baeldung.com/java-graphs): [Graphs in Java - Baeldung](https://www.baeldung.com/java-graphs)
[2](https://www.javatpoint.com/java-graph): [Java Graph - Javatpoint](https://www.javatpoint.com/java-graph)
[3](https://www.programiz.com/java-programming/examples/graph-implementation): [Java Program to Implement the graph data structure - Programiz](https://www.programiz.com/java-programming/examples/graph-implementation)


## Directed Graphs 

In Java, a directed graph (or digraph) is a type of graph where edges have a specific direction, indicating a one-way relationship between vertices. Here's a detailed look at how directed graphs work internally and how they can be implemented:

### Structure
A directed graph is composed of:
- **Vertices (Nodes)**: Represent entities or points.
- **Edges (Arcs)**: Represent directed connections between pairs of vertices.

### Representation
Directed graphs can be represented using various methods, with the most common being adjacency lists and adjacency matrices.

#### Adjacency List
An adjacency list represents the graph as an array of lists. Each list corresponds to a vertex and contains a list of its outgoing edges.

```java
import java.util.LinkedList;

class Graph {
    private int V; // Number of vertices
    private LinkedList<Integer> adj[]; // Adjacency lists

    // Constructor
    Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList<>();
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w) {
        adj[v].add(w); // Add w to v's list.
    }

    // Method to perform DFS traversal
    void DFSUtil(int v, boolean visited[]) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int n : adj[v]) {
            if (!visited[n])
                DFSUtil(n, visited);
        }
    }

    // Method to perform DFS traversal starting from a given vertex
    void DFS(int v) {
        boolean visited[] = new boolean[V];
        DFSUtil(v, visited);
    }

    // Method to perform BFS traversal
    void BFS(int s) {
        boolean visited[] = new boolean[V];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int n : adj[s]) {
                if (!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    }
}
```

#### Adjacency Matrix
An adjacency matrix represents the graph as a 2D array. The element at row `i` and column `j` indicates the presence (and possibly the weight) of an edge from vertex `i` to vertex `j`.

```java
class Graph {
    private int V; // Number of vertices
    private int[][] adjMatrix; // Adjacency matrix

    // Constructor
    Graph(int v) {
        V = v;
        adjMatrix = new int[V][V];
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w) {
        adjMatrix[v][w] = 1; // Add edge from v to w
    }

    // Method to perform DFS traversal
    void DFSUtil(int v, boolean visited[]) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int i = 0; i < V; i++) {
            if (adjMatrix[v][i] == 1 && !visited[i])
                DFSUtil(i, visited);
        }
    }

    // Method to perform DFS traversal starting from a given vertex
    void DFS(int v) {
        boolean visited[] = new boolean[V];
        DFSUtil(v, visited);
    }

    // Method to perform BFS traversal
    void BFS(int s) {
        boolean visited[] = new boolean[V];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int i = 0; i < V; i++) {
                if (adjMatrix[s][i] == 1 && !visited[i]) {
                    visited[i] = true;
                    queue.add(i);
                }
            }
        }
    }
}
```

### Key Operations
1. **Insertion**: Adding a vertex or an edge to the graph.
2. **Deletion**: Removing a vertex or an edge from the graph.
3. **Traversal**: Visiting all the vertices in the graph using methods like Depth-First Search (DFS) and Breadth-First Search (BFS).

### Example Usage
Here's how you can use the adjacency list representation to create a directed graph and perform some operations:

```java
public class Main {
    public static void main(String args[]) {
        Graph g = new Graph(4);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 0);
        g.addEdge(2, 3);
        g.addEdge(3, 3);

        System.out.println("Depth First Traversal starting from vertex 2:");
        g.DFS(2);

        System.out.println("\nBreadth First Traversal starting from vertex 2:");
        g.BFS(2);
    }
}
```

### Advantages
- **Versatile**: Can represent various types of relationships.
- **Efficient Traversal**: Algorithms like DFS and BFS allow efficient traversal and search.

### Disadvantages
- **Complexity**: Can be complex to implement and manage, especially for large graphs.
- **Memory Usage**: Can consume a lot of memory, especially with dense graphs[1](https://codepal.ai/code-generator/query/ibv3Mxu9/java-code-implement-directed-graphs)[2](https://dev.to/wittedtech-by-harshit/the-ultimate-guide-to-graphs-in-java-a-deep-dive-for-developers-of-all-levels-fo1)[3](https://www.softwaretestinghelp.com/java-graph-tutorial/).

Would you like to explore any specific operations or concepts related to directed graphs in more detail?

[1](https://codepal.ai/code-generator/query/ibv3Mxu9/java-code-implement-directed-graphs): [Implementing Directed Graphs in Java - CodePal](https://codepal.ai/code-generator/query/ibv3Mxu9/java-code-implement-directed-graphs)
[2](https://dev.to/wittedtech-by-harshit/the-ultimate-guide-to-graphs-in-java-a-deep-dive-for-developers-of-all-levels-fo1): [The Ultimate Guide to Graphs in Java - DEV Community](https://dev.to/wittedtech-by-harshit/the-ultimate-guide-to-graphs-in-java-a-deep-dive-for-developers-of-all-levels-fo1)
[3](https://www.softwaretestinghelp.com/java-graph-tutorial/): [Java Graph Tutorial – How To Implement Graph Data Structure](https://www.softwaretestinghelp.com/java-graph-tutorial/)


# How Undirected Graphs works internally in Java

In Java, an undirected graph is a type of graph where edges have no direction, meaning the relationship between vertices is bidirectional. Here's a detailed look at how undirected graphs work internally and how they can be implemented:

### Structure
An undirected graph is composed of:
- **Vertices (Nodes)**: Represent entities or points.
- **Edges (Arcs)**: Represent bidirectional connections between pairs of vertices.

### Representation
Undirected graphs can be represented using various methods, with the most common being adjacency lists and adjacency matrices.

#### Adjacency List
An adjacency list represents the graph as an array of lists. Each list corresponds to a vertex and contains a list of its adjacent vertices.

```java
import java.util.LinkedList;

class Graph {
    private int V; // Number of vertices
    private LinkedList<Integer> adj[]; // Adjacency lists

    // Constructor
    Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList<>();
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w) {
        adj[v].add(w); // Add w to v's list.
        adj[w].add(v); // Add v to w's list (since the graph is undirected).
    }

    // Method to perform DFS traversal
    void DFSUtil(int v, boolean visited[]) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int n : adj[v]) {
            if (!visited[n])
                DFSUtil(n, visited);
        }
    }

    // Method to perform DFS traversal starting from a given vertex
    void DFS(int v) {
        boolean visited[] = new boolean[V];
        DFSUtil(v, visited);
    }

    // Method to perform BFS traversal
    void BFS(int s) {
        boolean visited[] = new boolean[V];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int n : adj[s]) {
                if (!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    }
}
```

#### Adjacency Matrix
An adjacency matrix represents the graph as a 2D array. The element at row `i` and column `j` indicates the presence (and possibly the weight) of an edge between vertices `i` and `j`.

```java
class Graph {
    private int V; // Number of vertices
    private int[][] adjMatrix; // Adjacency matrix

    // Constructor
    Graph(int v) {
        V = v;
        adjMatrix = new int[V][V];
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w) {
        adjMatrix[v][w] = 1; // Add edge from v to w
        adjMatrix[w][v] = 1; // Add edge from w to v (since the graph is undirected)
    }

    // Method to perform DFS traversal
    void DFSUtil(int v, boolean visited[]) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int i = 0; i < V; i++) {
            if (adjMatrix[v][i] == 1 && !visited[i])
                DFSUtil(i, visited);
        }
    }

    // Method to perform DFS traversal starting from a given vertex
    void DFS(int v) {
        boolean visited[] = new boolean[V];
        DFSUtil(v, visited);
    }

    // Method to perform BFS traversal
    void BFS(int s) {
        boolean visited[] = new boolean[V];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int i = 0; i < V; i++) {
                if (adjMatrix[s][i] == 1 && !visited[i]) {
                    visited[i] = true;
                    queue.add(i);
                }
            }
        }
    }
}
```

### Key Operations
1. **Insertion**: Adding a vertex or an edge to the graph.
2. **Deletion**: Removing a vertex or an edge from the graph.
3. **Traversal**: Visiting all the vertices in the graph using methods like Depth-First Search (DFS) and Breadth-First Search (BFS).

### Example Usage
Here's how you can use the adjacency list representation to create an undirected graph and perform some operations:

```java
public class Main {
    public static void main(String args[]) {
        Graph g = new Graph(4);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 3);

        System.out.println("Depth First Traversal starting from vertex 2:");
        g.DFS(2);

        System.out.println("\nBreadth First Traversal starting from vertex 2:");
        g.BFS(2);
    }
}
```

### Advantages
- **Versatile**: Can represent various types of relationships.
- **Efficient Traversal**: Algorithms like DFS and BFS allow efficient traversal and search.

### Disadvantages
- **Complexity**: Can be complex to implement and manage, especially for large graphs.
- **Memory Usage**: Can consume a lot of memory, especially with dense graphs[1](https://computinglearner.com/undirected-simple-graph-data-structure-implementation-and-usage-in-java/)[2](https://www.algolist.net/Data_structures/Graph/Internal_representation)[3](https://www.youtube.com/watch?v=qEEswKeAzB8).

Would you like to explore any specific operations or concepts related to undirected graphs in more detail?

[1](https://computinglearner.com/undirected-simple-graph-data-structure-implementation-and-usage-in-java/): [Undirected Simple Graph Data Structure: Implementation and usage in Java](https://computinglearner.com/undirected-simple-graph-data-structure-implementation-and-usage-in-java/)
[2](https://www.algolist.net/Data_structures/Graph/Internal_representation): [UNDIRECTED GRAPHS REPRESENTATION :: GRAPH THEORY (Java, C++)](https://www.algolist.net/Data_structures/Graph/Internal_representation)
[3](https://www.youtube.com/watch?v=qEEswKeAzB8): [How To Implement Undirected Graph and Graph Processor In Java](https://www.youtube.com/watch?v=qEEswKeAzB8)


## Weighted Graphs

In Java, a weighted graph is a type of graph where each edge has an associated weight or cost. These weights can represent various properties such as distance, time, or any other numerical value relevant to the problem being modeled. Here's a detailed look at how weighted graphs work internally and how they can be implemented:

### Structure
A weighted graph is composed of:
- **Vertices (Nodes)**: Represent entities or points.
- **Edges (Arcs)**: Represent connections between pairs of vertices, each with an associated weight.

### Representation
Weighted graphs can be represented using various methods, with the most common being adjacency lists and adjacency matrices.

#### Adjacency List
An adjacency list represents the graph as an array of lists. Each list corresponds to a vertex and contains a list of its adjacent vertices along with the weights of the edges connecting them.

```java
import java.util.LinkedList;

class Graph {
    private int V; // Number of vertices
    private LinkedList<Edge>[] adj; // Adjacency lists

    // Edge class to represent an edge with a weight
    static class Edge {
        int destination;
        int weight;

        public Edge(int destination, int weight) {
            this.destination = destination;
            this.weight = weight;
        }
    }

    // Constructor
    Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList<>();
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w, int weight) {
        adj[v].add(new Edge(w, weight)); // Add w to v's list with weight
        adj[w].add(new Edge(v, weight)); // Add v to w's list with weight (for undirected graph)
    }

    // Method to print the graph
    void printGraph() {
        for (int i = 0; i < V; i++) {
            LinkedList<Edge> list = adj[i];
            System.out.print("Vertex " + i + " is connected to: ");
            for (Edge edge : list) {
                System.out.print(edge.destination + " (weight " + edge.weight + ") ");
            }
            System.out.println();
        }
    }
}
```

#### Adjacency Matrix
An adjacency matrix represents the graph as a 2D array. The element at row `i` and column `j` indicates the weight of the edge between vertices `i` and `j`. If there is no edge, the element is typically set to 0 or a large value (e.g., `Integer.MAX_VALUE`) to indicate the absence of a connection.

```java
class Graph {
    private int V; // Number of vertices
    private int[][] adjMatrix; // Adjacency matrix

    // Constructor
    Graph(int v) {
        V = v;
        adjMatrix = new int[V][V];
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w, int weight) {
        adjMatrix[v][w] = weight; // Add edge from v to w with weight
        adjMatrix[w][v] = weight; // Add edge from w to v with weight (for undirected graph)
    }

    // Method to print the graph
    void printGraph() {
        for (int i = 0; i < V; i++) {
            System.out.print("Vertex " + i + " is connected to: ");
            for (int j = 0; j < V; j++) {
                if (adjMatrix[i][j] != 0) {
                    System.out.print(j + " (weight " + adjMatrix[i][j] + ") ");
                }
            }
            System.out.println();
        }
    }
}
```

### Key Operations
1. **Insertion**: Adding a vertex or an edge with a weight to the graph.
2. **Deletion**: Removing a vertex or an edge from the graph.
3. **Traversal**: Visiting all the vertices in the graph using methods like Depth-First Search (DFS) and Breadth-First Search (BFS).
4. **Shortest Path Algorithms**: Algorithms like Dijkstra's and Bellman-Ford are used to find the shortest path between vertices in a weighted graph.

### Example Usage
Here's how you can use the adjacency list representation to create a weighted graph and perform some operations:

```java
public class Main {
    public static void main(String args[]) {
        Graph g = new Graph(4);

        g.addEdge(0, 1, 5);
        g.addEdge(0, 2, 3);
        g.addEdge(1, 2, 2);
        g.addEdge(1, 3, 1);
        g.addEdge(2, 3, 4);

        System.out.println("Graph representation:");
        g.printGraph();
    }
}
```

### Advantages
- **Versatile**: Can represent various types of relationships with associated costs.
- **Efficient Traversal**: Algorithms like DFS and BFS allow efficient traversal and search.

### Disadvantages
- **Complexity**: Can be complex to implement and manage, especially for large graphs.
- **Memory Usage**: Can consume a lot of memory, especially with dense graphs[1](https://labex.io/tutorials/java-how-to-create-a-weighted-graph-in-java-413986)[2](https://tutorialhorizon.com/algorithms/weighted-graph-implementation-java/)[3](https://labex.io/tutorials/java-how-to-handle-graph-edge-weights-in-java-419112).

Would you like to explore any specific operations or concepts related to weighted graphs in more detail?

[1](https://labex.io/tutorials/java-how-to-create-a-weighted-graph-in-java-413986): [How to create a weighted graph in Java - LabEx](https://labex.io/tutorials/java-how-to-create-a-weighted-graph-in-java-413986)
[2](https://tutorialhorizon.com/algorithms/weighted-graph-implementation-java/): [Weighted Graph Implementation – JAVA - TutorialHorizon](https://tutorialhorizon.com/algorithms/weighted-graph-implementation-java/)
[3](https://labex.io/tutorials/java-how-to-handle-graph-edge-weights-in-java-419112): [How to handle graph edge weights in Java - LabEx](https://labex.io/tutorials/java-how-to-handle-graph-edge-weights-in-java-419112)

## Unweighted Graphs

In Java, an unweighted graph is a type of graph where all edges are treated equally, meaning they do not have any associated weights or costs. Here's a detailed look at how unweighted graphs work internally and how they can be implemented:

### Structure
An unweighted graph is composed of:
- **Vertices (Nodes)**: Represent entities or points.
- **Edges (Arcs)**: Represent connections between pairs of vertices without any weights.

### Representation
Unweighted graphs can be represented using various methods, with the most common being adjacency lists and adjacency matrices.

#### Adjacency List
An adjacency list represents the graph as an array of lists. Each list corresponds to a vertex and contains a list of its adjacent vertices.

```java
import java.util.LinkedList;

class Graph {
    private int V; // Number of vertices
    private LinkedList<Integer> adj[]; // Adjacency lists

    // Constructor
    Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList<>();
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w) {
        adj[v].add(w); // Add w to v's list.
        adj[w].add(v); // Add v to w's list (since the graph is undirected).
    }

    // Method to perform DFS traversal
    void DFSUtil(int v, boolean visited[]) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int n : adj[v]) {
            if (!visited[n])
                DFSUtil(n, visited);
        }
    }

    // Method to perform DFS traversal starting from a given vertex
    void DFS(int v) {
        boolean visited[] = new boolean[V];
        DFSUtil(v, visited);
    }

    // Method to perform BFS traversal
    void BFS(int s) {
        boolean visited[] = new boolean[V];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int n : adj[s]) {
                if (!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    }
}
```

#### Adjacency Matrix
An adjacency matrix represents the graph as a 2D array. The element at row `i` and column `j` indicates the presence of an edge between vertices `i` and `j`. If there is no edge, the element is typically set to 0.

```java
class Graph {
    private int V; // Number of vertices
    private int[][] adjMatrix; // Adjacency matrix

    // Constructor
    Graph(int v) {
        V = v;
        adjMatrix = new int[V][V];
    }

    // Method to add an edge into the graph
    void addEdge(int v, int w) {
        adjMatrix[v][w] = 1; // Add edge from v to w
        adjMatrix[w][v] = 1; // Add edge from w to v (since the graph is undirected)
    }

    // Method to perform DFS traversal
    void DFSUtil(int v, boolean visited[]) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int i = 0; i < V; i++) {
            if (adjMatrix[v][i] == 1 && !visited[i])
                DFSUtil(i, visited);
        }
    }

    // Method to perform DFS traversal starting from a given vertex
    void DFS(int v) {
        boolean visited[] = new boolean[V];
        DFSUtil(v, visited);
    }

    // Method to perform BFS traversal
    void BFS(int s) {
        boolean visited[] = new boolean[V];
        LinkedList<Integer> queue = new LinkedList<>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {
            s = queue.poll();
            System.out.print(s + " ");

            for (int i = 0; i < V; i++) {
                if (adjMatrix[s][i] == 1 && !visited[i]) {
                    visited[i] = true;
                    queue.add(i);
                }
            }
        }
    }
}
```

### Key Operations
1. **Insertion**: Adding a vertex or an edge to the graph.
2. **Deletion**: Removing a vertex or an edge from the graph.
3. **Traversal**: Visiting all the vertices in the graph using methods like Depth-First Search (DFS) and Breadth-First Search (BFS).

### Example Usage
Here's how you can use the adjacency list representation to create an unweighted graph and perform some operations:

```java
public class Main {
    public static void main(String args[]) {
        Graph g = new Graph(4);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 3);

        System.out.println("Depth First Traversal starting from vertex 2:");
        g.DFS(2);

        System.out.println("\nBreadth First Traversal starting from vertex 2:");
        g.BFS(2);
    }
}
```

### Advantages
- **Versatile**: Can represent various types of relationships.
- **Efficient Traversal**: Algorithms like DFS and BFS allow efficient traversal and search.

### Disadvantages
- **Complexity**: Can be complex to implement and manage, especially for large graphs.
- **Memory Usage**: Can consume a lot of memory, especially with dense graphs[1](https://jgrapht.org/javadoc/org.jgrapht.core/org/jgrapht/graph/AsUnweightedGraph.html)[2](https://stackoverflow.com/questions/43327156/how-to-represent-a-unweight-directed-graph-and-find-the-shortest-path-java)[3](https://dev.to/wittedtech-by-harshit/the-ultimate-guide-to-graphs-in-java-a-deep-dive-for-developers-of-all-levels-fo1).

Would you like to explore any specific operations or concepts related to unweighted graphs in more detail?

[1](https://jgrapht.org/javadoc/org.jgrapht.core/org/jgrapht/graph/AsUnweightedGraph.html): [AsUnweightedGraph - JGraphT](https://jgrapht.org/javadoc/org.jgrapht.core/org/jgrapht/graph/AsUnweightedGraph.html)
[2](https://stackoverflow.com/questions/43327156/how-to-represent-a-unweight-directed-graph-and-find-the-shortest-path-java): [How to represent a unweight directed graph and find the shortest path? - Stack Overflow](https://stackoverflow.com/questions/43327156/how-to-represent-a-unweight-directed-graph-and-find-the-shortest-path-java)
[3](https://dev.to/wittedtech-by-harshit/the-ultimate-guide-to-graphs-in-java-a-deep-dive-for-developers-of-all-levels-fo1): [The Ultimate Guide to Graphs in Java - DEV Community](https://dev.to/wittedtech-by-harshit/the-ultimate-guide-to-graphs-in-java-a-deep-dive-for-developers-of-all-levels-fo1)

## Hash-Based

Hash-based data structures use hash functions to map keys to specific locations in a data structure, allowing for efficient data retrieval, insertion, and deletion. Here's a detailed look at how hash-based structures work:

### Core Concepts
1. **Hash Function**: A mathematical algorithm that transforms input data (keys) into a fixed-size numerical value, called a hash code. The hash code is used to index into an array, where the actual data is stored.
   - **Deterministic**: The same input will always produce the same hash code.
   - **Uniform Distribution**: Ideally, hash codes should be uniformly distributed to minimize collisions.
   - **Fixed Size**: The output hash code is of a fixed size, regardless of the input size.

2. **Hash Table**: The primary data structure used in hash-based structures. It consists of an array where each index corresponds to a hash code generated by the hash function.

### Key Operations
1. **Insertion**: The hash function is applied to the key to determine the index in the hash table where the value should be stored.
   ```java
   public void put(K key, V value) {
       int index = hash(key);
       table[index] = value;
   }
   ```

2. **Search**: The hash function is applied to the key to determine the index in the hash table where the value is stored.
   ```java
   public V get(K key) {
       int index = hash(key);
       return table[index];
   }
   ```

3. **Deletion**: The hash function is applied to the key to determine the index in the hash table where the value is stored, and the value is removed.
   ```java
   public void remove(K key) {
       int index = hash(key);
       table[index] = null;
   }
   ```

### Handling Collisions
Collisions occur when two different keys produce the same hash code. There are several strategies to handle collisions:

1. **Chaining**: Each index in the hash table points to a linked list of entries that have the same hash code.
   ```java
   class HashTable {
       private LinkedList<Entry>[] table;

       public void put(K key, V value) {
           int index = hash(key);
           if (table[index] == null) {
               table[index] = new LinkedList<>();
           }
           table[index].add(new Entry(key, value));
       }

       public V get(K key) {
           int index = hash(key);
           if (table[index] != null) {
               for (Entry entry : table[index]) {
                   if (entry.key.equals(key)) {
                       return entry.value;
                   }
               }
           }
           return null;
       }
   }
   ```

2. **Open Addressing**: When a collision occurs, the algorithm searches for the next available slot in the hash table.
   - **Linear Probing**: Searches sequentially for the next available slot.
   - **Quadratic Probing**: Searches using a quadratic function to find the next available slot.
   - **Double Hashing**: Uses a second hash function to determine the step size for finding the next available slot.

### Example: HashMap in Java
The `HashMap` class in Java is a widely used hash-based data structure that implements the `Map` interface. It uses an array of linked lists to handle collisions (chaining).

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();

        // Insertion
        map.put("apple", 1);
        map.put("banana", 2);
        map.put("cherry", 3);

        // Search
        System.out.println("Value for 'apple': " + map.get("apple"));

        // Deletion
        map.remove("banana");
        System.out.println("Value for 'banana': " + map.get("banana"));
    }
}
```

### Advantages
- **Efficient Operations**: Provides average-case O(1) time complexity for insertion, search, and deletion.
- **Scalability**: Can handle large datasets efficiently.

### Disadvantages
- **Collisions**: Requires strategies to handle collisions, which can affect performance.
- **Memory Usage**: Can consume more memory due to the need for additional data structures to handle collisions[1](https://www.baeldung.com/cs/hashing)[2](https://www.scholarhat.com/tutorial/datastructures/hashing-in-data-structures)[3](https://www.theknowledgeacademy.com/blog/hashing-in-data-structure/).

Would you like to explore any specific hash-based data structure or concept in more detail?

[1](https://www.baeldung.com/cs/hashing): [Deep Dive into Hashing - Baeldung](https://www.baeldung.com/cs/hashing)
[2](https://www.scholarhat.com/tutorial/datastructures/hashing-in-data-structures): [Hash Function in Data Structure: Types and Functions - ScholarHat](https://www.scholarhat.com/tutorial/datastructures/hashing-in-data-structures)
[3](https://www.theknowledgeacademy.com/blog/hashing-in-data-structure/): [Hashing in Data Structure: Usage, Function, and Examples - The Knowledge Academy](https://www.theknowledgeacademy.com/blog/hashing-in-data-structure/)

## Hash Tables

In Java, a hash table is a data structure that stores key-value pairs and allows for efficient data retrieval, insertion, and deletion. The `Hashtable` class in Java is part of the `java.util` package and implements the `Map` interface. Here's a detailed look at how hash tables work internally:

### Structure
A hash table consists of an array of "buckets" or "slots," where each bucket can store multiple key-value pairs. The position of each key-value pair in the array is determined by a hash function applied to the key.

### Key Components
1. **Hash Function**: A function that takes a key and returns an index in the array. The goal is to distribute keys uniformly across the array to minimize collisions.
   ```java
   int hash(Object key) {
       return key.hashCode() % capacity;
   }
   ```

2. **Buckets**: Each bucket can store multiple key-value pairs. In Java's `Hashtable`, each bucket is typically implemented as a linked list to handle collisions.

### Key Operations
1. **Insertion**: The hash function is applied to the key to determine the index in the array where the key-value pair should be stored. If the bucket at that index is already occupied, the new key-value pair is added to the linked list at that bucket.
   ```java
   public void put(K key, V value) {
       int index = hash(key);
       Entry<K, V> newEntry = new Entry<>(key, value, null);
       if (table[index] == null) {
           table[index] = newEntry;
       } else {
           Entry<K, V> current = table[index];
           while (current.next != null) {
               if (current.key.equals(key)) {
                   current.value = value;
                   return;
               }
               current = current.next;
           }
           current.next = newEntry;
       }
   }
   ```

2. **Search**: The hash function is applied to the key to determine the index in the array where the key-value pair is stored. The linked list at that bucket is then searched for the key.
   ```java
   public V get(Object key) {
       int index = hash(key);
       Entry<K, V> current = table[index];
       while (current != null) {
           if (current.key.equals(key)) {
               return current.value;
           }
           current = current.next;
       }
       return null;
   }
   ```

3. **Deletion**: The hash function is applied to the key to determine the index in the array where the key-value pair is stored. The linked list at that bucket is then searched for the key, and the key-value pair is removed.
   ```java
   public V remove(Object key) {
       int index = hash(key);
       Entry<K, V> current = table[index];
       Entry<K, V> previous = null;
       while (current != null) {
           if (current.key.equals(key)) {
               if (previous == null) {
                   table[index] = current.next;
               } else {
                   previous.next = current.next;
               }
               return current.value;
           }
           previous = current;
           current = current.next;
       }
       return null;
   }
   ```

### Handling Collisions
Collisions occur when two different keys produce the same hash code. In Java's `Hashtable`, collisions are handled using chaining, where each bucket contains a linked list of entries that have the same hash code.

### Example: Hashtable in Java
Here's a simple example demonstrating how to use the `Hashtable` class in Java:

```java
import java.util.Hashtable;

public class HashtableExample {
    public static void main(String[] args) {
        Hashtable<String, Integer> hashtable = new Hashtable<>();

        // Insertion
        hashtable.put("apple", 1);
        hashtable.put("banana", 2);
        hashtable.put("cherry", 3);

        // Search
        System.out.println("Value for 'apple': " + hashtable.get("apple"));

        // Deletion
        hashtable.remove("banana");
        System.out.println("Value for 'banana': " + hashtable.get("banana"));
    }
}
```

### Advantages
- **Efficient Operations**: Provides average-case O(1) time complexity for insertion, search, and deletion.
- **Thread-Safe**: The `Hashtable` class is synchronized, making it thread-safe for concurrent access.

### Disadvantages
- **Synchronization Overhead**: The synchronization can slow down performance in single-threaded environments.
- **No Null Keys or Values**: The `Hashtable` class does not allow null keys or values[1](https://www.javatpoint.com/java-hashtable)[2](https://howtodoinjava.com/java/collections/hashtable-class/)[3](https://www.baeldung.com/java-hash-table).

Would you like to explore any specific operations or concepts related to hash tables in more detail?

[1](https://www.javatpoint.com/java-hashtable): [Java Hashtable Class - Javatpoint](https://www.javatpoint.com/java-hashtable)
[2](https://howtodoinjava.com/java/collections/hashtable-class/): [HashTable in Java - Java Hashtable example - HowToDoInJava](https://howtodoinjava.com/java/collections/hashtable-class/)
[3](https://www.baeldung.com/java-hash-table): [An Introduction to java.util.Hashtable Class - Baeldung](https://www.baeldung.com/java-hash-table)

## Hash Maps

In Java, a `HashMap` is a widely used data structure that stores key-value pairs and allows for efficient data retrieval, insertion, and deletion. Here's a detailed look at how `HashMap` works internally:

### Structure
A `HashMap` consists of an array of "buckets" or "bins," where each bucket can store multiple key-value pairs. The position of each key-value pair in the array is determined by a hash function applied to the key.

### Key Components
1. **Hash Function**: A function that takes a key and returns an index in the array. The goal is to distribute keys uniformly across the array to minimize collisions.
   ```java
   int hash(Object key) {
       return key.hashCode() % capacity;
   }
   ```

2. **Buckets**: Each bucket can store multiple key-value pairs. In Java's `HashMap`, each bucket is typically implemented as a linked list to handle collisions.

### Key Operations
1. **Insertion**: The hash function is applied to the key to determine the index in the array where the key-value pair should be stored. If the bucket at that index is already occupied, the new key-value pair is added to the linked list at that bucket.
   ```java
   public void put(K key, V value) {
       int index = hash(key);
       Node<K, V> newNode = new Node<>(key, value, null);
       if (table[index] == null) {
           table[index] = newNode;
       } else {
           Node<K, V> current = table[index];
           while (current.next != null) {
               if (current.key.equals(key)) {
                   current.value = value;
                   return;
               }
               current = current.next;
           }
           current.next = newNode;
       }
   }
   ```

2. **Search**: The hash function is applied to the key to determine the index in the array where the key-value pair is stored. The linked list at that bucket is then searched for the key.
   ```java
   public V get(Object key) {
       int index = hash(key);
       Node<K, V> current = table[index];
       while (current != null) {
           if (current.key.equals(key)) {
               return current.value;
           }
           current = current.next;
       }
       return null;
   }
   ```

3. **Deletion**: The hash function is applied to the key to determine the index in the array where the key-value pair is stored, and the key-value pair is removed.
   ```java
   public V remove(Object key) {
       int index = hash(key);
       Node<K, V> current = table[index];
       Node<K, V> previous = null;
       while (current != null) {
           if (current.key.equals(key)) {
               if (previous == null) {
                   table[index] = current.next;
               } else {
                   previous.next = current.next;
               }
               return current.value;
           }
           previous = current;
           current = current.next;
       }
       return null;
   }
   ```

### Handling Collisions
Collisions occur when two different keys produce the same hash code. In Java's `HashMap`, collisions are handled using chaining, where each bucket contains a linked list of entries that have the same hash code. Starting from Java 8, if the number of entries in a bucket exceeds a certain threshold (TREEIFY_THRESHOLD, default value 8), the linked list is converted to a balanced tree (Red-Black Tree) to improve performance[1](https://howtodoinjava.com/java/collections/hashmap/how-hashmap-works-in-java/)[2](https://www.freecodecamp.org/news/how-java-hashmaps-work-internal-mechanics-explained/).

### Example: HashMap in Java
Here's a simple example demonstrating how to use the `HashMap` class in Java:

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();

        // Insertion
        map.put("apple", 1);
        map.put("banana", 2);
        map.put("cherry", 3);

        // Search
        System.out.println("Value for 'apple': " + map.get("apple"));

        // Deletion
        map.remove("banana");
        System.out.println("Value for 'banana': " + map.get("banana"));
    }
}
```

### Advantages
- **Efficient Operations**: Provides average-case O(1) time complexity for insertion, search, and deletion.
- **Dynamic Resizing**: Automatically resizes when the load factor exceeds a certain threshold to maintain performance.

### Disadvantages
- **Memory Usage**: Can consume more memory due to the need for additional data structures to handle collisions.
- **No Null Keys or Values**: Unlike `Hashtable`, `HashMap` allows one null key and multiple null values[1](https://howtodoinjava.com/java/collections/hashmap/how-hashmap-works-in-java/)[2](https://www.freecodecamp.org/news/how-java-hashmaps-work-internal-mechanics-explained/)[3](https://www.javatpoint.com/working-of-hashmap-in-java).

Would you like to explore any specific operations or concepts related to `HashMap` in more detail?

[1](https://howtodoinjava.com/java/collections/hashmap/how-hashmap-works-in-java/): [Internal Working of HashMap: How HashMap Works? - HowToDoInJava](https://howtodoinjava.com/java/collections/hashmap/how-hashmap-works-in-java/)
[2](https://www.freecodecamp.org/news/how-java-hashmaps-work-internal-mechanics-explained/): [How Java HashMaps Work – Internal Mechanics Explained - freeCodeCamp.org](https://www.freecodecamp.org/news/how-java-hashmaps-work-internal-mechanics-explained/)
[3](https://www.javatpoint.com/working-of-hashmap-in-java): [Working of HashMap in Java | How HashMap works - javatpoint](https://www.javatpoint.com/working-of-hashmap-in-java)

## Segment Trees

Segment Trees are a powerful data structure used for efficiently solving range queries and updates on arrays. Here's a brief overview of how they work internally in Java:

### Structure of a Segment Tree
1. **Tree Representation**: A Segment Tree is a binary tree where each node represents a segment (or range) of the array. The leaf nodes represent individual elements of the array, while internal nodes represent the sum (or other operations) of their child nodes.
2. **Array Representation**: Segment Trees can be represented using arrays. For an array of size \( n \), the Segment Tree can be represented in an array of size \( 2 \times 2^{\lceil \log_2 n \rceil} - 1 \).

### Building the Segment Tree
1. **Initialization**: Start by initializing an array to store the Segment Tree.
2. **Recursive Construction**: Build the tree recursively. The root node represents the entire array, and each internal node represents a segment of the array. The left child of a node at index \( i \) is at \( 2i + 1 \) and the right child is at \( 2i + 2 \).

### Operations on Segment Tree
1. **Range Query**: To find the sum (or other operations) of elements in a given range, traverse the tree from the root, checking if the current segment overlaps with the query range. If it does, combine the results from the left and right children.
2. **Update**: To update an element, find the corresponding leaf node and update its value. Then, propagate the changes up the tree by updating the values of the internal nodes.

### Example Code in Java
Here's a simple implementation of a Segment Tree in Java:

```java
class SegmentTree {
    int[] tree;
    int n;

    public SegmentTree(int[] arr) {
        n = arr.length;
        tree = new int[2 * n];
        buildTree(arr);
    }

    private void buildTree(int[] arr) {
        for (int i = 0; i < n; i++) {
            tree[n + i] = arr[i];
        }
        for (int i = n - 1; i > 0; --i) {
            tree[i] = tree[2 * i] + tree[2 * i + 1];
        }
    }

    public void update(int pos, int value) {
        pos += n;
        tree[pos] = value;
        while (pos > 1) {
            pos /= 2;
            tree[pos] = tree[2 * pos] + tree[2 * pos + 1];
        }
    }

    public int query(int left, int right) {
        left += n;
        right += n;
        int sum = 0;
        while (left < right) {
            if ((left & 1) == 1) {
                sum += tree[left++];
            }
            if ((right & 1) == 1) {
                sum += tree[--right];
            }
            left /= 2;
            right /= 2;
        }
        return sum;
    }
}
```

This code demonstrates how to build a Segment Tree, update an element, and perform a range query. Segment Trees are highly efficient, with both update and query operations having a time complexity of \( O(\log n) \)[1](https://www.javatpoint.com/segment-tree-in-java)[2](https://www.wscubetech.com/resources/dsa/segment-tree).

If you have any specific questions or need further details, feel free to ask!

## Fenwick Trees (Binary Indexed Trees)

Fenwick Trees, also known as Binary Indexed Trees (BIT), are a data structure that efficiently supports range queries and updates. Here's a breakdown of how they work internally in Java:

### Structure of a Fenwick Tree
1. **Tree Representation**: A Fenwick Tree is represented as an array where each element at index \( i \) stores the cumulative frequency or sum of elements up to that index.
2. **Indexing**: The key idea is to use the binary representation of indices to determine the range of elements each node covers.

### Operations on Fenwick Tree
1. **Update Operation**: To update an element, you need to update all the relevant nodes that include this element in their range.
2. **Query Operation**: To get the sum of elements up to a given index, you sum the values of all relevant nodes that contribute to this range.

### Example Code in Java
Here's a simple implementation of a Fenwick Tree in Java:

```java
class FenwickTree {
    private int[] tree;
    private int n;

    public FenwickTree(int size) {
        this.n = size;
        this.tree = new int[n + 1];
    }

    // Update the Fenwick Tree with value at position index
    public void update(int index, int value) {
        while (index <= n) {
            tree[index] += value;
            index += index & -index;
        }
    }

    // Query the sum of the range [1, index]
    public int query(int index) {
        int sum = 0;
        while (index > 0) {
            sum += tree[index];
            index -= index & -index;
        }
        return sum;
    }

    // Query the sum of the range [left, right]
    public int rangeQuery(int left, int right) {
        return query(right) - query(left - 1);
    }
}
```

### Explanation
1. **Update Operation**: The `update` method adds a value to the element at the given index and updates all relevant nodes. The expression `index += index & -index` moves to the next node that includes the current index in its range.
2. **Query Operation**: The `query` method calculates the sum of elements up to the given index by summing the values of all relevant nodes. The expression `index -= index & -index` moves to the parent node.

### Usage
- **Initialization**: Create an instance of `FenwickTree` with the size of the array.
- **Update**: Use the `update` method to add a value to an element.
- **Query**: Use the `query` method to get the sum of elements up to a given index or `rangeQuery` for a specific range.

Fenwick Trees are highly efficient, with both update and query operations having a time complexity of \( O(\log n) \)[1](https://www.baeldung.com/cs/fenwick-tree)[2](https://www.wscubetech.com/resources/dsa/fenwick-tree).

If you have any specific questions or need further details, feel free to ask!

# How Disjoint Set Union (Union-Find) works internally in Java

Disjoint Set Union, also known as Union-Find, is a data structure that efficiently handles the union and find operations on disjoint sets. Here's a detailed explanation of how it works internally in Java:

### Structure of Disjoint Set Union
1. **Parent Array**: Each element points to its parent, and a root element points to itself.
2. **Rank Array**: This helps in keeping the tree flat by attaching the smaller tree under the root of the larger tree.

### Operations on Disjoint Set Union
1. **Find Operation**: Determines the root of the set containing a particular element. This operation uses path compression to make future queries faster.
2. **Union Operation**: Merges two sets into one. This operation uses union by rank to keep the tree flat.

### Example Code in Java
Here's a simple implementation of Disjoint Set Union in Java:

```java
class DisjointSetUnion {
    private int[] parent;
    private int[] rank;

    public DisjointSetUnion(int size) {
        parent = new int[size];
        rank = new int[size];
        for (int i = 0; i < size; i++) {
            parent[i] = i;
            rank[i] = 0;
        }
    }

    // Find the root of the set containing element x
    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]); // Path compression
        }
        return parent[x];
    }

    // Union of two sets containing elements x and y
    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
}
```

### Explanation
1. **Initialization**: The `parent` array is initialized such that each element is its own parent, and the `rank` array is initialized to zero.
2. **Find Operation**: The `find` method uses path compression to make the tree flatter, which speeds up future operations.
3. **Union Operation**: The `union` method uses union by rank to attach the smaller tree under the root of the larger tree, ensuring the tree remains balanced.

### Usage
- **Initialization**: Create an instance of `DisjointSetUnion` with the size of the set.
- **Union**: Use the `union` method to merge two sets.
- **Find**: Use the `find` method to determine the root of the set containing a particular element.

Disjoint Set Union is highly efficient, with both union and find operations having an average time complexity of \( O(\log n) \) due to path compression and union by rank[1](https://www.javatpoint.com/disjoint-set-data-structure)[2](https://automationtestlab.com/disjoint-sets-in-java/).

If you have any specific questions or need further details, feel free to ask!

## Multimaps

Multimaps in Java are a type of data structure that allows a single key to be associated with multiple values, unlike traditional maps where each key is associated with a single value. Java does not have a built-in Multimap implementation, but you can use libraries like Google's Guava or Apache Commons Collections to achieve this functionality.

### Structure of a Multimap
1. **Key-Value Mapping**: In a Multimap, each key can map to multiple values. This is similar to having a `Map<K, Collection<V>>`, where each key maps to a collection of values.
2. **Implementation**: Common implementations include `ArrayListMultimap`, `HashMultimap`, `LinkedListMultimap`, and `TreeMultimap` from the Guava library.

### Operations on Multimap
1. **Put Operation**: Adds a key-value pair to the multimap. If the key already exists, the value is added to the collection of values for that key.
2. **Get Operation**: Retrieves the collection of values associated with a key.
3. **Remove Operation**: Removes a specific key-value pair or all values associated with a key.

### Example Code in Java using Guava
Here's a simple implementation of a Multimap using the Guava library:

```java
import com.google.common.collect.ArrayListMultimap;
import com.google.common.collect.Multimap;

public class MultimapExample {
    public static void main(String[] args) {
        Multimap<String, String> multimap = ArrayListMultimap.create();

        // Adding key-value pairs
        multimap.put("a", "Andrew");
        multimap.put("b", "Albert");
        multimap.put("b", "Tom");
        multimap.put("d", "Sam");
        multimap.put("d", "Reo");
        multimap.put("g", "Jack");
        multimap.put("g", "David");

        // Retrieving values
        System.out.println("Values for key 'b': " + multimap.get("b"));

        // Removing a key-value pair
        multimap.remove("b", "Tom");
        System.out.println("Values for key 'b' after removal: " + multimap.get("b"));
    }
}
```

### Explanation
1. **Initialization**: The `ArrayListMultimap.create()` method creates a new instance of a Multimap.
2. **Put Operation**: The `put` method adds key-value pairs to the multimap.
3. **Get Operation**: The `get` method retrieves the collection of values associated with a key.
4. **Remove Operation**: The `remove` method removes a specific key-value pair from the multimap.

### Custom Implementation
If you prefer not to use external libraries, you can implement your own Multimap using a `Map<K, Collection<V>>`:

```java
import java.util.*;

public class CustomMultimap<K, V> {
    private Map<K, Collection<V>> map = new HashMap<>();

    public void put(K key, V value) {
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(value);
    }

    public Collection<V> get(K key) {
        return map.getOrDefault(key, Collections.emptyList());
    }

    public void remove(K key, V value) {
        Collection<V> values = map.get(key);
        if (values != null) {
            values.remove(value);
            if (values.isEmpty()) {
                map.remove(key);
            }
        }
    }

    public static void main(String[] args) {
        CustomMultimap<String, String> multimap = new CustomMultimap<>();

        // Adding key-value pairs
        multimap.put("a", "Andrew");
        multimap.put("b", "Albert");
        multimap.put("b", "Tom");
        multimap.put("d", "Sam");
        multimap.put("d", "Reo");
        multimap.put("g", "Jack");
        multimap.put("g", "David");

        // Retrieving values
        System.out.println("Values for key 'b': " + multimap.get("b"));

        // Removing a key-value pair
        multimap.remove("b", "Tom");
        System.out.println("Values for key 'b' after removal: " + multimap.get("b"));
    }
}
```

This custom implementation uses a `HashMap` to store the keys and an `ArrayList` to store the values for each key.

Multimaps are useful in scenarios where you need to associate multiple values with a single key, such as in database indexing or grouping data[1](https://www.javatpoint.com/java-8-multimap)[2](https://redisson.org/glossary/java-multimap.html).

If you have any specific questions or need further details, feel free to ask!

## Multisets (Bags)

Multisets, also known as Bags, are a type of collection that allows duplicate elements. Unlike a standard Set, which only allows unique elements, a Multiset can store multiple occurrences of the same element. Java does not have a built-in Multiset implementation, but you can use libraries like Google's Guava or Apache Commons Collections to achieve this functionality.

### Structure of a Multiset
1. **Element Storage**: A Multiset stores elements along with their counts. This can be implemented using a `Map<E, Integer>`, where the key is the element and the value is the count of that element.
2. **Count Management**: The count of each element is managed internally, allowing for efficient addition, removal, and querying of elements.

### Operations on Multiset
1. **Add Operation**: Adds an element to the multiset and increments its count.
2. **Remove Operation**: Removes an element from the multiset and decrements its count.
3. **Count Operation**: Retrieves the count of a specific element in the multiset.

### Example Code in Java using Guava
Here's a simple implementation of a Multiset using the Guava library:

```java
import com.google.common.collect.HashMultiset;
import com.google.common.collect.Multiset;

public class MultisetExample {
    public static void main(String[] args) {
        Multiset<String> multiset = HashMultiset.create();

        // Adding elements
        multiset.add("apple");
        multiset.add("banana");
        multiset.add("apple");
        multiset.add("orange");
        multiset.add("banana");
        multiset.add("apple");

        // Retrieving counts
        System.out.println("Count of 'apple': " + multiset.count("apple"));
        System.out.println("Count of 'banana': " + multiset.count("banana"));
        System.out.println("Count of 'orange': " + multiset.count("orange"));

        // Removing elements
        multiset.remove("apple");
        System.out.println("Count of 'apple' after removal: " + multiset.count("apple"));
    }
}
```

### Explanation
1. **Initialization**: The `HashMultiset.create()` method creates a new instance of a Multiset.
2. **Add Operation**: The `add` method adds elements to the multiset and increments their counts.
3. **Count Operation**: The `count` method retrieves the count of a specific element.
4. **Remove Operation**: The `remove` method removes an element from the multiset and decrements its count.

### Custom Implementation
If you prefer not to use external libraries, you can implement your own Multiset using a `HashMap`:

```java
import java.util.HashMap;
import java.util.Map;

public class CustomMultiset<E> {
    private Map<E, Integer> map = new HashMap<>();

    public void add(E element) {
        map.put(element, map.getOrDefault(element, 0) + 1);
    }

    public void remove(E element) {
        if (map.containsKey(element)) {
            if (map.get(element) > 1) {
                map.put(element, map.get(element) - 1);
            } else {
                map.remove(element);
            }
        }
    }

    public int count(E element) {
        return map.getOrDefault(element, 0);
    }

    public static void main(String[] args) {
        CustomMultiset<String> multiset = new CustomMultiset<>();

        // Adding elements
        multiset.add("apple");
        multiset.add("banana");
        multiset.add("apple");
        multiset.add("orange");
        multiset.add("banana");
        multiset.add("apple");

        // Retrieving counts
        System.out.println("Count of 'apple': " + multiset.count("apple"));
        System.out.println("Count of 'banana': " + multiset.count("banana"));
        System.out.println("Count of 'orange': " + multiset.count("orange"));

        // Removing elements
        multiset.remove("apple");
        System.out.println("Count of 'apple' after removal: " + multiset.count("apple"));
    }
}
```

This custom implementation uses a `HashMap` to store elements and their counts, providing a simple and efficient way to manage a Multiset.

Multisets are useful in scenarios where you need to count occurrences of elements, such as in frequency analysis or inventory management[1](https://www.techiedelight.com/multiset-implementation-java/)[2](https://jminded.com/bag-multiset-implementation-with-linkedlist-in-java/).

If you have any specific questions or need further details, feel free to ask!

## Fibonacci Heap

A Fibonacci heap is a data structure used for priority queue operations, consisting of a collection of heap-ordered trees. It was invented by Michael L. Fredman and Robert E. Tarjan in 1984 and is named after the Fibonacci numbers, which are used in its running time analysis[1](https://en.wikipedia.org/wiki/Fibonacci_heap)[2](https://www.programiz.com/dsa/fibonacci-heap).

### Key Properties
1. **Heap-Ordered Trees**: The trees in a Fibonacci heap follow the min-heap or max-heap property, meaning the key of a child is always greater than or equal to the key of the parent.
2. **Flexible Structure**: Unlike binomial heaps, Fibonacci heaps do not have a rigid structure. This flexibility allows some operations to be executed lazily, postponing work for later operations.
3. **Amortized Time Complexity**: Fibonacci heaps have better amortized running times for many operations compared to other heap data structures. For example:
   - **Insert**: \( O(1) \)
   - **Find-Min**: \( O(1) \)
   - **Delete-Min**: \( O(\log n) \)
   - **Decrease-Key**: \( O(1) \)
   - **Merge**: \( O(1) \)

### Operations
1. **Insertion**: Adding a new node to the heap is done in constant time by simply adding it to the root list.
2. **Find-Min**: The minimum element is always at the root of one of the trees, so it can be found in constant time.
3. **Union**: Merging two Fibonacci heaps is done by concatenating their root lists, which takes constant time.
4. **Extract-Min**: Removing the minimum element involves removing the root of the tree containing the minimum element and then consolidating the trees to maintain the heap properties.
5. **Decrease-Key**: Decreasing the key of a node may involve cutting the node from its parent and adding it to the root list, followed by a cascading cut if necessary.
6. **Delete**: Deleting a node is done by decreasing its key to negative infinity and then performing an extract-min operation.

### Example Structure
A Fibonacci heap is a collection of trees where each tree is a min-heap. The roots of all trees are linked together in a circular doubly linked list for efficient access. The child nodes of a parent node are also connected in a circular doubly linked list[1](https://en.wikipedia.org/wiki/Fibonacci_heap)[2](https://www.programiz.com/dsa/fibonacci-heap).

### Advantages
- **Efficient Amortized Time**: Many operations have very efficient amortized time complexities, making Fibonacci heaps suitable for algorithms that require frequent priority queue operations, such as Dijkstra's and Prim's algorithms.
- **Lazy Operations**: Some operations are performed lazily, which can lead to better performance in practice.

Fibonacci heaps are particularly useful in scenarios where the decrease-key operation is frequently used, as they offer a significant performance improvement over other heap data structures[1](https://en.wikipedia.org/wiki/Fibonacci_heap)[2](https://www.programiz.com/dsa/fibonacci-heap).

If you have any specific questions or need further details, feel free to ask!

## Design a O(1) All one

Designing a data structure that supports O(1) operations for insertion, deletion, and access can be quite challenging but is achievable with the right approach. One well-known example is the **All O`one Data Structure**, which supports the following operations in constant time:

1. **Insert**: Insert a new key with a value.
2. **Delete**: Remove a key.
3. **GetMaxKey**: Retrieve the key with the maximum value.
4. **GetMinKey**: Retrieve the key with the minimum value.

### Design Overview
To achieve O(1) time complexity for these operations, we can use a combination of a **HashMap** and a **Doubly Linked List**.

1. **HashMap**: This will store the keys and their corresponding nodes in the doubly linked list.
2. **Doubly Linked List**: This will store the keys grouped by their values, allowing us to quickly access the keys with the maximum and minimum values.

### Detailed Design
1. **Node Structure**: Each node in the doubly linked list will represent a unique value and store a set of keys with that value.
2. **HashMap Structure**: The HashMap will map each key to its corresponding node in the doubly linked list.

### Example Code in Java

Here's a simplified implementation of the All O`one Data Structure in Java:

```java
import java.util.*;

class AllOne {
    private class Node {
        int value;
        Set<String> keys;
        Node prev, next;

        Node(int value) {
            this.value = value;
            this.keys = new HashSet<>();
        }
    }

    private Map<String, Node> keyNodeMap;
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
            if (node.next.value != node.value + 1) {
                Node newNode = new Node(node.value + 1);
                insertNodeAfter(node, newNode);
            }
            node.next.keys.add(key);
            keyNodeMap.put(key, node.next);
            if (node.keys.isEmpty()) removeNode(node);
        } else {
            if (head.next.value != 1) {
                Node newNode = new Node(1);
                insertNodeAfter(head, newNode);
            }
            head.next.keys.add(key);
            keyNodeMap.put(key, head.next);
        }
    }

    public void dec(String key) {
        if (!keyNodeMap.containsKey(key)) return;
        Node node = keyNodeMap.get(key);
        node.keys.remove(key);
        if (node.value > 1) {
            if (node.prev.value != node.value - 1) {
                Node newNode = new Node(node.value - 1);
                insertNodeAfter(node.prev, newNode);
            }
            node.prev.keys.add(key);
            keyNodeMap.put(key, node.prev);
        } else {
            keyNodeMap.remove(key);
        }
        if (node.keys.isEmpty()) removeNode(node);
    }

    public String getMaxKey() {
        return tail.prev == head ? "" : tail.prev.keys.iterator().next();
    }

    public String getMinKey() {
        return head.next == tail ? "" : head.next.keys.iterator().next();
    }

    private void insertNodeAfter(Node prevNode, Node newNode) {
        newNode.prev = prevNode;
        newNode.next = prevNode.next;
        prevNode.next.prev = newNode;
        prevNode.next = newNode;
    }

    private void removeNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
}
```

### Explanation
1. **Initialization**: The `AllOne` class initializes the HashMap and the doubly linked list with dummy head and tail nodes.
2. **Increment Operation**: The `inc` method increases the value of a key. If the key does not exist, it is added with a value of 1. If it exists, it is moved to the next node with an incremented value.
3. **Decrement Operation**: The `dec` method decreases the value of a key. If the key's value becomes 0, it is removed from the data structure.
4. **GetMaxKey and GetMinKey Operations**: These methods return the keys with the maximum and minimum values, respectively, by accessing the tail and head of the doubly linked list.

This design ensures that all operations are performed in constant time, making it highly efficient for scenarios where frequent updates and queries are required[1](https://algo.monster/liteproblems/432)[2](https://iq.opengenus.org/all-oone-data-structure/)[3](https://iq.opengenus.org/design-data-structure-random-get/).

If you have any specific questions or need further details, feel free to ask!

# Sorting Algorithms

Sure! Here is a list of some common sorting algorithms, along with a brief description of each:

### Comparison-Based Sorting Algorithms
1. **Bubble Sort**: Repeatedly swaps adjacent elements if they are in the wrong order. Simple but inefficient for large datasets.
2. **Selection Sort**: Selects the smallest (or largest) element from the unsorted portion and swaps it with the first unsorted element.
3. **Insertion Sort**: Builds the sorted array one element at a time by repeatedly inserting the next element into the correct position.
4. **Merge Sort**: Divides the array into halves, recursively sorts them, and then merges the sorted halves. Efficient with a time complexity of \(O(n \log n)\).
5. **Quick Sort**: Divides the array into two parts based on a pivot element, recursively sorts the parts, and combines them. Average time complexity is \(O(n \log n)\).
6. **Heap Sort**: Converts the array into a heap data structure, then repeatedly extracts the maximum element and rebuilds the heap. Time complexity is \(O(n \log n)\).
7. **Shell Sort**: Generalization of insertion sort that allows the exchange of far-apart elements. Time complexity varies based on the gap sequence used.

### Non-Comparison-Based Sorting Algorithms
1. **Counting Sort**: Counts the occurrences of each element and uses this information to place elements in the correct position. Efficient for small range of integers.
2. **Radix Sort**: Sorts numbers digit by digit, starting from the least significant digit to the most significant digit. Often used with counting sort as a subroutine.
3. **Bucket Sort**: Divides the array into a number of buckets, sorts each bucket individually, and then concatenates the sorted buckets. Useful when input is uniformly distributed.

### Other Sorting Algorithms
1. **Cocktail Shaker Sort**: A variation of bubble sort that sorts in both directions on each pass through the list.
2. **Comb Sort**: An improvement over bubble sort that eliminates turtles, or small values near the end of the list, by using a gap sequence.
3. **Gnome Sort**: Similar to insertion sort but uses a different method to move elements to their correct position.
4. **Odd-Even Sort**: A parallel version of bubble sort that compares and swaps adjacent elements in alternating phases.

These algorithms cover a wide range of use cases and performance characteristics[1](https://en.wikipedia.org/wiki/Sorting_algorithm)[2](https://www.wscubetech.com/resources/dsa/sorting-algorithms).

Would you like more details on any specific sorting algorithm?
[1](https://en.wikipedia.org/wiki/Sorting_algorithm): [1](https://en.wikipedia.org/wiki/Sorting_algorithm)
[2](https://www.wscubetech.com/resources/dsa/sorting-algorithms): [2](https://www.wscubetech.com/resources/dsa/sorting-algorithms)

## Bubble Sort

Sure! Bubble Sort is one of the simplest sorting algorithms. It works by repeatedly stepping through the list, comparing adjacent elements, and swapping them if they are in the wrong order. This process is repeated until the list is sorted. Here's how you can implement Bubble Sort in Java:

### Bubble Sort Implementation in Java

```java
public class BubbleSort {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap arr[j] and arr[j + 1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Array before Bubble Sort:");
        System.out.println(Arrays.toString(arr));

        bubbleSort(arr);

        System.out.println("Array after Bubble Sort:");
        System.out.println(Arrays.toString(arr));
    }
}
```

### How It Works
1. **Outer Loop**: Runs from the start of the array to the second last element.
2. **Inner Loop**: Runs from the start of the array to the last unsorted element.
3. **Comparison and Swap**: Compares each pair of adjacent elements and swaps them if they are in the wrong order.

### Complexity Analysis
- **Time Complexity**: \(O(n^2)\) in the worst and average cases, where \(n\) is the number of elements in the array. This is because each element is compared with every other element.
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- Simple to understand and implement.
- Does not require additional memory space.

### Disadvantages
- Inefficient for large datasets due to its high time complexity.
- Not suitable for performance-critical applications.

Bubble Sort is often used for educational purposes to help understand the basics of sorting algorithms[1](https://www.javatpoint.com/bubble-sort-in-java)[2](https://javacodepoint.com/logical-programs/bubble-sort-in-java/).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/bubble-sort-in-java): [1](https://www.javatpoint.com/bubble-sort-in-java)
[2](https://javacodepoint.com/logical-programs/bubble-sort-in-java/): [2](https://javacodepoint.com/logical-programs/bubble-sort-in-java/)


## Selection Sort

Sure! Selection Sort is a simple comparison-based sorting algorithm. It works by dividing the array into a sorted and an unsorted part. The algorithm repeatedly selects the smallest (or largest, depending on sorting order) element from the unsorted part and moves it to the end of the sorted part. Here's how you can implement Selection Sort in Java:

### Selection Sort Implementation in Java

```java
public class SelectionSort {
    public static void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            // Find the minimum element in the unsorted part
            int minIdx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }
            // Swap the found minimum element with the first element of the unsorted part
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
        }
    }

    public static void main(String[] args) {
        int[] arr = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Original array:");
        System.out.println(Arrays.toString(arr));

        selectionSort(arr);

        System.out.println("Sorted array:");
        System.out.println(Arrays.toString(arr));
    }
}
```

### How It Works
1. **Outer Loop**: Runs from the start of the array to the second last element.
2. **Inner Loop**: Finds the minimum element in the unsorted part of the array.
3. **Swap**: Swaps the found minimum element with the first element of the unsorted part.

### Complexity Analysis
- **Time Complexity**: \(O(n^2)\) in the worst, average, and best cases, where \(n\) is the number of elements in the array. This is because each element is compared with every other element.
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- Simple to understand and implement.
- Does not require additional memory space.

### Disadvantages
- Inefficient for large datasets due to its high time complexity.
- Not suitable for performance-critical applications.

Selection Sort is often used for educational purposes to help understand the basics of sorting algorithms[1](https://www.javatpoint.com/selection-sort-in-java)[2](https://javacodepoint.com/logical-programs/selection-sort-in-java/).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/selection-sort-in-java): [1](https://www.javatpoint.com/selection-sort-in-java)
[2](https://javacodepoint.com/logical-programs/selection-sort-in-java/): [2](https://javacodepoint.com/logical-programs/selection-sort-in-java/)

## Insertion Sort

Sure! Insertion Sort is a simple and efficient comparison-based sorting algorithm that works similarly to how you might sort playing cards in your hands. It builds the sorted array one element at a time by placing each new element into its correct position within the already sorted part of the array. Here's how you can implement Insertion Sort in Java:

### Insertion Sort Implementation in Java

```java
public class InsertionSort {
    public static void insertionSort(int[] array) {
        int n = array.length;
        for (int i = 1; i < n; i++) {
            int key = array[i];
            int j = i - 1;
            // Shift elements of the sorted part to the right to make space for the key
            while (j >= 0 && array[j] > key) {
                array[j + 1] = array[j];
                j--;
            }
            // Place the key in its correct position
            array[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        int[] numbers = {12, 11, 13, 5, 6};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(numbers));

        insertionSort(numbers);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(numbers));
    }
}
```

### How It Works
1. **Outer Loop**: Starts from the second element (index 1) and iterates through the array.
2. **Inner Loop**: Compares the current element (key) with the elements in the sorted portion of the array (from right to left) and shifts elements to the right to make space for the key.
3. **Insertion**: Places the key in its correct position within the sorted portion.

### Complexity Analysis
- **Time Complexity**:
   - Best Case (nearly sorted array): \(O(n)\)
   - Average Case: \(O(n^2)\)
   - Worst Case (reverse sorted array): \(O(n^2)\)
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- Simple to understand and implement.
- Efficient for small datasets and nearly sorted arrays.
- Adaptive: Performs well on partially sorted arrays.

### Disadvantages
- Inefficient for large datasets due to its high time complexity.
- Not suitable for performance-critical applications.

Insertion Sort is often used for educational purposes and in scenarios where the dataset is small or nearly sorted[1](https://www.javatpoint.com/insertion-sort-in-java)[2](https://javacodepoint.com/logical-programs/insertion-sort-in-java/).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/insertion-sort-in-java): [1](https://www.javatpoint.com/insertion-sort-in-java)
[2](https://javacodepoint.com/logical-programs/insertion-sort-in-java/): [2](https://javacodepoint.com/logical-programs/insertion-sort-in-java/)

## Merge Sort

Sure! Merge Sort is an efficient, stable, comparison-based sorting algorithm that follows the divide-and-conquer paradigm. It works by recursively dividing the array into two halves, sorting each half, and then merging the sorted halves to produce the final sorted array. Here's how you can implement Merge Sort in Java:

### Merge Sort Implementation in Java

```java
public class MergeSort {
    public static void mergeSort(int[] array, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            mergeSort(array, left, mid);
            mergeSort(array, mid + 1, right);
            merge(array, left, mid, right);
        }
    }

    private static void merge(int[] array, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] leftArray = new int[n1];
        int[] rightArray = new int[n2];

        for (int i = 0; i < n1; i++) {
            leftArray[i] = array[left + i];
        }
        for (int i = 0; i < n2; i++) {
            rightArray[i] = array[mid + 1 + i];
        }

        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (leftArray[i] <= rightArray[j]) {
                array[k] = leftArray[i];
                i++;
            } else {
                array[k] = rightArray[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            array[k] = leftArray[i];
            i++;
            k++;
        }

        while (j < n2) {
            array[k] = rightArray[j];
            j++;
            k++;
        }
    }

    public static void main(String[] args) {
        int[] array = {12, 11, 13, 5, 6, 7};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        mergeSort(array, 0, array.length - 1);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Divide**: Recursively divide the array into two halves until each subarray contains a single element.
2. **Conquer**: Sort each subarray.
3. **Combine**: Merge the sorted subarrays to produce the final sorted array.

### Complexity Analysis
- **Time Complexity**: \(O(n \log n)\) for all cases (worst, average, and best).
- **Space Complexity**: \(O(n)\) due to the temporary arrays used for merging.

### Advantages
- Stable sort: Maintains the relative order of equal elements.
- Predictable time complexity: Always \(O(n \log n)\).

### Disadvantages
- Requires additional memory space proportional to the size of the array.
- Not as fast as some other algorithms (like Quick Sort) for small datasets.

Merge Sort is often used in scenarios where stability is important and predictable performance is required[1](https://www.baeldung.com/java-merge-sort)[2](https://www.programiz.com/java-programming/examples/merge-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.baeldung.com/java-merge-sort): [1](https://www.baeldung.com/java-merge-sort)
[2](https://www.programiz.com/java-programming/examples/merge-sort): [2](https://www.programiz.com/java-programming/examples/merge-sort)


## Quick Sort

Sure! Quick Sort is an efficient, comparison-based sorting algorithm that follows the divide-and-conquer paradigm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively. Here's how you can implement Quick Sort in Java:

### Quick Sort Implementation in Java

```java
public class QuickSort {
    // Method to find the partition position
    static int partition(int[] array, int low, int high) {
        int pivot = array[high]; // Choose the rightmost element as pivot
        int i = (low - 1); // Pointer for the greater element

        for (int j = low; j < high; j++) {
            if (array[j] <= pivot) {
                i++;
                // Swap elements at i and j
                int temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }
        }

        // Swap the pivot element with the greater element at i
        int temp = array[i + 1];
        array[i + 1] = array[high];
        array[high] = temp;

        return i + 1; // Return the partition point
    }

    // Main method to implement Quick Sort
    static void quickSort(int[] array, int low, int high) {
        if (low < high) {
            // Find the pivot element such that elements smaller than pivot are on the left
            // and elements greater than pivot are on the right
            int pi = partition(array, low, high);

            // Recursively sort the elements before and after partition
            quickSort(array, low, pi - 1);
            quickSort(array, pi + 1, high);
        }
    }

    public static void main(String[] args) {
        int[] data = {8, 7, 2, 1, 0, 9, 6};
        System.out.println("Unsorted Array:");
        System.out.println(Arrays.toString(data));

        int size = data.length;
        quickSort(data, 0, size - 1);

        System.out.println("Sorted Array in Ascending Order:");
        System.out.println(Arrays.toString(data));
    }
}
```

### How It Works
1. **Partitioning**: The array is partitioned into two parts based on the pivot element. Elements less than the pivot go to the left, and elements greater than the pivot go to the right.
2. **Recursive Sorting**: The left and right sub-arrays are recursively sorted.
3. **Combining**: The sorted sub-arrays are combined to form the final sorted array.

### Complexity Analysis
- **Time Complexity**:
   - Best Case: \(O(n \log n)\)
   - Average Case: \(O(n \log n)\)
   - Worst Case: \(O(n^2)\) (when the smallest or largest element is always chosen as the pivot)
- **Space Complexity**: \(O(\log n)\) due to the recursion stack.

### Advantages
- Efficient for large datasets.
- In-place sorting algorithm (requires only a small, constant amount of extra storage space).

### Disadvantages
- Worst-case time complexity can be \(O(n^2)\), but this can be mitigated by using randomized or median-of-three pivot selection.

Quick Sort is widely used due to its efficiency and simplicity[1](https://www.javatpoint.com/quick-sort)[2](https://www.programiz.com/java-programming/examples/quick-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/quick-sort): [1](https://www.javatpoint.com/quick-sort)
[2](https://www.programiz.com/java-programming/examples/quick-sort): [2](https://www.programiz.com/java-programming/examples/quick-sort)

## Heap Sort

Sure! Heap Sort is an efficient, comparison-based sorting algorithm that uses a binary heap data structure. It works by building a heap from the input data and then repeatedly extracting the maximum element from the heap and rebuilding the heap. Here's how you can implement Heap Sort in Java:

### Heap Sort Implementation in Java

```java
public class HeapSort {
    public void heapSort(int[] array) {
        int n = array.length;

        // Build max heap
        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(array, n, i);
        }

        // Extract elements from heap one by one
        for (int i = n - 1; i > 0; i--) {
            // Move current root to end
            int temp = array[0];
            array[0] = array[i];
            array[i] = temp;

            // Call max heapify on the reduced heap
            heapify(array, i, 0);
        }
    }

    // To heapify a subtree rooted with node i which is an index in array[]
    private void heapify(int[] array, int n, int i) {
        int largest = i; // Initialize largest as root
        int left = 2 * i + 1; // left child
        int right = 2 * i + 2; // right child

        // If left child is larger than root
        if (left < n && array[left] > array[largest]) {
            largest = left;
        }

        // If right child is larger than largest so far
        if (right < n && array[right] > array[largest]) {
            largest = right;
        }

        // If largest is not root
        if (largest != i) {
            int swap = array[i];
            array[i] = array[largest];
            array[largest] = swap;

            // Recursively heapify the affected sub-tree
            heapify(array, n, largest);
        }
    }

    public static void main(String[] args) {
        int[] array = {12, 11, 13, 5, 6, 7};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        HeapSort sorter = new HeapSort();
        sorter.heapSort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Build Max Heap**: Convert the array into a max heap, where the largest element is at the root.
2. **Heap Sort**: Repeatedly extract the maximum element from the heap and rebuild the heap with the remaining elements.

### Complexity Analysis
- **Time Complexity**: \(O(n \log n)\) for all cases (worst, average, and best).
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- Efficient for large datasets.
- In-place sorting algorithm (requires only a small, constant amount of extra storage space).

### Disadvantages
- Not a stable sort: Does not maintain the relative order of equal elements.

Heap Sort is often used in scenarios where a stable sort is not required and predictable performance is needed[1](https://www.javatpoint.com/heap-sort)[2](https://www.baeldung.com/java-heap-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/heap-sort): [1](https://www.javatpoint.com/heap-sort)
[2](https://www.baeldung.com/java-heap-sort): [2](https://www.baeldung.com/java-heap-sort)

## Shell Sort

Sure! Shell Sort is an efficient comparison-based sorting algorithm that generalizes Insertion Sort to allow the exchange of items that are far apart. The idea is to arrange the list of elements so that, starting anywhere, taking every \(k\)th element produces a sorted list. Here's how you can implement Shell Sort in Java:

### Shell Sort Implementation in Java

```java
public class ShellSort {
    public static void shellSort(int[] array) {
        int n = array.length;

        // Start with a big gap, then reduce the gap
        for (int gap = n / 2; gap > 0; gap /= 2) {
            // Do a gapped insertion sort for this gap size
            for (int i = gap; i < n; i++) {
                int key = array[i];
                int j = i;
                // Shift earlier gap-sorted elements up until the correct location for array[i] is found
                while (j >= gap && array[j - gap] > key) {
                    array[j] = array[j - gap];
                    j -= gap;
                }
                // Put key (the original array[i]) in its correct location
                array[j] = key;
            }
        }
    }

    public static void main(String[] args) {
        int[] array = {12, 34, 54, 2, 3};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        shellSort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Gap Sequence**: Start with a large gap and reduce the gap by half in each iteration.
2. **Gapped Insertion Sort**: Perform insertion sort for elements that are `gap` distance apart.
3. **Reduce Gap**: Continue reducing the gap until it becomes 1, at which point the array is fully sorted.

### Complexity Analysis
- **Time Complexity**: The time complexity of Shell Sort depends on the gap sequence. The worst-case time complexity is \(O(n^2)\), but with a good gap sequence, it can be as low as \(O(n \log^2 n)\).
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- More efficient than Insertion Sort for large arrays.
- In-place sorting algorithm (requires only a small, constant amount of extra storage space).

### Disadvantages
- The performance depends on the choice of gap sequence.
- Not a stable sort: Does not maintain the relative order of equal elements.

Shell Sort is often used in scenarios where a simple and efficient sorting algorithm is needed[1](https://www.baeldung.com/java-shell-sort)[2](https://www.javatpoint.com/shell-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.baeldung.com/java-shell-sort): [1](https://www.baeldung.com/java-shell-sort)
[2](https://www.javatpoint.com/shell-sort): [2](https://www.javatpoint.com/shell-sort)

## Counting Sort

Sure! Counting Sort is a non-comparison-based sorting algorithm that sorts elements by counting the number of occurrences of each unique element in the array. It is particularly efficient when the range of input values is not significantly larger than the number of elements. Here's how you can implement Counting Sort in Java:

### Counting Sort Implementation in Java

```java
public class CountingSort {
    public static void countingSort(int[] array) {
        int n = array.length;

        // Find the maximum element in the array
        int max = array[0];
        for (int i = 1; i < n; i++) {
            if (array[i] > max) {
                max = array[i];
            }
        }

        // Create a count array to store the count of each unique element
        int[] count = new int[max + 1];

        // Store the count of each element in the count array
        for (int i = 0; i < n; i++) {
            count[array[i]]++;
        }

        // Modify the count array such that each element at each index
        // stores the sum of previous counts
        for (int i = 1; i <= max; i++) {
            count[i] += count[i - 1];
        }

        // Output array to store the sorted elements
        int[] output = new int[n];

        // Build the output array using the count array
        for (int i = n - 1; i >= 0; i--) {
            output[count[array[i]] - 1] = array[i];
            count[array[i]]--;
        }

        // Copy the sorted elements back to the original array
        for (int i = 0; i < n; i++) {
            array[i] = output[i];
        }
    }

    public static void main(String[] args) {
        int[] array = {4, 2, 2, 8, 3, 3, 1};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        countingSort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Find Maximum Element**: Determine the maximum value in the array to define the range of the count array.
2. **Count Occurrences**: Create a count array to store the count of each unique element.
3. **Cumulative Count**: Modify the count array to store the cumulative count of elements.
4. **Build Output Array**: Use the count array to place elements in their correct positions in the output array.
5. **Copy Back**: Copy the sorted elements from the output array back to the original array.

### Complexity Analysis
- **Time Complexity**: \(O(n + k)\), where \(n\) is the number of elements in the array and \(k\) is the range of the input values.
- **Space Complexity**: \(O(n + k)\) due to the count and output arrays.

### Advantages
- Efficient for sorting integers with a limited range.
- Linear time complexity for small ranges.

### Disadvantages
- Not suitable for large ranges of input values.
- Requires additional memory proportional to the range of the input values.

Counting Sort is often used in scenarios where the range of input values is small compared to the number of elements[1](https://www.javatpoint.com/counting-sort-in-java)[2](https://www.programiz.com/dsa/counting-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/counting-sort-in-java): [1](https://www.javatpoint.com/counting-sort-in-java)
[2](https://www.programiz.com/dsa/counting-sort): [2](https://www.baeldung.com/java-counting-sort)

## Radix Sort

Sure! Radix Sort is a non-comparison-based sorting algorithm that sorts integers by processing individual digits. It works by sorting the numbers digit by digit, starting from the least significant digit to the most significant digit. Here's how you can implement Radix Sort in Java:

### Radix Sort Implementation in Java

```java
import java.util.Arrays;

public class RadixSort {
    public static void radixSort(int[] array) {
        // Find the maximum number to know the number of digits
        int max = Arrays.stream(array).max().getAsInt();

        // Apply counting sort to sort elements based on place value
        for (int exp = 1; max / exp > 0; exp *= 10) {
            countingSort(array, exp);
        }
    }

    private static void countingSort(int[] array, int exp) {
        int n = array.length;
        int[] output = new int[n]; // Output array
        int[] count = new int[10]; // Count array to store count of occurrences of digits

        // Store count of occurrences of digits
        for (int i = 0; i < n; i++) {
            int index = (array[i] / exp) % 10;
            count[index]++;
        }

        // Change count[i] so that count[i] contains the actual position of this digit in output[]
        for (int i = 1; i < 10; i++) {
            count[i] += count[i - 1];
        }

        // Build the output array
        for (int i = n - 1; i >= 0; i--) {
            int index = (array[i] / exp) % 10;
            output[count[index] - 1] = array[i];
            count[index]--;
        }

        // Copy the output array to array[], so that array[] now contains sorted numbers
        System.arraycopy(output, 0, array, 0, n);
    }

    public static void main(String[] args) {
        int[] array = {170, 45, 75, 90, 802, 24, 2, 66};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        radixSort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Find Maximum Element**: Determine the maximum value in the array to know the number of digits.
2. **Counting Sort by Digit**: Perform counting sort for each digit, starting from the least significant digit to the most significant digit.

### Complexity Analysis
- **Time Complexity**: \(O(d \times (n + k))\), where \(d\) is the number of digits in the maximum number, \(n\) is the number of elements, and \(k\) is the range of the digit (0-9 for decimal numbers).
- **Space Complexity**: \(O(n + k)\) due to the count and output arrays.

### Advantages
- Efficient for sorting integers with a fixed range of digits.
- Linear time complexity for small ranges.

### Disadvantages
- Not suitable for large ranges of input values.
- Requires additional memory proportional to the range of the input values.

Radix Sort is often used in scenarios where the range of input values is small compared to the number of elements[1](https://www.javatpoint.com/radix-sort)[2](https://www.baeldung.com/java-radix-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/radix-sort): [1](https://www.javatpoint.com/radix-sort)
[2](https://www.baeldung.com/java-radix-sort): [2](https://www.baeldung.com/java-radix-sort)

## Bucket Sort

Sure! Bucket Sort is a non-comparison-based sorting algorithm that works by distributing elements into several buckets and then sorting each bucket individually. It is particularly useful for sorting floating-point numbers or uniformly distributed data. Here's how you can implement Bucket Sort in Java:

### Bucket Sort Implementation in Java

```java
import java.util.*;

public class BucketSort {
    public static void bucketSort(float[] array, int n) {
        if (n <= 0) return;

        // Create empty buckets
        @SuppressWarnings("unchecked")
        ArrayList<Float>[] buckets = new ArrayList[n];

        for (int i = 0; i < n; i++) {
            buckets[i] = new ArrayList<>();
        }

        // Put array elements in different buckets
        for (int i = 0; i < n; i++) {
            int bucketIndex = (int) array[i] * n;
            buckets[bucketIndex].add(array[i]);
        }

        // Sort individual buckets
        for (int i = 0; i < n; i++) {
            Collections.sort(buckets[i]);
        }

        // Concatenate all buckets into array
        int index = 0;
        for (int i = 0; i < n; i++) {
            for (float value : buckets[i]) {
                array[index++] = value;
            }
        }
    }

    public static void main(String[] args) {
        float[] array = {0.897f, 0.565f, 0.656f, 0.1234f, 0.665f, 0.3434f};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        bucketSort(array, array.length);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Create Buckets**: Create an array of empty buckets.
2. **Distribute Elements**: Distribute the elements into their respective buckets based on a hashing function.
3. **Sort Buckets**: Sort each bucket individually using a suitable sorting algorithm (e.g., Insertion Sort or Collections.sort).
4. **Concatenate Buckets**: Concatenate the sorted buckets to form the final sorted array.

### Complexity Analysis
- **Time Complexity**:
   - Best Case: \(O(n + k)\)
   - Average Case: \(O(n + k)\)
   - Worst Case: \(O(n^2)\) (when all elements are placed in a single bucket)
- **Space Complexity**: \(O(n + k)\), where \(n\) is the number of elements and \(k\) is the number of buckets.

### Advantages
- Efficient for sorting floating-point numbers or uniformly distributed data.
- Reduces the number of comparisons.

### Disadvantages
- Not an in-place sorting algorithm (requires additional space for buckets).
- Performance depends on the distribution of input data.

Bucket Sort is often used in scenarios where the input data is uniformly distributed and the range of values is known[1](https://www.javatpoint.com/bucket-sort-in-java)[2](https://www.baeldung.com/java-bucket-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/bucket-sort-in-java): [1](https://www.javatpoint.com/bucket-sort-in-java)
[2](https://www.baeldung.com/java-bucket-sort): [2](https://www.baeldung.com/java-bucket-sort)


## Cocktail Shaker Sort

Cocktail Shaker Sort, also known as Bidirectional Bubble Sort, is an extension of Bubble Sort that sorts an array in both directions. It improves on Bubble Sort by more quickly moving items to their correct positions at both ends of the list. Here's how you can implement Cocktail Shaker Sort in Java:

### Cocktail Shaker Sort Implementation in Java

```java
public class CocktailShakerSort {
    public static void cocktailShakerSort(int[] array) {
        boolean swapped = true;
        int start = 0;
        int end = array.length;

        while (swapped) {
            swapped = false;

            // Traverse the array from left to right
            for (int i = start; i < end - 1; ++i) {
                if (array[i] > array[i + 1]) {
                    // Swap elements
                    int temp = array[i];
                    array[i] = array[i + 1];
                    array[i + 1] = temp;
                    swapped = true;
                }
            }

            // If no elements were swapped, the array is sorted
            if (!swapped) {
                break;
            }

            // Otherwise, reset the swapped flag so that it can be used in the next stage
            swapped = false;

            // Move the end point back by one, because the last element is in its correct position
            end--;

            // Traverse the array from right to left
            for (int i = end - 1; i >= start; --i) {
                if (array[i] > array[i + 1]) {
                    // Swap elements
                    int temp = array[i];
                    array[i] = array[i + 1];
                    array[i + 1] = temp;
                    swapped = true;
                }
            }

            // Increase the starting point, because the first element is in its correct position
            start++;
        }
    }

    public static void main(String[] args) {
        int[] array = {5, 1, 4, 2, 8, 0, 2};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        cocktailShakerSort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Bidirectional Traversal**: The algorithm traverses the array from left to right, then from right to left, repeatedly.
2. **Swapping Elements**: During each traversal, adjacent elements are compared and swapped if they are in the wrong order.
3. **Adjusting Boundaries**: After each pass, the boundaries of the unsorted portion of the array are adjusted.

### Complexity Analysis
- **Time Complexity**:
   - Best Case: \(O(n)\) (when the array is already sorted)
   - Average and Worst Case: \(O(n^2)\)
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- Simple to understand and implement.
- More efficient than Bubble Sort for certain types of data.

### Disadvantages
- Still inefficient for large datasets due to its quadratic time complexity.
- Not widely used in practice, mainly serves educational purposes[1](https://en.wikipedia.org/wiki/Cocktail_shaker_sort)[2](https://www.baeldung.com/cs/cocktail-sort).

Would you like to know more about any other sorting algorithms?
[1](https://en.wikipedia.org/wiki/Cocktail_shaker_sort): [1](https://en.wikipedia.org/wiki/Cocktail_shaker_sort)
[2](https://www.baeldung.com/cs/cocktail-sort): [2](https://www.baeldung.com/cs/cocktail-sort)

## Comb Sort

Sure! Comb Sort is an improvement over Bubble Sort that eliminates "turtles" (small values near the end of the list) by using a gap sequence that starts larger and shrinks over time. The gap is initially set to the length of the array divided by a shrink factor (commonly 1.3), and it decreases with each iteration until it becomes 1. Here's how you can implement Comb Sort in Java:

### Comb Sort Implementation in Java

```java
public class CombSort {
    public static void combSort(int[] array) {
        int n = array.length;
        int gap = n;
        boolean swapped = true;
        double shrink = 1.3;

        while (gap > 1 || swapped) {
            // Update the gap value for the next comb
            gap = (int) (gap / shrink);
            if (gap < 1) {
                gap = 1;
            }

            swapped = false;

            // Compare all elements with the current gap
            for (int i = 0; i + gap < n; i++) {
                if (array[i] > array[i + gap]) {
                    // Swap elements
                    int temp = array[i];
                    array[i] = array[i + gap];
                    array[i + gap] = temp;
                    swapped = true;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] array = {8, 4, 1, 56, 3, -44, 23, -6, 28, 0};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        combSort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Gap Sequence**: Start with a large gap and reduce it by a shrink factor (commonly 1.3) in each iteration.
2. **Swapping Elements**: Compare and swap elements that are `gap` distance apart.
3. **Adjust Gap**: Continue reducing the gap until it becomes 1, at which point the array is sorted using a final pass similar to Bubble Sort.

### Complexity Analysis
- **Time Complexity**:
   - Best Case: \(O(n \log n)\)
   - Average and Worst Case: \(O(n^2)\)
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- More efficient than Bubble Sort for larger datasets.
- Simple to understand and implement.

### Disadvantages
- Still not as efficient as more advanced algorithms like Quick Sort or Merge Sort for very large datasets.

Comb Sort is often used as an educational tool to demonstrate improvements over Bubble Sort[1](https://www.javatpoint.com/comb-sort)[2](https://www.tutorialspoint.com/java-program-for-comb-sort).

Would you like to know more about any other sorting algorithms?
[1](https://www.javatpoint.com/comb-sort): [1](https://www.javatpoint.com/comb-sort)
[2](https://www.tutorialspoint.com/java-program-for-comb-sort): [2](https://www.tutorialspoint.com/java-program-for-comb-sort)

## Gnome Sort

Sure! Gnome Sort, also known as Stupid Sort, is a simple sorting algorithm that works by iterating through a list, comparing adjacent elements, and swapping them if they are in the wrong order. If a swap occurs, the algorithm moves one step backward to recheck the order; otherwise, it moves forward. This process continues until the array is sorted. Here's how you can implement Gnome Sort in Java:

### Gnome Sort Implementation in Java

```java
public class GnomeSort {
    public static void gnomeSort(int[] arr) {
        int index = 0;
        while (index < arr.length) {
            if (index == 0 || arr[index] >= arr[index - 1]) {
                index++;
            } else {
                // Swap elements
                int temp = arr[index];
                arr[index] = arr[index - 1];
                arr[index - 1] = temp;
                index--;
            }
        }
    }

    // Helper method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {34, 2, 78, 12, 45, 1, 90};
        System.out.println("Original Array:");
        printArray(arr);

        gnomeSort(arr);

        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```

### How It Works
1. **Forward Movement**: If the current element is greater than or equal to the previous element, move forward.
2. **Backward Movement**: If the current element is smaller than the previous element, swap them and move backward.
3. **Termination**: The loop continues until the end of the array is reached, ensuring all elements are sorted.

### Complexity Analysis
- **Time Complexity**: \(O(n^2)\) in the worst and average cases, similar to Bubble Sort.
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- Simple to understand and implement.
- Works well for small or nearly sorted datasets.

### Disadvantages
- Inefficient for large datasets due to its quadratic time complexity.

Gnome Sort is often used for educational purposes to demonstrate basic sorting concepts[1](https://www.tutorialspoint.com/java-program-for-gnome-sort)[2](https://www.w3resource.com/java-exercises/sorting/java-sorting-algorithm-exercise-13.php).

Would you like to know more about any other sorting algorithms?
[1](https://www.tutorialspoint.com/java-program-for-gnome-sort): [1](https://www.tutorialspoint.com/java-program-for-gnome-sort)
[2](https://www.w3resource.com/java-exercises/sorting/java-sorting-algorithm-exercise-13.php): [2](https://www.w3resource.com/java-exercises/sorting/java-sorting-algorithm-exercise-13.php)

## Odd-Even Sort

Sure! Odd-Even Sort, also known as Brick Sort, is a simple comparison-based sorting algorithm. It works by iteratively comparing and swapping adjacent elements in two phases: odd and even. Here's how you can implement Odd-Even Sort in Java:

### Odd-Even Sort Implementation in Java

```java
public class OddEvenSort {
    public static void oddEvenSort(int[] array) {
        boolean sorted = false;
        while (!sorted) {
            sorted = true;

            // Perform Bubble Sort on odd indexed elements
            for (int i = 1; i < array.length - 1; i += 2) {
                if (array[i] > array[i + 1]) {
                    // Swap elements
                    int temp = array[i];
                    array[i] = array[i + 1];
                    array[i + 1] = temp;
                    sorted = false;
                }
            }

            // Perform Bubble Sort on even indexed elements
            for (int i = 0; i < array.length - 1; i += 2) {
                if (array[i] > array[i + 1]) {
                    // Swap elements
                    int temp = array[i];
                    array[i] = array[i + 1];
                    array[i + 1] = temp;
                    sorted = false;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] array = {34, 2, 78, 12, 45, 1, 90};
        System.out.println("Original Array:");
        System.out.println(Arrays.toString(array));

        oddEvenSort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));
    }
}
```

### How It Works
1. **Odd Phase**: Compare and swap adjacent elements at odd indices.
2. **Even Phase**: Compare and swap adjacent elements at even indices.
3. **Repeat**: Continue the process until the array is sorted.

### Complexity Analysis
- **Time Complexity**:
   - Best Case: \(O(n)\) (when the array is already sorted)
   - Average and Worst Case: \(O(n^2)\)
- **Space Complexity**: \(O(1)\) as it is an in-place sorting algorithm.

### Advantages
- Simple to understand and implement.
- Can be parallelized easily.

### Disadvantages
- Inefficient for large datasets due to its quadratic time complexity.

Odd-Even Sort is often used for educational purposes and in parallel computing scenarios[1](https://en.wikipedia.org/wiki/Odd%E2%80%93even_sort)[2](https://www.altcademy.com/blog/odd-even-sort-or-brick-sort/).

Would you like to know more about any other sorting algorithms?
[1](https://en.wikipedia.org/wiki/Odd%E2%80%93even_sort): [1](https://en.wikipedia.org/wiki/Odd%E2%80%93even_sort)
[2](https://www.altcademy.com/blog/odd-even-sort-or-brick-sort/): [2](https://www.altcademy.com/blog/odd-even-sort-or-brick-sort/)


# Most asked Algorithms

Here are some of the most commonly asked algorithms in coding interviews by companies:

### 1. Sorting Algorithms
- **Quick Sort**
- **Merge Sort**
- **Heap Sort**

### 2. Searching Algorithms
- **Binary Search**
- **Depth-First Search (DFS)**
- **Breadth-First Search (BFS)**

### 3. Dynamic Programming
- **Longest Common Subsequence**
- **Knapsack Problem**
- **Fibonacci Sequence**

### 4. Greedy Algorithms
- **Activity Selection**
- **Huffman Coding**
- **Dijkstra's Algorithm**

### 5. Graph Algorithms
- **Kruskal's Algorithm**
- **Prim's Algorithm**
- **Bellman-Ford Algorithm**

### 6. Backtracking
- **N-Queens Problem**
- **Sudoku Solver**
- **Subset Sum Problem**

### 7. Divide and Conquer
- **Merge Sort**
- **Quick Sort**
- **Binary Search**

### 8. String Algorithms
- **KMP Algorithm**
- **Rabin-Karp Algorithm**
- **Longest Palindromic Substring**

### 9. Tree and Binary Tree Algorithms
- **Inorder, Preorder, Postorder Traversal**
- **Lowest Common Ancestor**
- **Binary Search Tree Operations**

### 10. Miscellaneous
- **Two-Pointer Technique**
- **Sliding Window Technique**
- **Union-Find Algorithm**

These algorithms cover a wide range of problem-solving techniques and are frequently encountered in coding interviews[1](https://igotanoffer.com/blogs/tech/algorithms-interview-questions)[2](https://www.nucamp.co/blog/coding-bootcamp-job-hunting-cracking-coding-interviews-top-algorithm-questions-explained)[3](https://www.educative.io/blog/ace-top-15-java-algorithm-questions). Preparing for these will help you tackle a variety of questions effectively.

Is there a specific algorithm or problem you'd like to dive deeper into?





# Leetcode 150 + Blind 75 and handpicked questions from Love Baber DSA 450 list


# Topic - Array

## Two Sum

The Two Sum problem is a classic algorithmic challenge that can be solved using various approaches. Here are three different methods to solve the Two Sum problem in Java:

### 1. Brute Force Approach
This is the simplest approach where we use two nested loops to check every possible pair of numbers to see if they add up to the target.

```java
public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[] { i, j };
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }

    public static void main(String[] args) {
        TwoSum ts = new TwoSum();
        int[] result = ts.twoSum(new int[] {2, 7, 11, 15}, 9);
        System.out.println("Indices: " + result[0] + ", " + result[1]);
    }
}
```
- **Time Complexity**: \( O(n^2) \)
- **Space Complexity**: \( O(1) \)

### 2. Using HashMap
This approach uses a HashMap to store the difference between the target and each element as we iterate through the array. This allows us to find the solution in linear time.

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
        TwoSum ts = new TwoSum();
        int[] result = ts.twoSum(new int[] {2, 7, 11, 15}, 9);
        System.out.println("Indices: " + result[0] + ", " + result[1]);
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

### 3. Two-Pointer Approach
This approach works when the array is sorted. We use two pointers, one starting from the beginning and the other from the end of the array, and move them towards each other until we find the target sum.

```java
import java.util.Arrays;

public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        int[] sortedNums = nums.clone();
        Arrays.sort(sortedNums);
        int left = 0, right = sortedNums.length - 1;
        while (left < right) {
            int sum = sortedNums[left] + sortedNums[right];
            if (sum == target) {
                return new int[] { left, right };
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }

    public static void main(String[] args) {
        TwoSum ts = new TwoSum();
        int[] result = ts.twoSum(new int[] {2, 7, 11, 15}, 9);
        System.out.println("Indices: " + result[0] + ", " + result[1]);
    }
}
```
- **Time Complexity**: \( O(n \log n) \) due to sorting
- **Space Complexity**: \( O(n) \)

Each of these approaches has its own advantages and trade-offs. The brute force method is straightforward but inefficient for large arrays. The HashMap approach is efficient and works well for unsorted arrays. The two-pointer approach is efficient but requires the array to be sorted[1](https://www.callicoder.com/two-sum-problem/)[2](https://kodeao.com/how-to-solve-two-sum-problem-2-solutions/)[3](https://dev.to/nullvoidkage/solving-the-two-sum-problem-multiple-approaches-using-javapython-9kk).

If you have any specific questions or need further details, feel free to ask!


## Best Time to Buy and Sell Stock

The "Best Time to Buy and Sell Stock" problem is a classic algorithmic challenge that can be solved using various approaches. Here are three different methods to solve this problem in Java:

### Problem Statement
Given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day, you want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

### 1. Brute Force Approach
This approach checks every possible pair of days to find the maximum profit. It is simple but inefficient for large inputs.

```java
public class BestTimeToBuyAndSellStock {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for (int i = 0; i < prices.length; i++) {
            for (int j = i + 1; j < prices.length; j++) {
                int profit = prices[j] - prices[i];
                if (profit > maxProfit) {
                    maxProfit = profit;
                }
            }
        }
        return maxProfit;
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStock solution = new BestTimeToBuyAndSellStock();
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 5
    }
}
```
- **Time Complexity**: \( O(n^2) \)
- **Space Complexity**: \( O(1) \)

### 2. One-Pass Approach
This approach keeps track of the minimum price encountered so far and calculates the maximum profit by comparing the current price with the minimum price.

```java
public class BestTimeToBuyAndSellStock {
    public int maxProfit(int[] prices) {
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
        BestTimeToBuyAndSellStock solution = new BestTimeToBuyAndSellStock();
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 5
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### 3. Dynamic Programming Approach
This approach uses dynamic programming to keep track of the maximum profit at each step. It maintains an array to store the maximum profit that can be achieved up to each day.

```java
public class BestTimeToBuyAndSellStock {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) return 0;
        int[] dp = new int[prices.length];
        int minPrice = prices[0];
        for (int i = 1; i < prices.length; i++) {
            dp[i] = Math.max(dp[i - 1], prices[i] - minPrice);
            minPrice = Math.min(minPrice, prices[i]);
        }
        return dp[prices.length - 1];
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStock solution = new BestTimeToBuyAndSellStock();
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 5
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

### Summary
- **Brute Force**: Simple but inefficient for large inputs.
- **One-Pass**: Efficient and straightforward, with linear time complexity.
- **Dynamic Programming**: Useful for understanding the problem in terms of subproblems, though it may use more space.

Each approach has its own advantages and trade-offs. The one-pass approach is generally preferred due to its simplicity and efficiency[1](https://favtutor.com/articles/best-time-to-buy-and-sell-stock-problem/)[2](https://algo.monster/liteproblems/121)[3](https://www.programcreek.com/2014/02/leetcode-best-time-to-buy-and-sell-stock-java/).

If you have any specific questions or need further details, feel free to ask!


# Best Time to Buy and Sell Stock II

The "Best Time to Buy and Sell Stock II" problem allows you to make multiple transactions to maximize profit. You can buy and sell the stock on the same day, but you can only hold one share of the stock at any time. Here are different approaches to solve this problem in Java:

### Problem Statement
Given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day, return the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

### 1. Greedy Approach
This approach takes advantage of every profitable opportunity by buying on one day and selling on the next if the price is higher.

```java
public class BestTimeToBuyAndSellStockII {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                maxProfit += prices[i] - prices[i - 1];
            }
        }
        return maxProfit;
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStockII solution = new BestTimeToBuyAndSellStockII();
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 7
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### 2. Peak Valley Approach
This approach identifies every peak immediately following a valley to maximize profit.

```java
public class BestTimeToBuyAndSellStockII {
    public int maxProfit(int[] prices) {
        int i = 0;
        int maxProfit = 0;
        int n = prices.length;
        while (i < n - 1) {
            // Find the next valley
            while (i < n - 1 && prices[i] >= prices[i + 1]) i++;
            int valley = prices[i];
            // Find the next peak
            while (i < n - 1 && prices[i] <= prices[i + 1]) i++;
            int peak = prices[i];
            maxProfit += peak - valley;
        }
        return maxProfit;
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStockII solution = new BestTimeToBuyAndSellStockII();
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 7
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### 3. Dynamic Programming Approach
This approach uses dynamic programming to keep track of the maximum profit at each step.

```java
public class BestTimeToBuyAndSellStockII {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        if (n == 0) return 0;
        int[][] dp = new int[n][2];
        dp[0][0] = 0; // Max profit on day 0 with no stock
        dp[0][1] = -prices[0]; // Max profit on day 0 with stock

        for (int i = 1; i < n; i++) {
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]); // No stock
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]); // With stock
        }
        return dp[n - 1][0];
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStockII solution = new BestTimeToBuyAndSellStockII();
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 7
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

### Summary
- **Greedy Approach**: Efficient and straightforward, focusing on every profitable opportunity.
- **Peak Valley Approach**: Identifies peaks and valleys to maximize profit.
- **Dynamic Programming Approach**: Uses a more structured approach to track profits, though it may use more space.

Each approach has its own advantages and trade-offs. The greedy approach is generally preferred due to its simplicity and efficiency[1](https://algo.monster/liteproblems/122)[2](https://github.com/ppriyasingh/LeetCode/blob/master/Solutions/122.%20Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.java)[3](https://favtutor.com/articles/best-time-to-buy-and-sell-stock-ii/).

If you have any specific questions or need further details, feel free to ask!

# Best Time to Buy and Sell Stock III

The "Best Time to Buy and Sell Stock III" problem allows you to complete at most two transactions to maximize profit. Here are different approaches to solve this problem in Java:

### Problem Statement
Given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day, return the maximum profit you can achieve from at most two transactions. A transaction consists of buying and then selling one share of the stock. You cannot engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

### 1. Dynamic Programming Approach
This approach uses dynamic programming to keep track of profits across four different states, representing the four actions you can take: buying the first stock, selling the first stock, buying the second stock, and selling the second stock.

```java
public class BestTimeToBuyAndSellStockIII {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) return 0;

        int n = prices.length;
        int[] dp1 = new int[n];
        int[] dp2 = new int[n];

        // First transaction
        int minPrice = prices[0];
        for (int i = 1; i < n; i++) {
            minPrice = Math.min(minPrice, prices[i]);
            dp1[i] = Math.max(dp1[i - 1], prices[i] - minPrice);
        }

        // Second transaction
        int maxPrice = prices[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            maxPrice = Math.max(maxPrice, prices[i]);
            dp2[i] = Math.max(dp2[i + 1], maxPrice - prices[i]);
        }

        // Combine the results of the two transactions
        int maxProfit = 0;
        for (int i = 0; i < n; i++) {
            maxProfit = Math.max(maxProfit, dp1[i] + dp2[i]);
        }

        return maxProfit;
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStockIII solution = new BestTimeToBuyAndSellStockIII();
        int[] prices = {3, 3, 5, 0, 0, 3, 1, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

### 2. Optimized Dynamic Programming Approach
This approach optimizes space by using variables instead of arrays to keep track of the four states.

```java
public class BestTimeToBuyAndSellStockIII {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) return 0;

        int buy1 = Integer.MIN_VALUE, buy2 = Integer.MIN_VALUE;
        int sell1 = 0, sell2 = 0;

        for (int price : prices) {
            buy1 = Math.max(buy1, -price);
            sell1 = Math.max(sell1, buy1 + price);
            buy2 = Math.max(buy2, sell1 - price);
            sell2 = Math.max(sell2, buy2 + price);
        }

        return sell2;
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStockIII solution = new BestTimeToBuyAndSellStockIII();
        int[] prices = {3, 3, 5, 0, 0, 3, 1, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### 3. Divide and Conquer Approach
This approach divides the array into two parts and calculates the maximum profit for each part, then combines the results.

```java
public class BestTimeToBuyAndSellStockIII {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) return 0;

        int n = prices.length;
        int[] leftProfits = new int[n];
        int[] rightProfits = new int[n + 1];

        // Left to right
        int minPrice = prices[0];
        for (int i = 1; i < n; i++) {
            minPrice = Math.min(minPrice, prices[i]);
            leftProfits[i] = Math.max(leftProfits[i - 1], prices[i] - minPrice);
        }

        // Right to left
        int maxPrice = prices[n - 1];
        for (int i = n - 1; i >= 0; i--) {
            maxPrice = Math.max(maxPrice, prices[i]);
            rightProfits[i] = Math.max(rightProfits[i + 1], maxPrice - prices[i]);
        }

        // Combine the results
        int maxProfit = 0;
        for (int i = 0; i < n; i++) {
            maxProfit = Math.max(maxProfit, leftProfits[i] + rightProfits[i + 1]);
        }

        return maxProfit;
    }

    public static void main(String[] args) {
        BestTimeToBuyAndSellStockIII solution = new BestTimeToBuyAndSellStockIII();
        int[] prices = {3, 3, 5, 0, 0, 3, 1, 4};
        System.out.println("Max Profit: " + solution.maxProfit(prices)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

### Summary
- **Dynamic Programming**: Uses arrays to keep track of profits for each transaction.
- **Optimized Dynamic Programming**: Uses variables to reduce space complexity.
- **Divide and Conquer**: Splits the problem into two parts and combines the results.

Each approach has its own advantages and trade-offs. The optimized dynamic programming approach is generally preferred due to its simplicity and efficiency[1](https://algo.monster/liteproblems/123)[2](https://favtutor.com/articles/best-time-to-buy-and-sell-stock-problem/)[3](https://www.naukri.com/code360/library/best-time-to-buy-and-sell-stock-iii).

If you have any specific questions or need further details, feel free to ask!


# Contains Duplicate 

The "Contains Duplicate" problem is a common algorithmic challenge where you need to determine if an array contains any duplicate elements. Here are a few different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach uses two nested loops to compare each element with every other element in the array.

```java
public class ContainsDuplicate {
    public boolean containsDuplicate(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] == nums[j]) {
                    return true;
                }
            }
        }
        return false;
    }

    public static void main(String[] args) {
        ContainsDuplicate solution = new ContainsDuplicate();
        int[] nums = {1, 2, 3, 1};
        System.out.println("Contains Duplicate: " + solution.containsDuplicate(nums)); // Output: true
    }
}
```
- **Time Complexity**: \( O(n^2) \)
- **Space Complexity**: \( O(1) \)

### 2. Using HashSet
This approach uses a HashSet to keep track of the elements we have seen so far. If we encounter an element that is already in the HashSet, we return true.

```java
import java.util.HashSet;
import java.util.Set;

public class ContainsDuplicate {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }
        return false;
    }

    public static void main(String[] args) {
        ContainsDuplicate solution = new ContainsDuplicate();
        int[] nums = {1, 2, 3, 1};
        System.out.println("Contains Duplicate: " + solution.containsDuplicate(nums)); // Output: true
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

### 3. Using Sorting
This approach sorts the array first and then checks for any consecutive duplicate elements.

```java
import java.util.Arrays;

public class ContainsDuplicate {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        ContainsDuplicate solution = new ContainsDuplicate();
        int[] nums = {1, 2, 3, 1};
        System.out.println("Contains Duplicate: " + solution.containsDuplicate(nums)); // Output: true
    }
}
```
- **Time Complexity**: \( O(n \log n) \) due to sorting
- **Space Complexity**: \( O(1) \) if sorting in place

### Summary
- **Brute Force**: Simple but inefficient for large arrays.
- **HashSet**: Efficient and straightforward, with linear time complexity.
- **Sorting**: Efficient but requires sorting the array first.

Each approach has its own advantages and trade-offs. The HashSet approach is generally preferred due to its simplicity and efficiency[1](https://leetcode.com/problems/contains-duplicate/)[2](https://www.baeldung.com/java-list-find-duplicates)[3](https://javaconceptoftheday.com/find-duplicates-in-array-in-java/).

If you have any specific questions or need further details, feel free to ask!

## Product of Array Except Self

The "Product of Array Except Self" problem requires creating a new array where each element at index \( i \) of the new array is the product of all the numbers in the original array except the one at \( i \). The challenge is to solve this without using division and in optimal time complexity. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach uses two nested loops to calculate the product of all elements except the current one for each element in the array.

```java
public class ProductOfArrayExceptSelf {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        for (int i = 0; i < n; i++) {
            int product = 1;
            for (int j = 0; j < n; j++) {
                if (i != j) {
                    product *= nums[j];
                }
            }
            result[i] = product;
        }
        return result;
    }

    public static void main(String[] args) {
        ProductOfArrayExceptSelf solution = new ProductOfArrayExceptSelf();
        int[] nums = {1, 2, 3, 4};
        int[] result = solution.productExceptSelf(nums);
        System.out.println(Arrays.toString(result)); // Output: [24, 12, 8, 6]
    }
}
```
- **Time Complexity**: \( O(n^2) \)
- **Space Complexity**: \( O(n) \)

### 2. Prefix and Suffix Products Approach
This approach uses two auxiliary arrays to store the prefix and suffix products. The prefix product at index \( i \) is the product of all elements before \( i \), and the suffix product at index \( i \) is the product of all elements after \( i \).

```java
public class ProductOfArrayExceptSelf {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] left = new int[n];
        int[] right = new int[n];
        int[] result = new int[n];

        // Fill the left array
        left[0] = 1;
        for (int i = 1; i < n; i++) {
            left[i] = left[i - 1] * nums[i - 1];
        }

        // Fill the right array
        right[n - 1] = 1;
        for (int i = n - 2; i >= 0; i--) {
            right[i] = right[i + 1] * nums[i + 1];
        }

        // Construct the result array
        for (int i = 0; i < n; i++) {
            result[i] = left[i] * right[i];
        }

        return result;
    }

    public static void main(String[] args) {
        ProductOfArrayExceptSelf solution = new ProductOfArrayExceptSelf();
        int[] nums = {1, 2, 3, 4};
        int[] result = solution.productExceptSelf(nums);
        System.out.println(Arrays.toString(result)); // Output: [24, 12, 8, 6]
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

### 3. Optimized Space Approach
This approach optimizes space by using the result array to store the prefix products and then updating it with the suffix products in a single pass.

```java
public class ProductOfArrayExceptSelf {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];

        // Calculate prefix products
        result[0] = 1;
        for (int i = 1; i < n; i++) {
            result[i] = result[i - 1] * nums[i - 1];
        }

        // Calculate suffix products and update the result array
        int suffixProduct = 1;
        for (int i = n - 1; i >= 0; i--) {
            result[i] *= suffixProduct;
            suffixProduct *= nums[i];
        }

        return result;
    }

    public static void main(String[] args) {
        ProductOfArrayExceptSelf solution = new ProductOfArrayExceptSelf();
        int[] nums = {1, 2, 3, 4};
        int[] result = solution.productExceptSelf(nums);
        System.out.println(Arrays.toString(result)); // Output: [24, 12, 8, 6]
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \) (excluding the output array)

### Summary
- **Brute Force**: Simple but inefficient for large arrays.
- **Prefix and Suffix Products**: Efficient and straightforward, with linear time complexity.
- **Optimized Space**: Efficient and uses constant extra space.

Each approach has its own advantages and trade-offs. The optimized space approach is generally preferred due to its simplicity and efficiency[1](https://kamleshsingad.com/efficiently-solving-the-product-of-array-except-self-problem-in-java/)[2](https://leetcode.com/problems/product-of-array-except-self/)[3](https://dev.to/aswinbarath/product-of-array-except-self-leetcode-java-solution-4j72).

If you have any specific questions or need further details, feel free to ask!

## Maximum Subarray

The "Maximum Subarray" problem involves finding the contiguous subarray within a one-dimensional array of numbers which has the largest sum. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach checks every possible subarray to find the one with the maximum sum. It is simple but inefficient for large inputs.

```java
public class MaximumSubarray {
    public int maxSubArray(int[] nums) {
        int maxSum = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int currentSum = 0;
            for (int j = i; j < nums.length; j++) {
                currentSum += nums[j];
                if (currentSum > maxSum) {
                    maxSum = currentSum;
                }
            }
        }
        return maxSum;
    }

    public static void main(String[] args) {
        MaximumSubarray solution = new MaximumSubarray();
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum Subarray Sum: " + solution.maxSubArray(nums)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n^2) \)
- **Space Complexity**: \( O(1) \)

### 2. Kadane's Algorithm
This approach uses dynamic programming to find the maximum subarray sum in linear time. It maintains a running sum of the current subarray and updates the maximum sum whenever the running sum exceeds it.

```java
public class MaximumSubarray {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0];
        int currentSum = nums[0];
        for (int i = 1; i < nums.length; i++) {
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }
        return maxSum;
    }

    public static void main(String[] args) {
        MaximumSubarray solution = new MaximumSubarray();
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum Subarray Sum: " + solution.maxSubArray(nums)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### 3. Divide and Conquer Approach
This approach divides the array into two halves and recursively finds the maximum subarray sum in the left half, right half, and the crossing subarray that spans both halves.

```java
public class MaximumSubarray {
    public int maxSubArray(int[] nums) {
        return maxSubArrayHelper(nums, 0, nums.length - 1);
    }

    private int maxSubArrayHelper(int[] nums, int left, int right) {
        if (left == right) {
            return nums[left];
        }
        int mid = left + (right - left) / 2;
        int leftMax = maxSubArrayHelper(nums, left, mid);
        int rightMax = maxSubArrayHelper(nums, mid + 1, right);
        int crossMax = maxCrossingSubArray(nums, left, mid, right);
        return Math.max(Math.max(leftMax, rightMax), crossMax);
    }

    private int maxCrossingSubArray(int[] nums, int left, int mid, int right) {
        int leftSum = Integer.MIN_VALUE;
        int sum = 0;
        for (int i = mid; i >= left; i--) {
            sum += nums[i];
            if (sum > leftSum) {
                leftSum = sum;
            }
        }
        int rightSum = Integer.MIN_VALUE;
        sum = 0;
        for (int i = mid + 1; i <= right; i++) {
            sum += nums[i];
            if (sum > rightSum) {
                rightSum = sum;
            }
        }
        return leftSum + rightSum;
    }

    public static void main(String[] args) {
        MaximumSubarray solution = new MaximumSubarray();
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum Subarray Sum: " + solution.maxSubArray(nums)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n \log n) \)
- **Space Complexity**: \( O(\log n) \) due to recursion stack

### Summary
- **Brute Force**: Simple but inefficient for large arrays.
- **Kadane's Algorithm**: Efficient and straightforward, with linear time complexity.
- **Divide and Conquer**: Uses a recursive approach to divide the problem, with logarithmic time complexity.

Each approach has its own advantages and trade-offs. Kadane's Algorithm is generally preferred due to its simplicity and efficiency[1](https://www.baeldung.com/java-maximum-subarray)[2](https://www.programcreek.com/2013/02/leetcode-maximum-subarray-java/)[3](https://blog.heycoach.in/maximum-subarray-solution-in-java/).

If you have any specific questions or need further details, feel free to ask!

## Maximum Product Subarray

The "Maximum Product Subarray" problem involves finding the contiguous subarray within a one-dimensional array of numbers which has the largest product. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach checks every possible subarray to find the one with the maximum product. It is simple but inefficient for large inputs.

```java
public class MaximumProductSubarray {
    public int maxProduct(int[] nums) {
        int maxProduct = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int currentProduct = 1;
            for (int j = i; j < nums.length; j++) {
                currentProduct *= nums[j];
                maxProduct = Math.max(maxProduct, currentProduct);
            }
        }
        return maxProduct;
    }

    public static void main(String[] args) {
        MaximumProductSubarray solution = new MaximumProductSubarray();
        int[] nums = {2, 3, -2, 4};
        System.out.println("Maximum Product Subarray: " + solution.maxProduct(nums)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n^2) \)
- **Space Complexity**: \( O(1) \)

### 2. Dynamic Programming Approach
This approach uses dynamic programming to keep track of both the maximum and minimum product of subarrays ending at each position. This is necessary because a negative number can turn a small product into a large one and vice versa.

```java
public class MaximumProductSubarray {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        int maxProduct = nums[0];
        int maxEndingHere = nums[0];
        int minEndingHere = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int temp = maxEndingHere;
            maxEndingHere = Math.max(Math.max(maxEndingHere * nums[i], minEndingHere * nums[i]), nums[i]);
            minEndingHere = Math.min(Math.min(temp * nums[i], minEndingHere * nums[i]), nums[i]);
            maxProduct = Math.max(maxProduct, maxEndingHere);
        }

        return maxProduct;
    }

    public static void main(String[] args) {
        MaximumProductSubarray solution = new MaximumProductSubarray();
        int[] nums = {2, 3, -2, 4};
        System.out.println("Maximum Product Subarray: " + solution.maxProduct(nums)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### 3. Optimized Dynamic Programming Approach
This approach is similar to the previous one but uses a single pass to update the maximum and minimum products.

```java
public class MaximumProductSubarray {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        int maxProduct = nums[0];
        int maxEndingHere = nums[0];
        int minEndingHere = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {
                int temp = maxEndingHere;
                maxEndingHere = minEndingHere;
                minEndingHere = temp;
            }
            maxEndingHere = Math.max(nums[i], maxEndingHere * nums[i]);
            minEndingHere = Math.min(nums[i], minEndingHere * nums[i]);
            maxProduct = Math.max(maxProduct, maxEndingHere);
        }

        return maxProduct;
    }

    public static void main(String[] args) {
        MaximumProductSubarray solution = new MaximumProductSubarray();
        int[] nums = {2, 3, -2, 4};
        System.out.println("Maximum Product Subarray: " + solution.maxProduct(nums)); // Output: 6
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### Summary
- **Brute Force**: Simple but inefficient for large arrays.
- **Dynamic Programming**: Efficient and straightforward, with linear time complexity.
- **Optimized Dynamic Programming**: Similar to dynamic programming but with a single pass and constant space.

Each approach has its own advantages and trade-offs. The optimized dynamic programming approach is generally preferred due to its simplicity and efficiency[1](https://www.javatpoint.com/java-program-for-maximum-product-subarray)[2](https://www.javatpoint.com/maximum-product-subarray)[3](https://prepinsta.com/java-program/for-finding-the-maximum-product-of-sub-array-of-a-given-array/).

If you have any specific questions or need further details, feel free to ask!

## Find Minimum in Rotated Sorted Array

The "Find Minimum in Rotated Sorted Array" problem involves finding the minimum element in a rotated sorted array. Here are different approaches to solve this problem in Java:

### 1. Linear Search Approach
This approach simply iterates through the array to find the minimum element. It is straightforward but not efficient for large arrays.

```java
public class FindMinimumInRotatedSortedArray {
    public int findMin(int[] nums) {
        int min = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < min) {
                min = nums[i];
            }
        }
        return min;
    }

    public static void main(String[] args) {
        FindMinimumInRotatedSortedArray solution = new FindMinimumInRotatedSortedArray();
        int[] nums = {3, 4, 5, 1, 2};
        System.out.println("Minimum Element: " + solution.findMin(nums)); // Output: 1
    }
}
```
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(1) \)

### 2. Binary Search Approach
This approach leverages the properties of a rotated sorted array and uses binary search to find the minimum element efficiently.

```java
public class FindMinimumInRotatedSortedArray {
    public int findMin(int[] nums) {
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
        FindMinimumInRotatedSortedArray solution = new FindMinimumInRotatedSortedArray();
        int[] nums = {3, 4, 5, 1, 2};
        System.out.println("Minimum Element: " + solution.findMin(nums)); // Output: 1
    }
}
```
- **Time Complexity**: \( O(\log n) \)
- **Space Complexity**: \( O(1) \)

### 3. Recursive Binary Search Approach
This approach uses recursion to implement the binary search for finding the minimum element.

```java
public class FindMinimumInRotatedSortedArray {
    public int findMin(int[] nums) {
        return findMinHelper(nums, 0, nums.length - 1);
    }

    private int findMinHelper(int[] nums, int left, int right) {
        if (left == right) {
            return nums[left];
        }

        int mid = left + (right - left) / 2;

        if (nums[mid] > nums[right]) {
            return findMinHelper(nums, mid + 1, right);
        } else {
            return findMinHelper(nums, left, mid);
        }
    }

    public static void main(String[] args) {
        FindMinimumInRotatedSortedArray solution = new FindMinimumInRotatedSortedArray();
        int[] nums = {3, 4, 5, 1, 2};
        System.out.println("Minimum Element: " + solution.findMin(nums)); // Output: 1
    }
}
```
- **Time Complexity**: \( O(\log n) \)
- **Space Complexity**: \( O(\log n) \) due to recursion stack

### Summary
- **Linear Search**: Simple but inefficient for large arrays.
- **Binary Search**: Efficient and straightforward, with logarithmic time complexity.
- **Recursive Binary Search**: Similar to binary search but uses recursion.

Each approach has its own advantages and trade-offs. The binary search approach is generally preferred due to its simplicity and efficiency[1](https://www.javatpoint.com/find-minimum-in-rotated-sorted-array)[2](https://algo.monster/liteproblems/153)[3](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/).

If you have any specific questions or need further details, feel free to ask!

## Search in Rotated Sorted Array

Sure! Searching in a rotated sorted array can be approached in several ways. Here are a few methods you can use in Java:

### 1. Linear Search
This is the simplest approach where you iterate through the array and compare each element with the target. The time complexity is \(O(n)\).

```java
public class LinearSearch {
    public static int search(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        System.out.println("Index of target: " + search(nums, target));
    }
}
```

### 2. Binary Search (Pivot-based Approach)
This approach leverages the properties of the rotated sorted array. The time complexity is \(O(\log n)\).

```java
public class BinarySearch {
    public static int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[left] <= nums[mid]) { // Left half is sorted
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else { // Right half is sorted
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        System.out.println("Index of target: " + search(nums, target));
    }
}
```

### 3. Recursive Binary Search
This is a more elegant solution with similar time complexity as the pivot-based method.

```java
public class RecursiveBinarySearch {
    public static int search(int[] nums, int target) {
        return search(nums, target, 0, nums.length - 1);
    }

    private static int search(int[] nums, int target, int left, int right) {
        if (left > right) {
            return -1;
        }
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        }
        if (nums[left] <= nums[mid]) { // Left half is sorted
            if (nums[left] <= target && target < nums[mid]) {
                return search(nums, target, left, mid - 1);
            } else {
                return search(nums, target, mid + 1, right);
            }
        } else { // Right half is sorted
            if (nums[mid] < target && target <= nums[right]) {
                return search(nums, target, mid + 1, right);
            } else {
                return search(nums, target, left, mid - 1);
            }
        }
    }

    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        System.out.println("Index of target: " + search(nums, target));
    }
}
```

These approaches cover the basic and more optimized ways to search in a rotated sorted array. The binary search methods are generally preferred due to their efficiency[1](https://www.javatpoint.com/search-in-a-rotated-sorted-array)[2](https://www.tutorialspoint.com/java-program-for-search-an-element-in-a-sorted-and-rotated-array).

Would you like more details on any specific approach?

## 3 Sum

Sure! The 3Sum problem involves finding all unique triplets in an array that sum up to zero. Here are a few different approaches to solve this problem in Java:

### 1. Brute Force Approach
This is the simplest approach where you use three nested loops to check all possible triplets. The time complexity is \(O(n^3)\).

```java
import java.util.*;

public class ThreeSumBruteForce {
    public static List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        int n = nums.length;
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        List<Integer> triplet = Arrays.asList(nums[i], nums[j], nums[k]);
                        Collections.sort(triplet);
                        if (!result.contains(triplet)) {
                            result.add(triplet);
                        }
                    }
                }
            }
        }
        return result;
    }

    public static void main(String[] args) {
        int[] nums = {-1, 0, 1, 2, -1, -4};
        System.out.println(threeSum(nums));
    }
}
```

### 2. Sorting and Two Pointers Approach
This approach sorts the array first and then uses two pointers to find the triplets. The time complexity is \(O(n^2)\).

```java
import java.util.*;

public class ThreeSumTwoPointers {
    public static List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip duplicates
            int left = i + 1, right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1]) left++; // Skip duplicates
                    while (left < right && nums[right] == nums[right - 1]) right--; // Skip duplicates
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
        System.out.println(threeSum(nums));
    }
}
```

### 3. HashSet Approach
This approach uses a HashSet to avoid duplicates and find the triplets. The time complexity is \(O(n^2)\).

```java
import java.util.*;

public class ThreeSumHashSet {
    public static List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> result = new HashSet<>();
        for (int i = 0; i < nums.length - 2; i++) {
            Set<Integer> seen = new HashSet<>();
            for (int j = i + 1; j < nums.length; j++) {
                int complement = -nums[i] - nums[j];
                if (seen.contains(complement)) {
                    List<Integer> triplet = Arrays.asList(nums[i], nums[j], complement);
                    Collections.sort(triplet);
                    result.add(triplet);
                }
                seen.add(nums[j]);
            }
        }
        return new ArrayList<>(result);
    }

    public static void main(String[] args) {
        int[] nums = {-1, 0, 1, 2, -1, -4};
        System.out.println(threeSum(nums));
    }
}
```

These approaches cover the basic and more optimized ways to solve the 3Sum problem. The two-pointers method is generally preferred due to its efficiency[1](https://leetcode.com/problems/3sum/solutions/1489162/3-different-approaches-for-java/)[2](https://www.callicoder.com/three-sum-problem/).

Would you like more details on any specific approach?

## Container With Most Water

Sure! The "Container With Most Water" problem involves finding two lines in an array that, together with the x-axis, form a container that holds the most water. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach checks all possible pairs of lines to find the maximum area. The time complexity is \(O(n^2)\).

```java
public class ContainerWithMostWaterBruteForce {
    public int maxArea(int[] height) {
        int maxArea = 0;
        for (int i = 0; i < height.length; i++) {
            for (int j = i + 1; j < height.length; j++) {
                int area = Math.min(height[i], height[j]) * (j - i);
                maxArea = Math.max(maxArea, area);
            }
        }
        return maxArea;
    }

    public static void main(String[] args) {
        int[] height = {1, 8, 6, 2, 5, 4, 8, 3, 7};
        ContainerWithMostWaterBruteForce solution = new ContainerWithMostWaterBruteForce();
        System.out.println("Max Area: " + solution.maxArea(height)); // Output: 49
    }
}
```

### 2. Two Pointers Approach
This optimized approach uses two pointers, starting at the beginning and end of the array, and moves them towards each other. The time complexity is \(O(n)\).

```java
public class ContainerWithMostWaterTwoPointers {
    public int maxArea(int[] height) {
        int maxArea = 0;
        int left = 0, right = height.length - 1;
        while (left < right) {
            int area = Math.min(height[left], height[right]) * (right - left);
            maxArea = Math.max(maxArea, area);
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxArea;
    }

    public static void main(String[] args) {
        int[] height = {1, 8, 6, 2, 5, 4, 8, 3, 7};
        ContainerWithMostWaterTwoPointers solution = new ContainerWithMostWaterTwoPointers();
        System.out.println("Max Area: " + solution.maxArea(height)); // Output: 49
    }
}
```

### 3. Optimized Two Pointers Approach
This approach is similar to the two pointers method but includes additional checks to skip unnecessary calculations. The time complexity remains \(O(n)\).

```java
public class ContainerWithMostWaterOptimized {
    public int maxArea(int[] height) {
        int maxArea = 0;
        int left = 0, right = height.length - 1;
        while (left < right) {
            int minHeight = Math.min(height[left], height[right]);
            int area = minHeight * (right - left);
            maxArea = Math.max(maxArea, area);
            while (left < right && height[left] <= minHeight) left++;
            while (left < right && height[right] <= minHeight) right--;
        }
        return maxArea;
    }

    public static void main(String[] args) {
        int[] height = {1, 8, 6, 2, 5, 4, 8, 3, 7};
        ContainerWithMostWaterOptimized solution = new ContainerWithMostWaterOptimized();
        System.out.println("Max Area: " + solution.maxArea(height)); // Output: 49
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Container With Most Water" problem. The two-pointers method is generally preferred due to its efficiency[1](https://algocademy.com/link/?problem=container-with-most-water&lang=java&solution=1)[2](https://algo.monster/liteproblems/11).

Would you like more details on any specific approach?

## Remove Element

The "Remove Element" problem on LeetCode involves removing all instances of a specified value from an array in-place and returning the new length of the array. Here are different approaches to solve this problem in Java:

### 1. Two Pointers Approach
This is the most efficient approach, using two pointers to overwrite the elements to be removed. The time complexity is \(O(n)\).

```java
public class RemoveElementTwoPointers {
    public int removeElement(int[] nums, int val) {
        int k = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }

    public static void main(String[] args) {
        int[] nums = {3, 2, 2, 3};
        int val = 3;
        RemoveElementTwoPointers solution = new RemoveElementTwoPointers();
        int newLength = solution.removeElement(nums, val);
        System.out.println("New length: " + newLength); // Output: 2
    }
}
```

### 2. Two Pointers - When Elements to Remove are Rare
This approach is optimized for cases where the elements to be removed are rare. It swaps the elements to be removed with the last element in the array. The time complexity is \(O(n)\).

```java
public class RemoveElementOptimized {
    public int removeElement(int[] nums, int val) {
        int n = nums.length;
        int i = 0;
        while (i < n) {
            if (nums[i] == val) {
                nums[i] = nums[n - 1];
                n--;
            } else {
                i++;
            }
        }
        return n;
    }

    public static void main(String[] args) {
        int[] nums = {0, 1, 2, 2, 3, 0, 4, 2};
        int val = 2;
        RemoveElementOptimized solution = new RemoveElementOptimized();
        int newLength = solution.removeElement(nums, val);
        System.out.println("New length: " + newLength); // Output: 5
    }
}
```

### 3. Brute Force Approach
This approach uses a simple loop to shift elements left whenever an element to be removed is found. The time complexity is \(O(n^2)\).

```java
public class RemoveElementBruteForce {
    public int removeElement(int[] nums, int val) {
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (nums[i] == val) {
                for (int j = i; j < n - 1; j++) {
                    nums[j] = nums[j + 1];
                }
                n--;
                i--;
            }
        }
        return n;
    }

    public static void main(String[] args) {
        int[] nums = {3, 2, 2, 3};
        int val = 3;
        RemoveElementBruteForce solution = new RemoveElementBruteForce();
        int newLength = solution.removeElement(nums, val);
        System.out.println("New length: " + newLength); // Output: 2
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Remove Element" problem. The two-pointers method is generally preferred due to its efficiency[1](https://www.programcreek.com/2014/04/leetcode-remove-element-java/)[2](https://dev.to/rahulgithubweb/leetcode-challenge-remove-element-top-interview-questions-java-solution-3f6h).

Would you like more details on any specific approach?


## Merge Sorted Array

The "Merge Sorted Array" problem on LeetCode involves merging two sorted arrays into one sorted array in-place. Here are different approaches to solve this problem in Java:

### 1. Two Pointers from End
This approach uses two pointers starting from the end of both arrays and merges them into the first array. The time complexity is \(O(m + n)\).

```java
public class MergeSortedArray {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1; // Pointer for nums1
        int j = n - 1; // Pointer for nums2
        int k = m + n - 1; // Pointer for the merged array

        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }

        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 3, 0, 0, 0};
        int m = 3;
        int[] nums2 = {2, 5, 6};
        int n = 3;
        MergeSortedArray solution = new MergeSortedArray();
        solution.merge(nums1, m, nums2, n);
        System.out.println("Merged array: " + Arrays.toString(nums1)); // Output: [1, 2, 2, 3, 5, 6]
    }
}
```

### 2. Two Pointers from Start
This approach uses two pointers starting from the beginning of both arrays and merges them into a temporary array. The time complexity is \(O(m + n)\), but it requires extra space.

```java
public class MergeSortedArrayTemp {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int[] temp = new int[m + n];
        int i = 0, j = 0, k = 0;

        while (i < m && j < n) {
            if (nums1[i] <= nums2[j]) {
                temp[k++] = nums1[i++];
            } else {
                temp[k++] = nums2[j++];
            }
        }

        while (i < m) {
            temp[k++] = nums1[i++];
        }

        while (j < n) {
            temp[k++] = nums2[j++];
        }

        System.arraycopy(temp, 0, nums1, 0, m + n);
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 3, 0, 0, 0};
        int m = 3;
        int[] nums2 = {2, 5, 6};
        int n = 3;
        MergeSortedArrayTemp solution = new MergeSortedArrayTemp();
        solution.merge(nums1, m, nums2, n);
        System.out.println("Merged array: " + Arrays.toString(nums1)); // Output: [1, 2, 2, 3, 5, 6]
    }
}
```

### 3. Using Built-in Functions
This approach leverages Java's built-in functions to merge and sort the arrays. The time complexity is \(O((m + n) \log(m + n))\).

```java
import java.util.Arrays;

public class MergeSortedArrayBuiltIn {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        System.arraycopy(nums2, 0, nums1, m, n);
        Arrays.sort(nums1);
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 3, 0, 0, 0};
        int m = 3;
        int[] nums2 = {2, 5, 6};
        int n = 3;
        MergeSortedArrayBuiltIn solution = new MergeSortedArrayBuiltIn();
        solution.merge(nums1, m, nums2, n);
        System.out.println("Merged array: " + Arrays.toString(nums1)); // Output: [1, 2, 2, 3, 5, 6]
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Merge Sorted Array" problem. The two-pointers method from the end is generally preferred due to its efficiency and in-place merging[1](https://leetcode.com/problems/merge-sorted-array/)[2](https://dev.to/rahulgithubweb/leetcode-challenge-merge-sorted-array-top-interview-questions-java-solution-dpa).

Would you like more details on any specific approach?
[1](https://leetcode.com/problems/merge-sorted-array/): [1](https://leetcode.com/problems/merge-sorted-array/)
[2](https://dev.to/rahulgithubweb/leetcode-challenge-merge-sorted-array-top-interview-questions-java-solution-dpa): [2](https://dev.to/rahulgithubweb/leetcode-challenge-merge-sorted-array-top-interview-questions-java-solution-dpa)

## Remove Duplicates from Sorted Array II

The "Remove Duplicates from Sorted Array II" problem on LeetCode requires modifying a sorted array in-place so that each element appears at most twice. Here are different approaches to solve this problem in Java:

### 1. Two Pointers Approach
This approach uses two pointers to keep track of the position in the array where the next unique element should be placed. The time complexity is \(O(n)\).

```java
public class RemoveDuplicates {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 2) return nums.length;

        int k = 2; // Pointer for the position of the next unique element
        for (int i = 2; i < nums.length; i++) {
            if (nums[i] != nums[k - 2]) {
                nums[k++] = nums[i];
            }
        }
        return k;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 1, 2, 2, 3};
        RemoveDuplicates solution = new RemoveDuplicates();
        int newLength = solution.removeDuplicates(nums);
        System.out.println("New length: " + newLength); // Output: 5
        System.out.println("Modified array: " + Arrays.toString(Arrays.copyOf(nums, newLength))); // Output: [1, 1, 2, 2, 3]
    }
}
```

### 2. Optimized Two Pointers Approach
This approach is similar to the first one but includes additional checks to handle edge cases more efficiently. The time complexity remains \(O(n)\).

```java
public class RemoveDuplicatesOptimized {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 2) return nums.length;

        int i = 1; // Pointer for the previous element
        int j = 2; // Pointer for the current element
        while (j < nums.length) {
            if (nums[j] != nums[i] || nums[j] != nums[i - 1]) {
                nums[++i] = nums[j];
            }
            j++;
        }
        return i + 1;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 1, 2, 2, 3};
        RemoveDuplicatesOptimized solution = new RemoveDuplicatesOptimized();
        int newLength = solution.removeDuplicates(nums);
        System.out.println("New length: " + newLength); // Output: 5
        System.out.println("Modified array: " + Arrays.toString(Arrays.copyOf(nums, newLength))); // Output: [1, 1, 2, 2, 3]
    }
}
```

### 3. Brute Force Approach
This approach uses a simple loop to shift elements left whenever an element appears more than twice. The time complexity is \(O(n^2)\).

```java
public class RemoveDuplicatesBruteForce {
    public int removeDuplicates(int[] nums) {
        int n = nums.length;
        if (n <= 2) return n;

        int k = 2; // Pointer for the position of the next unique element
        for (int i = 2; i < n; i++) {
            if (nums[i] != nums[k - 2]) {
                nums[k++] = nums[i];
            }
        }
        return k;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 1, 2, 2, 3};
        RemoveDuplicatesBruteForce solution = new RemoveDuplicatesBruteForce();
        int newLength = solution.removeDuplicates(nums);
        System.out.println("New length: " + newLength); // Output: 5
        System.out.println("Modified array: " + Arrays.toString(Arrays.copyOf(nums, newLength))); // Output: [1, 1, 2, 2, 3]
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Remove Duplicates from Sorted Array II" problem. The two-pointers method is generally preferred due to its efficiency[1](https://algo.monster/liteproblems/80)[2](https://www.programcreek.com/2013/01/leetcode-remove-duplicates-from-sorted-array-ii-java/).

Would you like more details on any specific approach?
[1](https://algo.monster/liteproblems/80): [1](https://algo.monster/liteproblems/80)
[2](https://www.programcreek.com/2013/01/leetcode-remove-duplicates-from-sorted-array-ii-java/): [2](https://www.programcreek.com/2013/01/leetcode-remove-duplicates-from-sorted-array-ii-java/)


## Remove Duplicates from Sorted Array

The "Remove Duplicates from Sorted Array" problem on LeetCode requires modifying a sorted array in-place so that each element appears only once. Here are different approaches to solve this problem in Java:

### 1. Two Pointers Approach
This is the most efficient approach, using two pointers to overwrite the duplicates. The time complexity is \(O(n)\).

```java
public class RemoveDuplicates {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2};
        RemoveDuplicates solution = new RemoveDuplicates();
        int newLength = solution.removeDuplicates(nums);
        System.out.println("New length: " + newLength); // Output: 2
        System.out.println("Modified array: " + Arrays.toString(Arrays.copyOf(nums, newLength))); // Output: [1, 2]
    }
}
```

### 2. Using a Set
This approach uses a `Set` to store unique elements and then copies them back to the array. The time complexity is \(O(n)\), but it requires extra space.

```java
import java.util.*;

public class RemoveDuplicatesWithSet {
    public int removeDuplicates(int[] nums) {
        Set<Integer> set = new LinkedHashSet<>();
        for (int num : nums) {
            set.add(num);
        }
        int i = 0;
        for (int num : set) {
            nums[i++] = num;
        }
        return set.size();
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2};
        RemoveDuplicatesWithSet solution = new RemoveDuplicatesWithSet();
        int newLength = solution.removeDuplicates(nums);
        System.out.println("New length: " + newLength); // Output: 2
        System.out.println("Modified array: " + Arrays.toString(Arrays.copyOf(nums, newLength))); // Output: [1, 2]
    }
}
```

### 3. Using Streams (Java 8+)
This modern approach uses Java Streams to filter out duplicates and then copies the result back to the array. The time complexity is \(O(n)\), but it also requires extra space.

```java
import java.util.*;
import java.util.stream.*;

public class RemoveDuplicatesWithStreams {
    public int removeDuplicates(int[] nums) {
        int[] uniqueNums = Arrays.stream(nums).distinct().toArray();
        System.arraycopy(uniqueNums, 0, nums, 0, uniqueNums.length);
        return uniqueNums.length;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2};
        RemoveDuplicatesWithStreams solution = new RemoveDuplicatesWithStreams();
        int newLength = solution.removeDuplicates(nums);
        System.out.println("New length: " + newLength); // Output: 2
        System.out.println("Modified array: " + Arrays.toString(Arrays.copyOf(nums, newLength))); // Output: [1, 2]
    }
}
```

### 4. Brute Force Approach
This approach uses a simple loop to shift elements left whenever a duplicate is found. The time complexity is \(O(n^2)\).

```java
public class RemoveDuplicatesBruteForce {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int n = nums.length;
        for (int i = 0; i < n - 1; i++) {
            if (nums[i] == nums[i + 1]) {
                for (int j = i + 1; j < n - 1; j++) {
                    nums[j] = nums[j + 1];
                }
                n--;
                i--;
            }
        }
        return n;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2};
        RemoveDuplicatesBruteForce solution = new RemoveDuplicatesBruteForce();
        int newLength = solution.removeDuplicates(nums);
        System.out.println("New length: " + newLength); // Output: 2
        System.out.println("Modified array: " + Arrays.toString(Arrays.copyOf(nums, newLength))); // Output: [1, 2]
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Remove Duplicates from Sorted Array" problem. The two-pointers method is generally preferred due to its efficiency[1](https://www.codementor.io/@noelkamphoa/5-effective-methods-to-remove-array-duplicates-while-preserving-original-order-2bff62aydc)[2](https://www.javaguides.net/2018/08/java-program-to-remove-duplicate.html).

Would you like more details on any specific approach?
[1](https://www.codementor.io/@noelkamphoa/5-effective-methods-to-remove-array-duplicates-while-preserving-original-order-2bff62aydc): [1](https://www.javaguides.net/2023/12/remove-duplicates-from-sorted-array-java.html)
[2](https://www.javaguides.net/2018/08/java-program-to-remove-duplicate.html): [2](https://www.codementor.io/@noelkamphoa/5-effective-methods-to-remove-array-duplicates-while-preserving-original-order-2bff62aydc)

## Majority Element

The "Majority Element" problem involves finding an element in an array that appears more than \( \frac{n}{2} \) times, where \( n \) is the length of the array. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach uses nested loops to count the occurrences of each element. The time complexity is \( O(n^2) \).

```java
public class MajorityElementBruteForce {
    public static Integer findMajorityElement(int[] nums) {
        int majorityThreshold = nums.length / 2;
        for (int i = 0; i < nums.length; i++) {
            int count = 0;
            for (int j = 0; j < nums.length; j++) {
                if (nums[i] == nums[j]) {
                    count++;
                }
            }
            if (count > majorityThreshold) {
                return nums[i];
            }
        }
        return null; // No majority element found
    }

    public static void main(String[] args) {
        int[] nums = {2, 2, 1, 1, 2};
        System.out.println("Majority Element: " + findMajorityElement(nums)); // Output: 2
    }
}
```

### 2. HashMap Approach
This approach uses a `HashMap` to count the occurrences of each element. The time complexity is \( O(n) \), and the space complexity is \( O(n) \).

```java
import java.util.HashMap;

public class MajorityElementHashMap {
    public static Integer findMajorityElement(int[] nums) {
        HashMap<Integer, Integer> counts = new HashMap<>();
        for (int num : nums) {
            counts.put(num, counts.getOrDefault(num, 0) + 1);
        }
        for (Integer key : counts.keySet()) {
            if (counts.get(key) > nums.length / 2) {
                return key;
            }
        }
        return null; // No majority element found
    }

    public static void main(String[] args) {
        int[] nums = {2, 2, 1, 1, 2};
        System.out.println("Majority Element: " + findMajorityElement(nums)); // Output: 2
    }
}
```

### 3. Sorting Approach
This approach sorts the array and then checks the middle element. The time complexity is \( O(n \log n) \).

```java
import java.util.Arrays;

public class MajorityElementSorting {
    public static Integer findMajorityElement(int[] nums) {
        Arrays.sort(nums);
        int candidate = nums[nums.length / 2];
        int count = 0;
        for (int num : nums) {
            if (num == candidate) {
                count++;
            }
        }
        return count > nums.length / 2 ? candidate : null;
    }

    public static void main(String[] args) {
        int[] nums = {2, 2, 1, 1, 2};
        System.out.println("Majority Element: " + findMajorityElement(nums)); // Output: 2
    }
}
```

### 4. Moore's Voting Algorithm
This is an optimal approach with a time complexity of \( O(n) \) and space complexity of \( O(1) \).

```java
public class MajorityElementMooreVoting {
    public static Integer findMajorityElement(int[] nums) {
        int candidate = -1;
        int count = 0;
        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }
        // Verification step
        count = 0;
        for (int num : nums) {
            if (num == candidate) {
                count++;
            }
        }
        return count > nums.length / 2 ? candidate : null;
    }

    public static void main(String[] args) {
        int[] nums = {2, 2, 1, 1, 2};
        System.out.println("Majority Element: " + findMajorityElement(nums)); // Output: 2
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Majority Element" problem. Moore's Voting Algorithm is generally preferred due to its efficiency[1](https://www.baeldung.com/java-array-find-majority-element)[2](https://javanexus.com/blog/solving-majority-element-java-arrays).

Would you like more details on any specific approach?
[1](https://www.baeldung.com/java-array-find-majority-element): [1](https://www.baeldung.com/java-array-find-majority-element)
[2](https://javanexus.com/blog/solving-majority-element-java-arrays): [2](https://javanexus.com/blog/solving-majority-element-java-arrays)


## Rotate Array

Rotating an array involves shifting its elements by a specified number of positions. Here are different approaches to solve the "Rotate Array" problem in Java:

### 1. Brute Force Approach
This approach rotates the array one step at a time. The time complexity is \(O(n \times k)\), where \(n\) is the length of the array and \(k\) is the number of rotations.

```java
public class RotateArrayBruteForce {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        for (int i = 0; i < k; i++) {
            int previous = nums[nums.length - 1];
            for (int j = 0; j < nums.length; j++) {
                int temp = nums[j];
                nums[j] = previous;
                previous = temp;
            }
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5, 6, 7};
        int k = 3;
        RotateArrayBruteForce solution = new RotateArrayBruteForce();
        solution.rotate(nums, k);
        System.out.println("Rotated array: " + Arrays.toString(nums)); // Output: [5, 6, 7, 1, 2, 3, 4]
    }
}
```

### 2. Using Extra Array
This approach uses an extra array to store the rotated elements. The time complexity is \(O(n)\), but it requires \(O(n)\) extra space.

```java
public class RotateArrayExtraArray {
    public void rotate(int[] nums, int k) {
        int[] rotated = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            rotated[(i + k) % nums.length] = nums[i];
        }
        System.arraycopy(rotated, 0, nums, 0, nums.length);
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5, 6, 7};
        int k = 3;
        RotateArrayExtraArray solution = new RotateArrayExtraArray();
        solution.rotate(nums, k);
        System.out.println("Rotated array: " + Arrays.toString(nums)); // Output: [5, 6, 7, 1, 2, 3, 4]
    }
}
```

### 3. Reverse Approach
This approach reverses parts of the array to achieve the rotation. The time complexity is \(O(n)\) and it requires \(O(1)\) extra space.

```java
public class RotateArrayReverse {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5, 6, 7};
        int k = 3;
        RotateArrayReverse solution = new RotateArrayReverse();
        solution.rotate(nums, k);
        System.out.println("Rotated array: " + Arrays.toString(nums)); // Output: [5, 6, 7, 1, 2, 3, 4]
    }
}
```

### 4. Cyclic Replacements
This approach uses cyclic replacements to rotate the array. The time complexity is \(O(n)\) and it requires \(O(1)\) extra space.

```java
public class RotateArrayCyclic {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        int count = 0;
        for (int start = 0; count < nums.length; start++) {
            int current = start;
            int prev = nums[start];
            do {
                int next = (current + k) % nums.length;
                int temp = nums[next];
                nums[next] = prev;
                prev = temp;
                current = next;
                count++;
            } while (start != current);
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5, 6, 7};
        int k = 3;
        RotateArrayCyclic solution = new RotateArrayCyclic();
        solution.rotate(nums, k);
        System.out.println("Rotated array: " + Arrays.toString(nums)); // Output: [5, 6, 7, 1, 2, 3, 4]
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Rotate Array" problem. The reverse method is generally preferred due to its efficiency and in-place rotation[1](https://www.baeldung.com/java-rotate-arrays)[2](https://examples.javacodegeeks.com/rotate-arrays-in-java/).

Would you like more details on any specific approach?
[1](https://www.baeldung.com/java-rotate-arrays): [1](https://www.baeldung.com/java-rotate-arrays)
[2](https://examples.javacodegeeks.com/rotate-arrays-in-java/): [2](https://examples.javacodegeeks.com/rotate-arrays-in-java/)


## Jump Game

The "Jump Game" problem on LeetCode involves determining if you can reach the last index of an array given the maximum jumps at each element. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach tries all possible jumps from each index. The time complexity is \(O(2^n)\), which is inefficient for large arrays.

```java
public class JumpGameBruteForce {
    public boolean canJump(int[] nums) {
        return canJumpFromPosition(0, nums);
    }

    private boolean canJumpFromPosition(int position, int[] nums) {
        if (position == nums.length - 1) {
            return true;
        }
        int furthestJump = Math.min(position + nums[position], nums.length - 1);
        for (int nextPosition = position + 1; nextPosition <= furthestJump; nextPosition++) {
            if (canJumpFromPosition(nextPosition, nums)) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        JumpGameBruteForce solution = new JumpGameBruteForce();
        System.out.println("Can jump: " + solution.canJump(nums)); // Output: true
    }
}
```

### 2. Dynamic Programming Approach
This approach uses a memoization table to store the results of subproblems. The time complexity is \(O(n^2)\).

```java
public class JumpGameDP {
    public boolean canJump(int[] nums) {
        int[] memo = new int[nums.length];
        Arrays.fill(memo, -1);
        memo[nums.length - 1] = 1;
        return canJumpFromPosition(0, nums, memo);
    }

    private boolean canJumpFromPosition(int position, int[] nums, int[] memo) {
        if (memo[position] != -1) {
            return memo[position] == 1;
        }
        int furthestJump = Math.min(position + nums[position], nums.length - 1);
        for (int nextPosition = position + 1; nextPosition <= furthestJump; nextPosition++) {
            if (canJumpFromPosition(nextPosition, nums, memo)) {
                memo[position] = 1;
                return true;
            }
        }
        memo[position] = 0;
        return false;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        JumpGameDP solution = new JumpGameDP();
        System.out.println("Can jump: " + solution.canJump(nums)); // Output: true
    }
}
```

### 3. Greedy Approach
This approach keeps track of the furthest index that can be reached. The time complexity is \(O(n)\).

```java
public class JumpGameGreedy {
    public boolean canJump(int[] nums) {
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
        JumpGameGreedy solution = new JumpGameGreedy();
        System.out.println("Can jump: " + solution.canJump(nums)); // Output: true
    }
}
```

### 4. Backtracking Approach
This approach explores all possible paths using backtracking. The time complexity is \(O(2^n)\), similar to the brute force approach.

```java
public class JumpGameBacktracking {
    public boolean canJump(int[] nums) {
        return canJumpFromPosition(0, nums);
    }

    private boolean canJumpFromPosition(int position, int[] nums) {
        if (position == nums.length - 1) {
            return true;
        }
        int furthestJump = Math.min(position + nums[position], nums.length - 1);
        for (int nextPosition = furthestJump; nextPosition > position; nextPosition--) {
            if (canJumpFromPosition(nextPosition, nums)) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        JumpGameBacktracking solution = new JumpGameBacktracking();
        System.out.println("Can jump: " + solution.canJump(nums)); // Output: true
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Jump Game" problem. The greedy method is generally preferred due to its efficiency[1](https://www.youtube.com/watch?v=Gtugy3mRV-A)[2](https://www.youtube.com/watch?v=XlR0ytsj9JQ).

Would you like more details on any specific approach?
[1](https://www.youtube.com/watch?v=Gtugy3mRV-A): [4](https://www.programcreek.com/2014/03/leetcode-jump-game-java/)
[2](https://www.youtube.com/watch?v=XlR0ytsj9JQ): [5](https://algo.monster/liteproblems/55)

## Jump Game II

The "Jump Game II" problem on LeetCode requires finding the minimum number of jumps to reach the last index of an array. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach tries all possible jumps from each index. The time complexity is \(O(2^n)\), which is inefficient for large arrays.

```java
public class JumpGameIIBruteForce {
    public int jump(int[] nums) {
        return jumpFromPosition(0, nums);
    }

    private int jumpFromPosition(int position, int[] nums) {
        if (position >= nums.length - 1) {
            return 0;
        }
        int furthestJump = Math.min(position + nums[position], nums.length - 1);
        int minJumps = Integer.MAX_VALUE;
        for (int nextPosition = position + 1; nextPosition <= furthestJump; nextPosition++) {
            int jumps = jumpFromPosition(nextPosition, nums);
            if (jumps != Integer.MAX_VALUE) {
                minJumps = Math.min(minJumps, jumps + 1);
            }
        }
        return minJumps;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        JumpGameIIBruteForce solution = new JumpGameIIBruteForce();
        System.out.println("Minimum jumps: " + solution.jump(nums)); // Output: 2
    }
}
```

### 2. Dynamic Programming Approach
This approach uses a memoization table to store the results of subproblems. The time complexity is \(O(n^2)\).

```java
public class JumpGameIIDP {
    public int jump(int[] nums) {
        int[] dp = new int[nums.length];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for (int i = 0; i < nums.length; i++) {
            for (int j = 1; j <= nums[i] && i + j < nums.length; j++) {
                dp[i + j] = Math.min(dp[i + j], dp[i] + 1);
            }
        }
        return dp[nums.length - 1];
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        JumpGameIIDP solution = new JumpGameIIDP();
        System.out.println("Minimum jumps: " + solution.jump(nums)); // Output: 2
    }
}
```

### 3. Greedy Approach
This approach keeps track of the furthest index that can be reached and the end of the current jump range. The time complexity is \(O(n)\).

```java
public class JumpGameIIGreedy {
    public int jump(int[] nums) {
        int jumps = 0, currentEnd = 0, farthest = 0;
        for (int i = 0; i < nums.length - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);
            if (i == currentEnd) {
                jumps++;
                currentEnd = farthest;
            }
        }
        return jumps;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        JumpGameIIGreedy solution = new JumpGameIIGreedy();
        System.out.println("Minimum jumps: " + solution.jump(nums)); // Output: 2
    }
}
```

### 4. Backtracking Approach
This approach explores all possible paths using backtracking. The time complexity is \(O(2^n)\), similar to the brute force approach.

```java
public class JumpGameIIBacktracking {
    public int jump(int[] nums) {
        return jumpFromPosition(0, nums);
    }

    private int jumpFromPosition(int position, int[] nums) {
        if (position >= nums.length - 1) {
            return 0;
        }
        int furthestJump = Math.min(position + nums[position], nums.length - 1);
        int minJumps = Integer.MAX_VALUE;
        for (int nextPosition = furthestJump; nextPosition > position; nextPosition--) {
            int jumps = jumpFromPosition(nextPosition, nums);
            if (jumps != Integer.MAX_VALUE) {
                minJumps = Math.min(minJumps, jumps + 1);
            }
        }
        return minJumps;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, 1, 1, 4};
        JumpGameIIBacktracking solution = new JumpGameIIBacktracking();
        System.out.println("Minimum jumps: " + solution.jump(nums)); // Output: 2
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Jump Game II" problem. The greedy method is generally preferred due to its efficiency[1](https://algo.monster/liteproblems/45)[2](https://dev.to/dhanush9952/jump-game-ii-a-deep-dive-into-leetcodes-classic-algorithm-problem-45i3).

Would you like more details on any specific approach?

## H-Index

The H-Index is a metric used to quantify the productivity and citation impact of a researcher. It measures how many papers (h) have received at least h citations. Here are different approaches to solve the H-Index problem in Java:

### 1. Sorting Approach
This approach sorts the array in descending order and then iterates to find the H-Index. The time complexity is \(O(n \log n)\).

```java
import java.util.Arrays;

public class HIndexSorting {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        int n = citations.length;
        for (int i = 0; i < n; i++) {
            if (citations[i] >= n - i) {
                return n - i;
            }
        }
        return 0;
    }

    public static void main(String[] args) {
        int[] citations = {3, 0, 6, 1, 5};
        HIndexSorting solution = new HIndexSorting();
        System.out.println("H-Index: " + solution.hIndex(citations)); // Output: 3
    }
}
```

### 2. Bucket Sort Approach
This approach uses a bucket sorting technique to count the number of papers with a certain number of citations. The time complexity is \(O(n)\).

```java
public class HIndexBucketSort {
    public int hIndex(int[] citations) {
        int n = citations.length;
        int[] buckets = new int[n + 1];
        for (int citation : citations) {
            if (citation >= n) {
                buckets[n]++;
            } else {
                buckets[citation]++;
            }
        }
        int count = 0;
        for (int i = n; i >= 0; i--) {
            count += buckets[i];
            if (count >= i) {
                return i;
            }
        }
        return 0;
    }

    public static void main(String[] args) {
        int[] citations = {3, 0, 6, 1, 5};
        HIndexBucketSort solution = new HIndexBucketSort();
        System.out.println("H-Index: " + solution.hIndex(citations)); // Output: 3
    }
}
```

### 3. Binary Search Approach
This approach uses binary search to find the H-Index. The time complexity is \(O(n \log n)\).

```java
import java.util.Arrays;

public class HIndexBinarySearch {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        int n = citations.length;
        int left = 0, right = n - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (citations[mid] >= n - mid) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return n - left;
    }

    public static void main(String[] args) {
        int[] citations = {3, 0, 6, 1, 5};
        HIndexBinarySearch solution = new HIndexBinarySearch();
        System.out.println("H-Index: " + solution.hIndex(citations)); // Output: 3
    }
}
```

These approaches cover the basic and more optimized ways to solve the H-Index problem. The bucket sort method is generally preferred due to its efficiency[1](https://codencofe.blogspot.com/2024/09/finding-h-index-in-java-simple-vs.html)[2](https://algo.monster/liteproblems/274).

Would you like more details on any specific approach?
[1](https://codencofe.blogspot.com/2024/09/finding-h-index-in-java-simple-vs.html): [1](https://codencofe.blogspot.com/2024/09/finding-h-index-in-java-simple-vs.html)
[2](https://algo.monster/liteproblems/274): [2](https://algo.monster/liteproblems/274)

## Insert Delete GetRandom O(1)

The "Insert Delete GetRandom O(1)" problem on LeetCode requires designing a data structure that supports inserting, deleting, and getting a random element in constant time. Here are different approaches to solve this problem in Java:

### 1. Using HashMap and ArrayList
This approach uses a `HashMap` to store the value-to-index mapping and an `ArrayList` to store the values. The time complexity for all operations is \(O(1)\).

```java
import java.util.*;

public class RandomizedSet {
    private Map<Integer, Integer> valueToIndex;
    private List<Integer> values;
    private Random random;

    /** Initialize your data structure here. */
    public RandomizedSet() {
        valueToIndex = new HashMap<>();
        values = new ArrayList<>();
        random = new Random();
    }

    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        if (valueToIndex.containsKey(val)) {
            return false;
        }
        valueToIndex.put(val, values.size());
        values.add(val);
        return true;
    }

    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        if (!valueToIndex.containsKey(val)) {
            return false;
        }
        int index = valueToIndex.get(val);
        int lastElement = values.get(values.size() - 1);
        values.set(index, lastElement);
        valueToIndex.put(lastElement, index);
        values.remove(values.size() - 1);
        valueToIndex.remove(val);
        return true;
    }

    /** Get a random element from the set. */
    public int getRandom() {
        return values.get(random.nextInt(values.size()));
    }

    public static void main(String[] args) {
        RandomizedSet randomizedSet = new RandomizedSet();
        System.out.println(randomizedSet.insert(1)); // true
        System.out.println(randomizedSet.remove(2)); // false
        System.out.println(randomizedSet.insert(2)); // true
        System.out.println(randomizedSet.getRandom()); // 1 or 2
        System.out.println(randomizedSet.remove(1)); // true
        System.out.println(randomizedSet.insert(2)); // false
        System.out.println(randomizedSet.getRandom()); // 2
    }
}
```

### 2. Using Two HashMaps
This approach uses two `HashMaps` to store the value-to-index and index-to-value mappings. The time complexity for all operations is \(O(1)\).

```java
import java.util.*;

public class RandomizedSetTwoMaps {
    private Map<Integer, Integer> valueToIndex;
    private Map<Integer, Integer> indexToValue;
    private Random random;

    /** Initialize your data structure here. */
    public RandomizedSetTwoMaps() {
        valueToIndex = new HashMap<>();
        indexToValue = new HashMap<>();
        random = new Random();
    }

    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        if (valueToIndex.containsKey(val)) {
            return false;
        }
        int index = valueToIndex.size();
        valueToIndex.put(val, index);
        indexToValue.put(index, val);
        return true;
    }

    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        if (!valueToIndex.containsKey(val)) {
            return false;
        }
        int index = valueToIndex.get(val);
        int lastIndex = valueToIndex.size() - 1;
        int lastValue = indexToValue.get(lastIndex);

        valueToIndex.put(lastValue, index);
        indexToValue.put(index, lastValue);

        valueToIndex.remove(val);
        indexToValue.remove(lastIndex);
        return true;
    }

    /** Get a random element from the set. */
    public int getRandom() {
        int randomIndex = random.nextInt(valueToIndex.size());
        return indexToValue.get(randomIndex);
    }

    public static void main(String[] args) {
        RandomizedSetTwoMaps randomizedSet = new RandomizedSetTwoMaps();
        System.out.println(randomizedSet.insert(1)); // true
        System.out.println(randomizedSet.remove(2)); // false
        System.out.println(randomizedSet.insert(2)); // true
        System.out.println(randomizedSet.getRandom()); // 1 or 2
        System.out.println(randomizedSet.remove(1)); // true
        System.out.println(randomizedSet.insert(2)); // false
        System.out.println(randomizedSet.getRandom()); // 2
    }
}
```

### 3. Using HashMap and LinkedList
This approach uses a `HashMap` to store the value-to-index mapping and a `LinkedList` to store the values. The time complexity for all operations is \(O(1)\).

```java
import java.util.*;

public class RandomizedSetLinkedList {
    private Map<Integer, Integer> valueToIndex;
    private List<Integer> values;
    private Random random;

    /** Initialize your data structure here. */
    public RandomizedSetLinkedList() {
        valueToIndex = new HashMap<>();
        values = new LinkedList<>();
        random = new Random();
    }

    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        if (valueToIndex.containsKey(val)) {
            return false;
        }
        valueToIndex.put(val, values.size());
        values.add(val);
        return true;
    }

    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        if (!valueToIndex.containsKey(val)) {
            return false;
        }
        int index = valueToIndex.get(val);
        int lastElement = values.get(values.size() - 1);
        values.set(index, lastElement);
        valueToIndex.put(lastElement, index);
        values.remove(values.size() - 1);
        valueToIndex.remove(val);
        return true;
    }

    /** Get a random element from the set. */
    public int getRandom() {
        return values.get(random.nextInt(values.size()));
    }

    public static void main(String[] args) {
        RandomizedSetLinkedList randomizedSet = new RandomizedSetLinkedList();
        System.out.println(randomizedSet.insert(1)); // true
        System.out.println(randomizedSet.remove(2)); // false
        System.out.println(randomizedSet.insert(2)); // true
        System.out.println(randomizedSet.getRandom()); // 1 or 2
        System.out.println(randomizedSet.remove(1)); // true
        System.out.println(randomizedSet.insert(2)); // false
        System.out.println(randomizedSet.getRandom()); // 2
    }
}
```

These approaches cover the basic and more optimized ways to solve the "Insert Delete GetRandom O(1)" problem. The HashMap and ArrayList method is generally preferred due to its efficiency[1](https://www.programcreek.com/2014/08/leetcode-insert-delete-getrandom-o1-java/)[2](https://www.programcreek.com/2014/08/leetcode-insert-delete-getrandom-o1-duplicates-allowed-java/).

Would you like more details on any specific approach?
[1](https://www.programcreek.com/2014/08/leetcode-insert-delete-getrandom-o1-java/): [1](https://www.programcreek.com/2014/08/leetcode-insert-delete-getrandom-o1-java/)
[2](https://www.programcreek.com/2014/08/leetcode-insert-delete-getrandom-o1-duplicates-allowed-java/): [2](https://tutorialcup.com/leetcode-solutions/insert-delete-getrandom-o1-leetcode-solution.htm)


## Sort 0 1 2 (DNF - Dutch National Flag)

Sure! Sorting an array containing only 0s, 1s, and 2s can be done using several approaches in Java. Here are a few methods:

### 1. Counting Sort
This approach counts the number of 0s, 1s, and 2s, and then reconstructs the array.

```java
public void sortColors(int[] nums) {
    int count0 = 0, count1 = 0, count2 = 0;
    for (int num : nums) {
        if (num == 0) count0++;
        else if (num == 1) count1++;
        else count2++;
    }
    int index = 0;
    while (count0-- > 0) nums[index++] = 0;
    while (count1-- > 0) nums[index++] = 1;
    while (count2-- > 0) nums[index++] = 2;
}
```

### 2. Dutch National Flag Algorithm
This is a single-pass algorithm with constant space complexity.

```java
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
```

### 3. Two-Pass Algorithm
This approach first moves all 0s to the beginning and then all 2s to the end.

```java
public void sortColors(int[] nums) {
    int n = nums.length;
    int index = 0;
    for (int i = 0; i < n; i++) {
        if (nums[i] == 0) {
            nums[index++] = 0;
        }
    }
    for (int i = 0; i < n; i++) {
        if (nums[i] == 1) {
            nums[index++] = 1;
        }
    }
    while (index < n) {
        nums[index++] = 2;
    }
}
```

Each of these methods has its own advantages. The Counting Sort is simple and easy to understand, the Dutch National Flag Algorithm is efficient with a single pass, and the Two-Pass Algorithm is straightforward but requires two passes through the array.

Which approach do you find most interesting?


## Move all the negative elements to one side of the array

Certainly! Moving all negative elements to one side of an array can be done using several approaches in Java. Here are a few methods:

### 1. Two-Pointer Approach
This approach uses two pointers to partition the array in a single pass.

```java
public void moveNegativesToOneSide(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        if (nums[left] < 0) {
            left++;
        } else if (nums[right] >= 0) {
            right--;
        } else {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
}
```

### 2. Partition Process of QuickSort
This method is similar to the partition process of the QuickSort algorithm.

```java
public void moveNegativesToOneSide(int[] nums) {
    int j = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] < 0) {
            if (i != j) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }
            j++;
        }
    }
}
```

### 3. Using Extra Space
This approach uses an additional array to store the result.

```java
public void moveNegativesToOneSide(int[] nums) {
    int[] result = new int[nums.length];
    int index = 0;
    for (int num : nums) {
        if (num < 0) {
            result[index++] = num;
        }
    }
    for (int num : nums) {
        if (num >= 0) {
            result[index++] = num;
        }
    }
    System.arraycopy(result, 0, nums, 0, nums.length);
}
```

### 4. Using Collections
This approach leverages Java Collections to achieve the same result.

```java
import java.util.*;

public void moveNegativesToOneSide(int[] nums) {
    List<Integer> negatives = new ArrayList<>();
    List<Integer> nonNegatives = new ArrayList<>();
    for (int num : nums) {
        if (num < 0) {
            negatives.add(num);
        } else {
            nonNegatives.add(num);
        }
    }
    int index = 0;
    for (int num : negatives) {
        nums[index++] = num;
    }
    for (int num : nonNegatives) {
        nums[index++] = num;
    }
}
```

Each of these methods has its own advantages. The Two-Pointer Approach is efficient with a single pass, the QuickSort Partition Process is straightforward, the Extra Space method is simple but uses additional memory, and the Collections method is easy to understand and implement.

Which approach do you find most suitable for your needs?

## Rearrange Postive and Negative alternatively element in array

Certainly! Placing positive and negative elements alternately in an array can be done using several approaches in Java. Here are a few methods:

### 1. Using Extra Space
This approach uses two separate arrays to store positive and negative numbers and then merges them alternately.

```java
public void rearrangeAlternately(int[] nums) {
    int[] positives = Arrays.stream(nums).filter(x -> x >= 0).toArray();
    int[] negatives = Arrays.stream(nums).filter(x -> x < 0).toArray();
    
    int posIndex = 0, negIndex = 0, index = 0;
    while (posIndex < positives.length && negIndex < negatives.length) {
        nums[index++] = positives[posIndex++];
        nums[index++] = negatives[negIndex++];
    }
    while (posIndex < positives.length) {
        nums[index++] = positives[posIndex++];
    }
    while (negIndex < negatives.length) {
        nums[index++] = negatives[negIndex++];
    }
}
```

### 2. In-Place Rearrangement
This approach rearranges the elements in place without using extra space.

```java
public void rearrangeAlternately(int[] nums) {
    int n = nums.length;
    int i = -1, temp = 0;
    for (int j = 0; j < n; j++) {
        if (nums[j] < 0) {
            i++;
            temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
    }
    
    int pos = i + 1, neg = 0;
    while (pos < n && neg < pos && nums[neg] < 0) {
        temp = nums[neg];
        nums[neg] = nums[pos];
        nums[pos] = temp;
        pos++;
        neg += 2;
    }
}
```

### 3. Using Collections
This approach leverages Java Collections to achieve the same result.

```java
import java.util.*;

public void rearrangeAlternately(int[] nums) {
    List<Integer> positives = new ArrayList<>();
    List<Integer> negatives = new ArrayList<>();
    for (int num : nums) {
        if (num >= 0) {
            positives.add(num);
        } else {
            negatives.add(num);
        }
    }
    
    int posIndex = 0, negIndex = 0, index = 0;
    while (posIndex < positives.size() && negIndex < negatives.size()) {
        nums[index++] = positives.get(posIndex++);
        nums[index++] = negatives.get(negIndex++);
    }
    while (posIndex < positives.size()) {
        nums[index++] = positives.get(posIndex++);
    }
    while (negIndex < negatives.size()) {
        nums[index++] = negatives.get(negIndex++);
    }
}
```

### 4. Two-Pointer Approach
This approach uses two pointers to rearrange the elements alternately.

```java
public void rearrangeAlternately(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    int posIndex = 0, negIndex = 1;
    
    for (int num : nums) {
        if (num >= 0 && posIndex < n) {
            result[posIndex] = num;
            posIndex += 2;
        } else if (num < 0 && negIndex < n) {
            result[negIndex] = num;
            negIndex += 2;
        }
    }
    
    for (int i = 0; i < n; i++) {
        nums[i] = result[i];
    }
}
```

Each of these methods has its own advantages. The Extra Space method is simple but uses additional memory, the In-Place Rearrangement is efficient with no extra space, the Collections method is easy to understand, and the Two-Pointer Approach is straightforward and efficient.

Which approach do you find most suitable for your needs?

# Median of 2 sorted arrays of equal size

Finding the median of two sorted arrays of equal size can be done using several approaches in Java. Here are a few methods:

### 1. Merge and Find Median
This approach merges the two arrays and then finds the median.

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int[] merged = new int[nums1.length + nums2.length];
    int i = 0, j = 0, k = 0;
    
    while (i < nums1.length && j < nums2.length) {
        if (nums1[i] < nums2[j]) {
            merged[k++] = nums1[i++];
        } else {
            merged[k++] = nums2[j++];
        }
    }
    
    while (i < nums1.length) {
        merged[k++] = nums1[i++];
    }
    
    while (j < nums2.length) {
        merged[k++] = nums2[j++];
    }
    
    int n = merged.length;
    return (merged[n / 2 - 1] + merged[n / 2]) / 2.0;
}
```

### 2. Binary Search Approach
This approach uses binary search to find the median in logarithmic time complexity.

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int n = nums1.length;
    return findMedianUtil(nums1, nums2, 0, n - 1, 0, n - 1);
}

private double findMedianUtil(int[] nums1, int[] nums2, int startA, int endA, int startB, int endB) {
    if (endA - startA == 1) {
        return (Math.max(nums1[startA], nums2[startB]) + Math.min(nums1[endA], nums2[endB])) / 2.0;
    }
    
    int m1 = median(nums1, startA, endA);
    int m2 = median(nums2, startB, endB);
    
    if (m1 == m2) {
        return m1;
    }
    
    if (m1 < m2) {
        return findMedianUtil(nums1, nums2, (endA + startA + 1) / 2, endA, startB, (endB + startB + 1) / 2);
    } else {
        return findMedianUtil(nums1, nums2, startA, (endA + startA + 1) / 2, (endB + startB + 1) / 2, endB);
    }
}

private int median(int[] nums, int start, int end) {
    int n = end - start + 1;
    if (n % 2 == 0) {
        return (nums[start + n / 2] + nums[start + n / 2 - 1]) / 2;
    } else {
        return nums[start + n / 2];
    }
}
```

### 3. Using Two Pointers
This approach uses two pointers to find the median without merging the arrays.

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int n = nums1.length;
    int medianIndex1 = n - 1;
    int medianIndex2 = n;
    
    int i = 0, j = 0, count = 0;
    int median1 = 0, median2 = 0;
    
    while (count <= medianIndex2) {
        int num;
        if (i < n && (j >= n || nums1[i] < nums2[j])) {
            num = nums1[i++];
        } else {
            num = nums2[j++];
        }
        
        if (count == medianIndex1) {
            median1 = num;
        }
        if (count == medianIndex2) {
            median2 = num;
        }
        count++;
    }
    
    return (median1 + median2) / 2.0;
}
```

Each of these methods has its own advantages. The Merge and Find Median approach is simple but has a higher time complexity, the Binary Search approach is efficient with logarithmic time complexity, and the Two Pointers approach is straightforward and avoids merging the arrays.

Which approach do you find most suitable for your needs?

## Median of 2 sorted arrays of different size

Finding the median of two sorted arrays of different sizes can be done using several approaches in Java. Here are a few methods:

### 1. Merge and Find Median
This approach merges the two arrays and then finds the median.

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int[] merged = new int[nums1.length + nums2.length];
    int i = 0, j = 0, k = 0;
    
    while (i < nums1.length && j < nums2.length) {
        if (nums1[i] < nums2[j]) {
            merged[k++] = nums1[i++];
        } else {
            merged[k++] = nums2[j++];
        }
    }
    
    while (i < nums1.length) {
        merged[k++] = nums1[i++];
    }
    
    while (j < nums2.length) {
        merged[k++] = nums2[j++];
    }
    
    int n = merged.length;
    if (n % 2 == 0) {
        return (merged[n / 2 - 1] + merged[n / 2]) / 2.0;
    } else {
        return merged[n / 2];
    }
}
```

### 2. Binary Search Approach
This approach uses binary search to find the median in logarithmic time complexity.

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    if (nums1.length > nums2.length) {
        return findMedianSortedArrays(nums2, nums1);
    }
    
    int x = nums1.length;
    int y = nums2.length;
    int low = 0, high = x;
    
    while (low <= high) {
        int partitionX = (low + high) / 2;
        int partitionY = (x + y + 1) / 2 - partitionX;
        
        int maxX = (partitionX == 0) ? Integer.MIN_VALUE : nums1[partitionX - 1];
        int maxY = (partitionY == 0) ? Integer.MIN_VALUE : nums2[partitionY - 1];
        
        int minX = (partitionX == x) ? Integer.MAX_VALUE : nums1[partitionX];
        int minY = (partitionY == y) ? Integer.MAX_VALUE : nums2[partitionY];
        
        if (maxX <= minY && maxY <= minX) {
            if ((x + y) % 2 == 0) {
                return (Math.max(maxX, maxY) + Math.min(minX, minY)) / 2.0;
            } else {
                return Math.max(maxX, maxY);
            }
        } else if (maxX > minY) {
            high = partitionX - 1;
        } else {
            low = partitionX + 1;
        }
    }
    
    throw new IllegalArgumentException();
}
```

### 3. Using Two Pointers
This approach uses two pointers to find the median without merging the arrays.

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int m = nums1.length;
    int n = nums2.length;
    int totalLength = m + n;
    int medianIndex1 = (totalLength - 1) / 2;
    int medianIndex2 = totalLength / 2;
    
    int i = 0, j = 0, count = 0;
    int median1 = 0, median2 = 0;
    
    while (count <= medianIndex2) {
        int num;
        if (i < m && (j >= n || nums1[i] < nums2[j])) {
            num = nums1[i++];
        } else {
            num = nums2[j++];
        }
        
        if (count == medianIndex1) {
            median1 = num;
        }
        if (count == medianIndex2) {
            median2 = num;
        }
        count++;
    }
    
    return (median1 + median2) / 2.0;
}
```

Each of these methods has its own advantages. The Merge and Find Median approach is simple but has a higher time complexity, the Binary Search approach is efficient with logarithmic time complexity, and the Two Pointers approach is straightforward and avoids merging the arrays.

Which approach do you find most suitable for your needs?

## Minimum no. of operations required to make an array palindrome

Making an array a palindrome involves ensuring that the array reads the same forwards and backwards. Here are a few approaches to find the minimum number of operations required to achieve this in Java:

### 1. Two-Pointer Approach
This approach uses two pointers to compare elements from both ends of the array and counts the necessary operations.

```java
public int minOperationsToMakePalindrome(int[] nums) {
    int left = 0, right = nums.length - 1;
    int operations = 0;
    
    while (left < right) {
        if (nums[left] != nums[right]) {
            operations++;
        }
        left++;
        right--;
    }
    
    return operations;
}
```

### 2. Dynamic Programming
This approach uses dynamic programming to find the minimum number of operations.

```java
public int minOperationsToMakePalindrome(int[] nums) {
    int n = nums.length;
    int[][] dp = new int[n][n];
    
    for (int len = 2; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (nums[i] == nums[j]) {
                dp[i][j] = dp[i + 1][j - 1];
            } else {
                dp[i][j] = Math.min(dp[i + 1][j], dp[i][j - 1]) + 1;
            }
        }
    }
    
    return dp[0][n - 1];
}
```

### 3. Recursive Approach
This approach uses recursion to find the minimum number of operations.

```java
public int minOperationsToMakePalindrome(int[] nums) {
    return minOperations(nums, 0, nums.length - 1);
}

private int minOperations(int[] nums, int left, int right) {
    if (left >= right) {
        return 0;
    }
    if (nums[left] == nums[right]) {
        return minOperations(nums, left + 1, right - 1);
    }
    return Math.min(minOperations(nums, left + 1, right), minOperations(nums, left, right - 1)) + 1;
}
```

### 4. Greedy Approach
This approach uses a greedy algorithm to minimize the number of operations.

```java
public int minOperationsToMakePalindrome(int[] nums) {
    int left = 0, right = nums.length - 1;
    int operations = 0;
    
    while (left < right) {
        if (nums[left] != nums[right]) {
            if (nums[left] < nums[right]) {
                nums[left + 1] += nums[left];
                left++;
            } else {
                nums[right - 1] += nums[right];
                right--;
            }
            operations++;
        } else {
            left++;
            right--;
        }
    }
    
    return operations;
}
```

Each of these methods has its own advantages. The Two-Pointer Approach is simple and efficient, the Dynamic Programming approach is more comprehensive but uses extra space, the Recursive Approach is elegant but may have higher time complexity, and the Greedy Approach is straightforward and efficient.

Which approach do you find most suitable for your needs?

## Three-way partitioning of an array around a given value

Three-way partitioning of an array around a given value involves rearranging the array such that all elements less than the given value come first, followed by elements equal to the value, and then elements greater than the value. Here are a few approaches in Java:

### 1. Dutch National Flag Algorithm
This approach is efficient and uses a single pass through the array.

```java
public void threeWayPartition(int[] nums, int pivot) {
    int low = 0, mid = 0, high = nums.length - 1;
    while (mid <= high) {
        if (nums[mid] < pivot) {
            swap(nums, low++, mid++);
        } else if (nums[mid] > pivot) {
            swap(nums, mid, high--);
        } else {
            mid++;
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

### 2. Two-Pass Approach
This approach uses two passes to partition the array.

```java
public void threeWayPartition(int[] nums, int pivot) {
    int n = nums.length;
    int[] temp = new int[n];
    int index = 0;
    
    // First pass: elements less than pivot
    for (int num : nums) {
        if (num < pivot) {
            temp[index++] = num;
        }
    }
    
    // Second pass: elements equal to pivot
    for (int num : nums) {
        if (num == pivot) {
            temp[index++] = num;
        }
    }
    
    // Third pass: elements greater than pivot
    for (int num : nums) {
        if (num > pivot) {
            temp[index++] = num;
        }
    }
    
    // Copy back to original array
    System.arraycopy(temp, 0, nums, 0, n);
}
```

### 3. Using Collections
This approach leverages Java Collections to achieve the same result.

```java
import java.util.*;

public void threeWayPartition(int[] nums, int pivot) {
    List<Integer> less = new ArrayList<>();
    List<Integer> equal = new ArrayList<>();
    List<Integer> greater = new ArrayList<>();
    
    for (int num : nums) {
        if (num < pivot) {
            less.add(num);
        } else if (num == pivot) {
            equal.add(num);
        } else {
            greater.add(num);
        }
    }
    
    int index = 0;
    for (int num : less) {
        nums[index++] = num;
    }
    for (int num : equal) {
        nums[index++] = num;
    }
    for (int num : greater) {
        nums[index++] = num;
    }
}
```

### 4. In-Place Partitioning
This approach partitions the array in place without using extra space.

```java
public void threeWayPartition(int[] nums, int pivot) {
    int start = 0, end = nums.length - 1;
    
    for (int i = 0; i <= end;) {
        if (nums[i] < pivot) {
            swap(nums, i++, start++);
        } else if (nums[i] > pivot) {
            swap(nums, i, end--);
        } else {
            i++;
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

Each of these methods has its own advantages. The Dutch National Flag Algorithm is efficient with a single pass, the Two-Pass Approach is straightforward but uses extra space, the Collections method is easy to understand, and the In-Place Partitioning is efficient and uses no extra space.

Which approach do you find most suitable for your needs?

## Smallest Subarray with sum greater than a given value

Finding the smallest subarray with a sum greater than a given value can be done using several approaches in Java. Here are a few methods:

### 1. Sliding Window Approach
This approach uses a sliding window to find the smallest subarray.

```java
public int smallestSubarrayWithSum(int[] nums, int target) {
    int n = nums.length;
    int minLength = n + 1;
    int start = 0, end = 0, currentSum = 0;
    
    while (end < n) {
        while (currentSum <= target && end < n) {
            currentSum += nums[end++];
        }
        
        while (currentSum > target && start < n) {
            minLength = Math.min(minLength, end - start);
            currentSum -= nums[start++];
        }
    }
    
    return (minLength == n + 1) ? 0 : minLength;
}
```

### 2. Brute Force Approach
This approach checks all possible subarrays to find the smallest one.

```java
public int smallestSubarrayWithSum(int[] nums, int target) {
    int n = nums.length;
    int minLength = n + 1;
    
    for (int start = 0; start < n; start++) {
        int currentSum = nums[start];
        if (currentSum > target) {
            return 1;
        }
        
        for (int end = start + 1; end < n; end++) {
            currentSum += nums[end];
            if (currentSum > target && (end - start + 1) < minLength) {
                minLength = end - start + 1;
            }
        }
    }
    
    return (minLength == n + 1) ? 0 : minLength;
}
```

### 3. Prefix Sum and Binary Search
This approach uses prefix sums and binary search to find the smallest subarray.

```java
import java.util.*;

public int smallestSubarrayWithSum(int[] nums, int target) {
    int n = nums.length;
    int[] prefixSums = new int[n + 1];
    for (int i = 0; i < n; i++) {
        prefixSums[i + 1] = prefixSums[i] + nums[i];
    }
    
    int minLength = n + 1;
    for (int i = 0; i <= n; i++) {
        int toFind = prefixSums[i] + target;
        int bound = Arrays.binarySearch(prefixSums, toFind);
        if (bound < 0) {
            bound = -bound - 1;
        }
        if (bound <= n) {
            minLength = Math.min(minLength, bound - i);
        }
    }
    
    return (minLength == n + 1) ? 0 : minLength;
}
```

### 4. Deque Approach
This approach uses a deque to maintain a window of indices.

```java
import java.util.*;

public int smallestSubarrayWithSum(int[] nums, int target) {
    int n = nums.length;
    int[] prefixSums = new int[n + 1];
    for (int i = 0; i < n; i++) {
        prefixSums[i + 1] = prefixSums[i] + nums[i];
    }
    
    int minLength = n + 1;
    Deque<Integer> deque = new LinkedList<>();
    
    for (int i = 0; i <= n; i++) {
        while (!deque.isEmpty() && prefixSums[i] - prefixSums[deque.peekFirst()] > target) {
            minLength = Math.min(minLength, i - deque.pollFirst());
        }
        while (!deque.isEmpty() && prefixSums[i] <= prefixSums[deque.peekLast()]) {
            deque.pollLast();
        }
        deque.offerLast(i);
    }
    
    return (minLength == n + 1) ? 0 : minLength;
}
```

Each of these methods has its own advantages. The Sliding Window Approach is efficient and straightforward, the Brute Force Approach is simple but less efficient, the Prefix Sum and Binary Search approach is more advanced and efficient, and the Deque Approach is also efficient and handles the problem well.

Which approach do you find most suitable for your needs?

## Find whether an array is a subset of another array

Determining whether one array is a subset of another can be done using several approaches in Java. Here are a few methods:

### 1. Using HashSet
This approach uses a HashSet to check for the presence of elements.

```java
import java.util.HashSet;

public boolean isSubset(int[] arr1, int[] arr2) {
    HashSet<Integer> set = new HashSet<>();
    for (int num : arr1) {
        set.add(num);
    }
    for (int num : arr2) {
        if (!set.contains(num)) {
            return false;
        }
    }
    return true;
}
```

### 2. Sorting and Merging
This approach sorts both arrays and then uses a merging technique to check for subset.

```java
import java.util.Arrays;

public boolean isSubset(int[] arr1, int[] arr2) {
    Arrays.sort(arr1);
    Arrays.sort(arr2);
    int i = 0, j = 0;
    while (i < arr1.length && j < arr2.length) {
        if (arr1[i] < arr2[j]) {
            i++;
        } else if (arr1[i] == arr2[j]) {
            i++;
            j++;
        } else {
            return false;
        }
    }
    return j == arr2.length;
}
```

### 3. Using Frequency Count
This approach uses frequency counts to check for the presence of elements.

```java
import java.util.HashMap;

public boolean isSubset(int[] arr1, int[] arr2) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int num : arr1) {
        map.put(num, map.getOrDefault(num, 0) + 1);
    }
    for (int num : arr2) {
        if (!map.containsKey(num) || map.get(num) == 0) {
            return false;
        }
        map.put(num, map.get(num) - 1);
    }
    return true;
}
```

### 4. Using Binary Search
This approach uses binary search after sorting the larger array.

```java
import java.util.Arrays;

public boolean isSubset(int[] arr1, int[] arr2) {
    Arrays.sort(arr1);
    for (int num : arr2) {
        if (Arrays.binarySearch(arr1, num) < 0) {
            return false;
        }
    }
    return true;
}
```

Each of these methods has its own advantages. The HashSet approach is efficient and straightforward, the Sorting and Merging approach is intuitive, the Frequency Count approach is useful for handling duplicates, and the Binary Search approach is efficient for large arrays.

Which approach do you find most suitable for your needs?

## Given an array of size n and a number k, find all elements that appear more than " n/k " times. - Majority Element II

Finding the majority element in an array where the element appears more than ⌊n/3⌋ times can be done using several approaches in Java. Here are a few methods:

### 1. Using HashMap
This approach uses a HashMap to count the frequency of each element.

```java
import java.util.*;

public List<Integer> majorityElement(int[] nums) {
    List<Integer> result = new ArrayList<>();
    Map<Integer, Integer> map = new HashMap<>();
    int n = nums.length;
    
    for (int num : nums) {
        map.put(num, map.getOrDefault(num, 0) + 1);
    }
    
    for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
        if (entry.getValue() > n / 3) {
            result.add(entry.getKey());
        }
    }
    
    return result;
}
```

### 2. Boyer-Moore Voting Algorithm
This approach uses the Boyer-Moore Voting Algorithm to find the majority elements.

```java
import java.util.*;

public List<Integer> majorityElement(int[] nums) {
    List<Integer> result = new ArrayList<>();
    if (nums == null || nums.length == 0) return result;
    
    int candidate1 = 0, candidate2 = 0, count1 = 0, count2 = 0;
    
    for (int num : nums) {
        if (num == candidate1) {
            count1++;
        } else if (num == candidate2) {
            count2++;
        } else if (count1 == 0) {
            candidate1 = num;
            count1 = 1;
        } else if (count2 == 0) {
            candidate2 = num;
            count2 = 1;
        } else {
            count1--;
            count2--;
        }
    }
    
    count1 = 0;
    count2 = 0;
    
    for (int num : nums) {
        if (num == candidate1) {
            count1++;
        } else if (num == candidate2) {
            count2++;
        }
    }
    
    if (count1 > nums.length / 3) result.add(candidate1);
    if (count2 > nums.length / 3) result.add(candidate2);
    
    return result;
}
```

### 3. Sorting and Counting
This approach sorts the array and then counts the frequency of each element.

```java
import java.util.*;

public List<Integer> majorityElement(int[] nums) {
    List<Integer> result = new ArrayList<>();
    Arrays.sort(nums);
    int n = nums.length;
    int count = 1;
    
    for (int i = 1; i < n; i++) {
        if (nums[i] == nums[i - 1]) {
            count++;
        } else {
            if (count > n / 3) {
                result.add(nums[i - 1]);
            }
            count = 1;
        }
    }
    
    if (count > n / 3) {
        result.add(nums[n - 1]);
    }
    
    return result;
}
```

### 4. Using Frequency Array
This approach uses a frequency array to count the occurrences of each element.

```java
import java.util.*;

public List<Integer> majorityElement(int[] nums) {
    List<Integer> result = new ArrayList<>();
    int n = nums.length;
    int[] freq = new int[200001];
    
    for (int num : nums) {
        freq[num + 100000]++;
    }
    
    for (int i = 0; i < freq.length; i++) {
        if (freq[i] > n / 3) {
            result.add(i - 100000);
        }
    }
    
    return result;
}
```

Each of these methods has its own advantages. The HashMap approach is straightforward and easy to implement, the Boyer-Moore Voting Algorithm is efficient with linear time complexity, the Sorting and Counting approach is intuitive, and the Frequency Array approach is simple but uses extra space.

Which approach do you find most suitable for your needs?

## 4 Sum

Finding all unique quadruplets in an array that sum up to a given target can be done using several approaches in Java. Here are a few methods:

### 1. Using HashMap
This approach uses a HashMap to store pairs of numbers and their sums.

```java
import java.util.*;

public List<List<Integer>> fourSum(int[] nums, int target) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length < 4) return result;
    
    Arrays.sort(nums);
    Map<Integer, List<int[]>> map = new HashMap<>();
    
    for (int i = 0; i < nums.length - 1; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            int sum = nums[i] + nums[j];
            if (!map.containsKey(sum)) {
                map.put(sum, new ArrayList<>());
            }
            map.get(sum).add(new int[]{i, j});
        }
    }
    
    for (int i = 0; i < nums.length - 1; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            int sum = target - nums[i] - nums[j];
            if (map.containsKey(sum)) {
                for (int[] pair : map.get(sum)) {
                    if (pair[0] > j) {
                        List<Integer> quad = Arrays.asList(nums[i], nums[j], nums[pair[0]], nums[pair[1]]);
                        if (!result.contains(quad)) {
                            result.add(quad);
                        }
                    }
                }
            }
        }
    }
    
    return result;
}
```

### 2. Two-Pointer Approach
This approach uses sorting and two pointers to find the quadruplets.

```java
import java.util.*;

public List<List<Integer>> fourSum(int[] nums, int target) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length < 4) return result;
    
    Arrays.sort(nums);
    
    for (int i = 0; i < nums.length - 3; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        for (int j = i + 1; j < nums.length - 2; j++) {
            if (j > i + 1 && nums[j] == nums[j - 1]) continue;
            int left = j + 1, right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[j] + nums[left] + nums[right];
                if (sum == target) {
                    result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
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
```

### 3. Recursive Approach
This approach uses recursion to find the quadruplets.

```java
import java.util.*;

public List<List<Integer>> fourSum(int[] nums, int target) {
    Arrays.sort(nums);
    return kSum(nums, target, 4, 0);
}

private List<List<Integer>> kSum(int[] nums, int target, int k, int start) {
    List<List<Integer>> result = new ArrayList<>();
    if (start == nums.length || nums[start] * k > target || target > nums[nums.length - 1] * k) {
        return result;
    }
    if (k == 2) {
        return twoSum(nums, target, start);
    }
    for (int i = start; i < nums.length; i++) {
        if (i == start || nums[i] != nums[i - 1]) {
            for (List<Integer> subset : kSum(nums, target - nums[i], k - 1, i + 1)) {
                result.add(new ArrayList<>(Arrays.asList(nums[i])));
                result.get(result.size() - 1).addAll(subset);
            }
        }
    }
    return result;
}

private List<List<Integer>> twoSum(int[] nums, int target, int start) {
    List<List<Integer>> result = new ArrayList<>();
    int left = start, right = nums.length - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            result.add(Arrays.asList(nums[left], nums[right]));
            while (left < right && nums[left] == nums[left + 1]) left++;
            while (left < right && nums[right] == nums[right - 1]) right--;
            left++;
            right--;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    return result;
}
```

### 4. Using HashSet
This approach uses a HashSet to avoid duplicate quadruplets.

```java
import java.util.*;

public List<List<Integer>> fourSum(int[] nums, int target) {
    Set<List<Integer>> result = new HashSet<>();
    if (nums == null || nums.length < 4) return new ArrayList<>(result);
    
    Arrays.sort(nums);
    
    for (int i = 0; i < nums.length - 3; i++) {
        for (int j = i + 1; j < nums.length - 2; j++) {
            int left = j + 1, right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[j] + nums[left] + nums[right];
                if (sum == target) {
                    result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
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
    
    return new ArrayList<>(result);
}
```

Each of these methods has its own advantages. The HashMap approach is efficient and avoids duplicates, the Two-Pointer approach is straightforward and efficient, the Recursive approach is flexible and handles different values of k, and the HashSet approach ensures unique quadruplets.

Which approach do you find most suitable for your needs?


# Tpoic - String

## Valid Parenthesis

Sure! The "Valid Parentheses" problem can be approached in several ways. Here are a few different methods to solve this problem in Java:

### 1. Using a Stack (Common Approach)
This is the most common and efficient approach to solve the "Valid Parentheses" problem. The idea is to use a stack to keep track of opening brackets and ensure they are closed in the correct order.

#### Steps:
1. Initialize an empty stack.
2. Traverse the input string character by character.
3. Push opening brackets ('(', '{', '[') onto the stack.
4. For closing brackets (')', '}', ']'), check if the stack is empty or if the top of the stack does not match the corresponding opening bracket. If so, return false.
5. After processing all characters, if the stack is empty, return true; otherwise, return false.

#### Code:
```java
import java.util.Stack;

public class ValidParentheses {
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
        String s = "{[]}";
        System.out.println(isValid(s)); // Output: true
    }
}
```

### 2. Using a HashMap and Stack
This approach is similar to the stack method but uses a `HashMap` to store the mapping of opening and closing brackets. This can make the code cleaner and more readable.

#### Steps:
1. Create a `HashMap` to store the mappings of opening and closing brackets.
2. Initialize an empty stack.
3. Traverse the input string character by character.
4. Push opening brackets onto the stack.
5. For closing brackets, check if the stack is empty or if the top of the stack does not match the corresponding opening bracket using the `HashMap`. If so, return false.
6. After processing all characters, if the stack is empty, return true; otherwise, return false.

#### Code:
```java
import java.util.HashMap;
import java.util.Stack;

public class ValidParentheses {
    public static boolean isValid(String s) {
        HashMap<Character, Character> map = new HashMap<>();
        map.put(')', '(');
        map.put('}', '{');
        map.put(']', '[');

        Stack<Character> stack = new Stack<>();
        for (char c : s.toCharArray()) {
            if (map.containsKey(c)) {
                char topElement = stack.isEmpty() ? '#' : stack.pop();
                if (topElement != map.get(c)) {
                    return false;
                }
            } else {
                stack.push(c);
            }
        }
        return stack.isEmpty();
    }

    public static void main(String[] args) {
        String s = "{[]}";
        System.out.println(isValid(s)); // Output: true
    }
}
```

### 3. Using Counters (Limited to Parentheses Only)
This approach uses counters and is limited to handling only parentheses ('(' and ')'). It does not work for curly braces or square brackets.

#### Steps:
1. Initialize a counter to zero.
2. Traverse the input string character by character.
3. Increment the counter for each opening parenthesis '('.
4. Decrement the counter for each closing parenthesis ')'.
5. If the counter becomes negative at any point, return false.
6. After processing all characters, if the counter is zero, return true; otherwise, return false.

#### Code:
```java
public class ValidParentheses {
    public static boolean isValid(String s) {
        int counter = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                counter++;
            } else if (c == ')') {
                counter--;
                if (counter < 0) {
                    return false;
                }
            }
        }
        return counter == 0;
    }

    public static void main(String[] args) {
        String s = "()()";
        System.out.println(isValid(s)); // Output: true
    }
}
```

### Conclusion
The stack-based approach is the most versatile and commonly used method for solving the "Valid Parentheses" problem, as it can handle all types of brackets and ensures they are properly nested and ordered[1](https://www.javatpoint.com/valid-parentheses-problem-in-java)[2](https://algo.monster/liteproblems/20)[3](https://www.javaguides.net/2023/12/valid-parentheses-problem-java-solution.html). The HashMap and stack combination can make the code cleaner, while the counter approach is a simpler but limited solution.

If you have any questions or need further clarification on any of these approaches, feel free to ask!


## Wildcard pattern Matching

Wildcard pattern matching is a common problem where you need to determine if a given string matches a pattern that includes wildcard characters. The two wildcard characters typically used are:
- `?` which matches any single character.
- `*` which matches any sequence of characters (including the empty sequence).

Here are different approaches to solve the wildcard pattern matching problem in Java:

### 1. Recursive Approach
This approach uses recursion to match the pattern with the string. It checks each character and handles the wildcards accordingly.

#### Steps:
1. If both the string and pattern are empty, return true.
2. If the pattern is empty but the string is not, return false.
3. If the string is empty but the pattern is not, return true only if the remaining characters in the pattern are all `*`.
4. If the current character in the pattern is `*`, it can match zero or more characters in the string.
5. If the current character in the pattern is `?`, it matches any single character in the string.
6. If the current character in the pattern is not a wildcard, it must match the current character in the string.

#### Code:
```java
public class WildcardMatching {
    public static boolean isMatch(String s, String p) {
        return isMatchHelper(s, p, 0, 0);
    }

    private static boolean isMatchHelper(String s, String p, int i, int j) {
        if (j == p.length()) {
            return i == s.length();
        }
        if (i < s.length() && (p.charAt(j) == '?' || p.charAt(j) == s.charAt(i))) {
            return isMatchHelper(s, p, i + 1, j + 1);
        }
        if (p.charAt(j) == '*') {
            return isMatchHelper(s, p, i, j + 1) || (i < s.length() && isMatchHelper(s, p, i + 1, j));
        }
        return false;
    }

    public static void main(String[] args) {
        String s = "adceb";
        String p = "*a*b";
        System.out.println(isMatch(s, p)); // Output: true
    }
}
```

### 2. Dynamic Programming Approach
This approach uses dynamic programming to store the results of subproblems and avoid redundant calculations.

#### Steps:
1. Create a 2D boolean array `dp` where `dp[i][j]` represents if the first `i` characters of the string match the first `j` characters of the pattern.
2. Initialize `dp[0][0]` to true since an empty string matches an empty pattern.
3. Fill the first row where the pattern contains only `*`.
4. Iterate through the string and pattern, filling the `dp` table based on the current characters and wildcards.

#### Code:
```java
public class WildcardMatching {
    public static boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;

        for (int j = 1; j <= n; j++) {
            if (p.charAt(j - 1) == '*') {
                dp[0][j] = dp[0][j - 1];
            }
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else if (p.charAt(j - 1) == '?' || p.charAt(j - 1) == s.charAt(i - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String s = "adceb";
        String p = "*a*b";
        System.out.println(isMatch(s, p)); // Output: true
    }
}
```

### 3. Greedy Approach
This approach uses two pointers to traverse the string and pattern, and a backtracking mechanism to handle `*`.

#### Steps:
1. Use two pointers to traverse the string and pattern.
2. Track the positions of the last `*` in the pattern and the corresponding position in the string.
3. If a mismatch occurs, backtrack to the last `*` and try to match the remaining characters.

#### Code:
```java
public class WildcardMatching {
    public static boolean isMatch(String s, String p) {
        int sLen = s.length();
        int pLen = p.length();
        int sIdx = 0, pIdx = 0;
        int starIdx = -1, sTmpIdx = -1;

        while (sIdx < sLen) {
            if (pIdx < pLen && (p.charAt(pIdx) == '?' || p.charAt(pIdx) == s.charAt(sIdx))) {
                sIdx++;
                pIdx++;
            } else if (pIdx < pLen && p.charAt(pIdx) == '*') {
                starIdx = pIdx;
                sTmpIdx = sIdx;
                pIdx++;
            } else if (starIdx == -1) {
                return false;
            } else {
                pIdx = starIdx + 1;
                sIdx = sTmpIdx + 1;
                sTmpIdx++;
            }
        }

        while (pIdx < pLen && p.charAt(pIdx) == '*') {
            pIdx++;
        }

        return pIdx == pLen;
    }

    public static void main(String[] args) {
        String s = "adceb";
        String p = "*a*b";
        System.out.println(isMatch(s, p)); // Output: true
    }
}
```

### Conclusion
Each approach has its own advantages and trade-offs. The recursive approach is simple but can be inefficient for large inputs. The dynamic programming approach is more efficient but uses extra space. The greedy approach is efficient and uses less space but can be more complex to implement[1](https://www.javatpoint.com/wildcard-pattern-matching)[2](https://www.techiedelight.com/wildcard-pattern-matching/)[3](https://algo.monster/liteproblems/44).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Longest common subsequence

The Longest Common Subsequence (LCS) problem is a classic problem in computer science. It involves finding the longest subsequence common to two sequences. A subsequence is a sequence derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

### Problem Statement
Given two strings, find the length of their longest common subsequence.

### Example
```java
Input: s1 = "abcde", s2 = "ace"
Output: 3
Explanation: The longest common subsequence is "ace" which has length 3.
```

### Different Approaches to Solve LCS

#### 1. Recursive Approach
This approach uses recursion to solve the problem by comparing characters from the end of both strings.

#### Steps:
1. If either string is empty, return 0.
2. If the last characters of both strings match, the LCS includes this character.
3. If the last characters do not match, the LCS is the maximum of the LCS obtained by removing the last character from either string.

#### Code:
```java
public class LCS {
    public static int lcs(String s1, String s2) {
        return lcsHelper(s1, s2, s1.length(), s2.length());
    }

    private static int lcsHelper(String s1, String s2, int m, int n) {
        if (m == 0 || n == 0) {
            return 0;
        }
        if (s1.charAt(m - 1) == s2.charAt(n - 1)) {
            return 1 + lcsHelper(s1, s2, m - 1, n - 1);
        } else {
            return Math.max(lcsHelper(s1, s2, m, n - 1), lcsHelper(s1, s2, m - 1, n));
        }
    }

    public static void main(String[] args) {
        String s1 = "abcde";
        String s2 = "ace";
        System.out.println("Length of LCS: " + lcs(s1, s2)); // Output: 3
    }
}
```

#### 2. Dynamic Programming Approach
This approach uses a 2D table to store the lengths of LCS for substrings of both strings, avoiding redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` represents the length of LCS of the first `i` characters of `s1` and the first `j` characters of `s2`.
2. Initialize the first row and first column to 0.
3. Fill the table using the following rules:
   - If `s1[i-1] == s2[j-1]`, then `dp[i][j] = dp[i-1][j-1] + 1`.
   - Otherwise, `dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1])`.

#### Code:
```java
public class LCS {
    public static int lcs(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }

    public static void main(String[] args) {
        String s1 = "abcde";
        String s2 = "ace";
        System.out.println("Length of LCS: " + lcs(s1, s2)); // Output: 3
    }
}
```

#### 3. Space Optimized Dynamic Programming
This approach optimizes the space complexity of the dynamic programming solution by using two 1D arrays instead of a 2D array.

#### Steps:
1. Use two 1D arrays `previous` and `current` to store the LCS lengths for the previous and current rows.
2. Update the arrays as you iterate through the characters of the strings.

#### Code:
```java
public class LCS {
    public static int lcs(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();
        int[] previous = new int[n + 1];
        int[] current = new int[n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    current[j] = previous[j - 1] + 1;
                } else {
                    current[j] = Math.max(previous[j], current[j - 1]);
                }
            }
            int[] temp = previous;
            previous = current;
            current = temp;
        }
        return previous[n];
    }

    public static void main(String[] args) {
        String s1 = "abcde";
        String s2 = "ace";
        System.out.println("Length of LCS: " + lcs(s1, s2)); // Output: 3
    }
}
```

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a time complexity of \(O(m \times n)\) and space complexity of \(O(m \times n)\).
- The **space-optimized dynamic programming approach** reduces the space complexity to \(O(n)\) while maintaining the same time complexity[1](https://www.javatpoint.com/longest-common-subsequence-in-java)[2](https://www.javatpoint.com/longest-common-subsequence)[3](https://www.programiz.com/dsa/longest-common-subsequence).

If you have any questions or need further clarification on any of these approaches, feel free to ask!


## Longest Pallindromic Subsequence

The Longest Palindromic Subsequence (LPS) problem involves finding the longest subsequence in a given string that is also a palindrome. A subsequence is a sequence derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

### Problem Statement
Given a string `s`, find the length of the longest palindromic subsequence in `s`.

### Example
```java
Input: s = "bbbab"
Output: 4
Explanation: One possible longest palindromic subsequence is "bbbb".
```

### Different Approaches to Solve LPS

#### 1. Recursive Approach
This approach uses recursion to solve the problem by comparing characters from both ends of the string.

#### Steps:
1. If the string is empty or has one character, return its length.
2. If the first and last characters of the string are the same, the LPS includes these characters.
3. If the first and last characters are different, the LPS is the maximum of the LPS obtained by removing either the first or the last character.

#### Code:
```java
public class LongestPalindromicSubsequence {
    public static int lps(String s) {
        return lpsHelper(s, 0, s.length() - 1);
    }

    private static int lpsHelper(String s, int start, int end) {
        if (start > end) {
            return 0;
        }
        if (start == end) {
            return 1;
        }
        if (s.charAt(start) == s.charAt(end)) {
            return 2 + lpsHelper(s, start + 1, end - 1);
        } else {
            return Math.max(lpsHelper(s, start + 1, end), lpsHelper(s, start, end - 1));
        }
    }

    public static void main(String[] args) {
        String s = "bbbab";
        System.out.println("Length of LPS: " + lps(s)); // Output: 4
    }
}
```

#### 2. Dynamic Programming Approach
This approach uses a 2D table to store the lengths of LPS for substrings of the given string, avoiding redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` represents the length of LPS of the substring `s[i...j]`.
2. Initialize the diagonal elements `dp[i][i]` to 1 since a single character is a palindrome of length 1.
3. Fill the table using the following rules:
   - If `s[i] == s[j]`, then `dp[i][j] = dp[i+1][j-1] + 2`.
   - Otherwise, `dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1])`.

#### Code:
```java
public class LongestPalindromicSubsequence {
    public static int lps(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];

        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

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
        System.out.println("Length of LPS: " + lps(s)); // Output: 4
    }
}
```

#### 3. Space Optimized Dynamic Programming
This approach optimizes the space complexity of the dynamic programming solution by using two 1D arrays instead of a 2D array.

#### Steps:
1. Use two 1D arrays `previous` and `current` to store the LPS lengths for the previous and current rows.
2. Update the arrays as you iterate through the characters of the string.

#### Code:
```java
public class LongestPalindromicSubsequence {
    public static int lps(String s) {
        int n = s.length();
        int[] previous = new int[n];
        int[] current = new int[n];

        for (int i = n - 1; i >= 0; i--) {
            current[i] = 1;
            for (int j = i + 1; j < n; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    current[j] = previous[j - 1] + 2;
                } else {
                    current[j] = Math.max(previous[j], current[j - 1]);
                }
            }
            int[] temp = previous;
            previous = current;
            current = temp;
        }

        return previous[n - 1];
    }

    public static void main(String[] args) {
        String s = "bbbab";
        System.out.println("Length of LPS: " + lps(s)); // Output: 4
    }
}
```

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a time complexity of \(O(n^2)\) and space complexity of \(O(n^2)\).
- The **space-optimized dynamic programming approach** reduces the space complexity to \(O(n)\) while maintaining the same time complexity[1](https://www.mastercoding.org/java-programs/java-solution-for-longest-palindromic-subsequence/)[2](https://www.interviewbit.com/blog/longest-palindromic-subsequence/)[3](https://www.upgrad.com/tutorials/software-engineering/software-key-tutorial/longest-palindromic-subsequence/).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Longest Palindromic Substring

The Longest Palindromic Substring (LPS) problem involves finding the longest contiguous substring within a given string that reads the same forwards and backwards.

### Problem Statement
Given a string `s`, find the longest palindromic substring in `s`.

### Example
```java
Input: s = "babad"
Output: "bab" or "aba"
Explanation: Both "bab" and "aba" are valid answers.
```

### Different Approaches to Solve LPS

#### 1. Brute Force Approach
This approach involves generating all possible substrings of the given string and checking each one to see if it is a palindrome.

#### Steps:
1. Generate all possible substrings.
2. Check each substring to see if it is a palindrome.
3. Keep track of the longest palindromic substring found.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        int n = s.length();
        if (n == 0) return "";
        String longest = s.substring(0, 1);
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                String substr = s.substring(i, j + 1);
                if (isPalindrome(substr) && substr.length() > longest.length()) {
                    longest = substr;
                }
            }
        }
        return longest;
    }

    private static boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n^3)\)

#### 2. Dynamic Programming Approach
This approach uses a 2D table to store whether substrings are palindromes, avoiding redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` is true if the substring `s[i...j]` is a palindrome.
2. Initialize the table for substrings of length 1 and 2.
3. Fill the table for substrings of length greater than 2.
4. Keep track of the longest palindromic substring found.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        int n = s.length();
        if (n == 0) return "";
        boolean[][] dp = new boolean[n][n];
        String longest = s.substring(0, 1);

        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }

        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                longest = s.substring(i, i + 2);
            }
        }

        for (int length = 3; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    longest = s.substring(i, j + 1);
                }
            }
        }

        return longest;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n^2)\)

#### 3. Expand Around Center Approach
This approach considers each character (and each pair of characters) as the center of a palindrome and expands outwards to find the longest palindromic substring.

#### Steps:
1. Iterate through each character and each pair of characters in the string.
2. Expand outwards from each center to find the longest palindromic substring.
3. Keep track of the longest palindromic substring found.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        if (s == null || s.length() < 1) return "";
        int start = 0, end = 0;
        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i + 1);
            int len = Math.max(len1, len2);
            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }
        return s.substring(start, end + 1);
    }

    private static int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n^2)\)

#### 4. Manacher's Algorithm
This approach finds the longest palindromic substring in linear time. It transforms the string to handle even-length palindromes and uses a clever technique to avoid redundant comparisons.

#### Steps:
1. Transform the string to handle even-length palindromes.
2. Use an array to store the lengths of palindromes centered at each character.
3. Use a center and right boundary to avoid redundant comparisons.
4. Find the longest palindromic substring from the array.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        if (s == null || s.length() == 0) return "";
        char[] t = preprocess(s);
        int[] p = new int[t.length];
        int center = 0, right = 0;
        for (int i = 1; i < t.length - 1; i++) {
            int mirror = 2 * center - i;
            if (right > i) {
                p[i] = Math.min(right - i, p[mirror]);
            }
            while (t[i + 1 + p[i]] == t[i - 1 - p[i]]) {
                p[i]++;
            }
            if (i + p[i] > right) {
                center = i;
                right = i + p[i];
            }
        }
        int maxLen = 0;
        int centerIndex = 0;
        for (int i = 1; i < t.length - 1; i++) {
            if (p[i] > maxLen) {
                maxLen = p[i];
                centerIndex = i;
            }
        }
        int start = (centerIndex - maxLen) / 2;
        return s.substring(start, start + maxLen);
    }

    private static char[] preprocess(String s) {
        char[] t = new char[s.length() * 2 + 3];
        t[0] = '^';
        for (int i = 0; i < s.length(); i++) {
            t[2 * i + 1] = '#';
            t[2 * i + 2] = s.charAt(i);
        }
        t[t.length - 2] = '#';
        t[t.length - 1] = '$';
        return t;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **brute force approach** is simple but inefficient for large inputs due to its cubic time complexity.
- The **dynamic programming approach** is more efficient with a quadratic time complexity but uses extra space.
- The **expand around center approach** is efficient and easy to implement with a quadratic time complexity.
- **Manacher's algorithm** is the most efficient with a linear time complexity but is more complex to implement[1](https://www.javatpoint.com/longest-palindrome-substring)[2](https://www.baeldung.com/java-palindrome-substrings)[3](https://favtutor.com/blogs/longest-palindromic-substring).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Longest substring without repeating characters

The "Longest Substring Without Repeating Characters" problem involves finding the length of the longest substring in a given string where all characters are unique.

### Problem Statement
Given a string `s`, find the length of the longest substring without repeating characters.

### Example
```java
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

### Different Approaches to Solve the Problem

#### 1. Brute Force Approach
This approach involves generating all possible substrings and checking each one to see if it contains all unique characters.

#### Steps:
1. Generate all possible substrings.
2. Check each substring to see if it contains all unique characters.
3. Keep track of the length of the longest substring found.

#### Code:
```java
import java.util.HashSet;
import java.util.Set;

public class LongestSubstringWithoutRepeatingCharacters {
    public static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int maxLength = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j <= n; j++) {
                if (allUnique(s, i, j)) {
                    maxLength = Math.max(maxLength, j - i);
                }
            }
        }
        return maxLength;
    }

    private static boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i < end; i++) {
            char ch = s.charAt(i);
            if (set.contains(ch)) {
                return false;
            }
            set.add(ch);
        }
        return true;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Length of Longest Substring Without Repeating Characters: " + lengthOfLongestSubstring(s)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n^3)\)

#### 2. Sliding Window Approach
This approach uses a sliding window to maintain a window of unique characters and expands or contracts the window as needed.

#### Steps:
1. Use two pointers to represent the window's start and end.
2. Expand the window by moving the end pointer and adding characters to a set.
3. If a duplicate character is found, move the start pointer to the right until the duplicate is removed.
4. Keep track of the maximum length of the window.

#### Code:
```java
import java.util.HashSet;
import java.util.Set;

public class LongestSubstringWithoutRepeatingCharacters {
    public static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int maxLength = 0, i = 0, j = 0;
        while (i < n && j < n) {
            if (!set.contains(s.charAt(j))) {
                set.add(s.charAt(j++));
                maxLength = Math.max(maxLength, j - i);
            } else {
                set.remove(s.charAt(i++));
            }
        }
        return maxLength;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Length of Longest Substring Without Repeating Characters: " + lengthOfLongestSubstring(s)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n)\)

#### 3. Optimized Sliding Window Using HashMap
This approach optimizes the sliding window by using a `HashMap` to store the characters and their indices, allowing for faster updates of the start pointer.

#### Steps:
1. Use a `HashMap` to store the characters and their latest indices.
2. Use two pointers to represent the window's start and end.
3. Expand the window by moving the end pointer and updating the `HashMap`.
4. If a duplicate character is found, update the start pointer to the maximum of its current value and the index of the duplicate character plus one.
5. Keep track of the maximum length of the window.

#### Code:
```java
import java.util.HashMap;
import java.util.Map;

public class LongestSubstringWithoutRepeatingCharacters {
    public static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Map<Character, Integer> map = new HashMap<>();
        int maxLength = 0;
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)) + 1, i);
            }
            map.put(s.charAt(j), j);
            maxLength = Math.max(maxLength, j - i + 1);
        }
        return maxLength;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Length of Longest Substring Without Repeating Characters: " + lengthOfLongestSubstring(s)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **brute force approach** is simple but inefficient for large inputs due to its cubic time complexity.
- The **sliding window approach** is more efficient with a linear time complexity and is easy to implement.
- The **optimized sliding window using HashMap** further improves efficiency by reducing the time complexity to linear while maintaining constant space complexity[1](https://www.javatpoint.com/length-of-the-longest-substring-without-repeating-characters-in-java)[2](https://www.baeldung.com/java-longest-substring-without-repeated-characters)[3](https://examples.javacodegeeks.com/longest-substring-without-repeating-characters/).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Group Anagram Together

The "Longest Substring Without Repeating Characters" problem involves finding the length of the longest substring in a given string where all characters are unique.

### Problem Statement
Given a string `s`, find the length of the longest substring without repeating characters.

### Example
```java
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

### Different Approaches to Solve the Problem

#### 1. Brute Force Approach
This approach involves generating all possible substrings and checking each one to see if it contains all unique characters.

#### Steps:
1. Generate all possible substrings.
2. Check each substring to see if it contains all unique characters.
3. Keep track of the length of the longest substring found.

#### Code:
```java
import java.util.HashSet;
import java.util.Set;

public class LongestSubstringWithoutRepeatingCharacters {
    public static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int maxLength = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j <= n; j++) {
                if (allUnique(s, i, j)) {
                    maxLength = Math.max(maxLength, j - i);
                }
            }
        }
        return maxLength;
    }

    private static boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i < end; i++) {
            char ch = s.charAt(i);
            if (set.contains(ch)) {
                return false;
            }
            set.add(ch);
        }
        return true;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Length of Longest Substring Without Repeating Characters: " + lengthOfLongestSubstring(s)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n^3)\)

#### 2. Sliding Window Approach
This approach uses a sliding window to maintain a window of unique characters and expands or contracts the window as needed.

#### Steps:
1. Use two pointers to represent the window's start and end.
2. Expand the window by moving the end pointer and adding characters to a set.
3. If a duplicate character is found, move the start pointer to the right until the duplicate is removed.
4. Keep track of the maximum length of the window.

#### Code:
```java
import java.util.HashSet;
import java.util.Set;

public class LongestSubstringWithoutRepeatingCharacters {
    public static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int maxLength = 0, i = 0, j = 0;
        while (i < n && j < n) {
            if (!set.contains(s.charAt(j))) {
                set.add(s.charAt(j++));
                maxLength = Math.max(maxLength, j - i);
            } else {
                set.remove(s.charAt(i++));
            }
        }
        return maxLength;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Length of Longest Substring Without Repeating Characters: " + lengthOfLongestSubstring(s)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n)\)

#### 3. Optimized Sliding Window Using HashMap
This approach optimizes the sliding window by using a `HashMap` to store the characters and their indices, allowing for faster updates of the start pointer.

#### Steps:
1. Use a `HashMap` to store the characters and their latest indices.
2. Use two pointers to represent the window's start and end.
3. Expand the window by moving the end pointer and updating the `HashMap`.
4. If a duplicate character is found, update the start pointer to the maximum of its current value and the index of the duplicate character plus one.
5. Keep track of the maximum length of the window.

#### Code:
```java
import java.util.HashMap;
import java.util.Map;

public class LongestSubstringWithoutRepeatingCharacters {
    public static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Map<Character, Integer> map = new HashMap<>();
        int maxLength = 0;
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)) + 1, i);
            }
            map.put(s.charAt(j), j);
            maxLength = Math.max(maxLength, j - i + 1);
        }
        return maxLength;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Length of Longest Substring Without Repeating Characters: " + lengthOfLongestSubstring(s)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **brute force approach** is simple but inefficient for large inputs due to its cubic time complexity.
- The **sliding window approach** is more efficient with a linear time complexity and is easy to implement.
- The **optimized sliding window using HashMap** further improves efficiency by reducing the time complexity to linear while maintaining constant space complexity[1](https://www.javatpoint.com/length-of-the-longest-substring-without-repeating-characters-in-java)[2](https://www.baeldung.com/java-longest-substring-without-repeated-characters)[3](https://examples.javacodegeeks.com/longest-substring-without-repeating-characters/).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Palindromic Partitioning

Palindrome partitioning involves dividing a string into substrings such that each substring is a palindrome. There are different approaches to solve this problem in Java, including recursive, dynamic programming, and backtracking methods.

### Problem Statement
Given a string `s`, partition `s` such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of `s`.

### Example
```java
Input: s = "aab"
Output: [["a","a","b"], ["aa","b"]]
```

### Different Approaches to Solve Palindromic Partitioning

#### 1. Recursive Approach
This approach uses recursion to explore all possible partitions and checks if each partition is a palindrome.

#### Steps:
1. Define a recursive function that partitions the string.
2. For each substring, check if it is a palindrome.
3. If it is, recursively partition the remaining string.
4. Collect all valid partitions.

#### Code:
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
        System.out.println(partition(s)); // Output: [["a","a","b"], ["aa","b"]]
    }
}
```

#### 2. Dynamic Programming Approach
This approach uses dynamic programming to store whether substrings are palindromes and minimizes the number of cuts needed.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` is true if the substring `s[i...j]` is a palindrome.
2. Use another array `cuts` to store the minimum cuts needed for the substring `s[0...i]`.
3. Fill the `dp` table and update the `cuts` array accordingly.

#### Code:
```java
import java.util.ArrayList;
import java.util.List;

public class PalindromePartitioning {
    public static List<List<String>> partition(String s) {
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        List<List<String>>[] result = new List[n + 1];
        result[0] = new ArrayList<>();
        result[0].add(new ArrayList<>());

        for (int i = 0; i < n; i++) {
            result[i + 1] = new ArrayList<>();
            for (int j = 0; j <= i; j++) {
                if (s.charAt(i) == s.charAt(j) && (i - j <= 2 || dp[j + 1][i - 1])) {
                    dp[j][i] = true;
                    String sub = s.substring(j, i + 1);
                    for (List<String> l : result[j]) {
                        List<String> newList = new ArrayList<>(l);
                        newList.add(sub);
                        result[i + 1].add(newList);
                    }
                }
            }
        }
        return result[n];
    }

    public static void main(String[] args) {
        String s = "aab";
        System.out.println(partition(s)); // Output: [["a","a","b"], ["aa","b"]]
    }
}
```

#### 3. Backtracking Approach
This approach uses backtracking to explore all possible partitions and checks if each partition is a palindrome.

#### Steps:
1. Use a helper function to perform backtracking.
2. For each substring, check if it is a palindrome.
3. If it is, add it to the current partition and recursively partition the remaining string.
4. Backtrack by removing the last added substring and trying different partitions.

#### Code:
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
        System.out.println(partition(s)); // Output: [["a","a","b"], ["aa","b"]]
    }
}
```

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a time complexity of \(O(n^2)\) and space complexity of \(O(n^2)\).
- The **backtracking approach** is efficient and easy to implement, leveraging the recursive nature of the problem[1](https://www.javatpoint.com/palindrome-partitioning-problem-in-java)[2](https://www.sourcecodeexamples.net/2023/12/palindrome-partitioning-java-solution.html)[3](https://algo.monster/liteproblems/131).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Palindromic Substring

Finding the longest palindromic substring in a given string is a common problem in computer science. Here are different approaches to solve this problem in Java:

### 1. Brute Force Approach
This approach involves generating all possible substrings and checking each one to see if it is a palindrome.

#### Steps:
1. Generate all possible substrings.
2. Check each substring to see if it is a palindrome.
3. Keep track of the longest palindromic substring found.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        int n = s.length();
        if (n == 0) return "";
        String longest = s.substring(0, 1);
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                String substr = s.substring(i, j + 1);
                if (isPalindrome(substr) && substr.length() > longest.length()) {
                    longest = substr;
                }
            }
        }
        return longest;
    }

    private static boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n^3)\)

### 2. Dynamic Programming Approach
This approach uses a 2D table to store whether substrings are palindromes, avoiding redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` is true if the substring `s[i...j]` is a palindrome.
2. Initialize the table for substrings of length 1 and 2.
3. Fill the table for substrings of length greater than 2.
4. Keep track of the longest palindromic substring found.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        int n = s.length();
        if (n == 0) return "";
        boolean[][] dp = new boolean[n][n];
        String longest = s.substring(0, 1);

        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }

        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                longest = s.substring(i, i + 2);
            }
        }

        for (int length = 3; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    longest = s.substring(i, j + 1);
                }
            }
        }

        return longest;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n^2)\)

### 3. Expand Around Center Approach
This approach considers each character (and each pair of characters) as the center of a palindrome and expands outwards to find the longest palindromic substring.

#### Steps:
1. Iterate through each character and each pair of characters in the string.
2. Expand outwards from each center to find the longest palindromic substring.
3. Keep track of the longest palindromic substring found.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        if (s == null || s.length() < 1) return "";
        int start = 0, end = 0;
        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i + 1);
            int len = Math.max(len1, len2);
            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }
        return s.substring(start, end + 1);
    }

    private static int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n^2)\)

### 4. Manacher's Algorithm
This approach finds the longest palindromic substring in linear time. It transforms the string to handle even-length palindromes and uses a clever technique to avoid redundant comparisons.

#### Steps:
1. Transform the string to handle even-length palindromes.
2. Use an array to store the lengths of palindromes centered at each character.
3. Use a center and right boundary to avoid redundant comparisons.
4. Find the longest palindromic substring from the array.

#### Code:
```java
public class LongestPalindromicSubstring {
    public static String longestPalindrome(String s) {
        if (s == null || s.length() == 0) return "";
        char[] t = preprocess(s);
        int[] p = new int[t.length];
        int center = 0, right = 0;
        for (int i = 1; i < t.length - 1; i++) {
            int mirror = 2 * center - i;
            if (right > i) {
                p[i] = Math.min(right - i, p[mirror]);
            }
            while (t[i + 1 + p[i]] == t[i - 1 - p[i]]) {
                p[i]++;
            }
            if (i + p[i] > right) {
                center = i;
                right = i + p[i];
            }
        }
        int maxLen = 0;
        int centerIndex = 0;
        for (int i = 1; i < t.length - 1; i++) {
            if (p[i] > maxLen) {
                maxLen = p[i];
                centerIndex = i;
            }
        }
        int start = (centerIndex - maxLen) / 2;
        return s.substring(start, start + maxLen);
    }

    private static char[] preprocess(String s) {
        char[] t = new char[s.length() * 2 + 3];
        t[0] = '^';
        for (int i = 0; i < s.length(); i++) {
            t[2 * i + 1] = '#';
            t[2 * i + 2] = s.charAt(i);
        }
        t[t.length - 2] = '#';
        t[t.length - 1] = '$';
        return t;
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s)); // Output: "bab" or "aba"
    }
}
```
#### Time Complexity: \(O(n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **brute force approach** is simple but inefficient for large inputs due to its cubic time complexity.
- The **dynamic programming approach** is more efficient with a quadratic time complexity but uses extra space.
- The **expand around center approach** is efficient and easy to implement with a quadratic time complexity.
- **Manacher's algorithm** is the most efficient with a linear time complexity but is more complex to implement[1](https://www.baeldung.com/java-palindrome-substrings)[2](https://www.javatpoint.com/find-all-palindromic-sub-strings-of-a-given-string-in-java)[3](https://bing.com/search?q=Pallindromic+substring+with+different+approaches+in+Java).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Edit Distance

The Edit Distance problem, also known as Levenshtein Distance, measures the minimum number of operations required to transform one string into another. The allowed operations are:
1. **Insert a character**
2. **Delete a character**
3. **Replace a character**

### Problem Statement
Given two strings `word1` and `word2`, find the minimum number of operations required to convert `word1` to `word2`.

### Example
```java
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

### Different Approaches to Solve Edit Distance

#### 1. Recursive Approach
This approach uses recursion to explore all possible operations and find the minimum number of operations required.

#### Steps:
1. If either string is empty, return the length of the other string.
2. If the last characters of both strings match, recursively compute the edit distance for the remaining substrings.
3. If the last characters do not match, consider all three operations (insert, delete, replace) and recursively compute the edit distance for each case.
4. Return the minimum of the three computed values.

#### Code:
```java
public class EditDistance {
    public static int minDistance(String word1, String word2) {
        return minDistanceHelper(word1, word2, word1.length(), word2.length());
    }

    private static int minDistanceHelper(String word1, String word2, int m, int n) {
        if (m == 0) return n;
        if (n == 0) return m;
        if (word1.charAt(m - 1) == word2.charAt(n - 1)) {
            return minDistanceHelper(word1, word2, m - 1, n - 1);
        }
        return 1 + Math.min(minDistanceHelper(word1, word2, m, n - 1), // Insert
                            Math.min(minDistanceHelper(word1, word2, m - 1, n), // Remove
                                     minDistanceHelper(word1, word2, m - 1, n - 1))); // Replace
    }

    public static void main(String[] args) {
        String word1 = "horse";
        String word2 = "ros";
        System.out.println("Minimum Edit Distance: " + minDistance(word1, word2)); // Output: 3
    }
}
```
#### Time Complexity: \(O(3^{\min(m, n)})\)

#### 2. Dynamic Programming Approach
This approach uses a 2D table to store the minimum edit distances for substrings of the given strings, avoiding redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` represents the minimum edit distance between the first `i` characters of `word1` and the first `j` characters of `word2`.
2. Initialize the first row and first column of the table.
3. Fill the table using the following rules:
   - If the characters match, `dp[i][j] = dp[i-1][j-1]`.
   - Otherwise, `dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])`.

#### Code:
```java
public class EditDistance {
    public static int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0) {
                    dp[i][j] = j;
                } else if (j == 0) {
                    dp[i][j] = i;
                } else if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j], Math.min(dp[i][j - 1], dp[i - 1][j - 1]));
                }
            }
        }
        return dp[m][n];
    }

    public static void main(String[] args) {
        String word1 = "horse";
        String word2 = "ros";
        System.out.println("Minimum Edit Distance: " + minDistance(word1, word2)); // Output: 3
    }
}
```
#### Time Complexity: \(O(m \times n)\)

#### 3. Space Optimized Dynamic Programming
This approach optimizes the space complexity of the dynamic programming solution by using two 1D arrays instead of a 2D array.

#### Steps:
1. Use two 1D arrays `previous` and `current` to store the minimum edit distances for the previous and current rows.
2. Update the arrays as you iterate through the characters of the strings.

#### Code:
```java
public class EditDistance {
    public static int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[] previous = new int[n + 1];
        int[] current = new int[n + 1];

        for (int j = 0; j <= n; j++) {
            previous[j] = j;
        }

        for (int i = 1; i <= m; i++) {
            current[0] = i;
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    current[j] = previous[j - 1];
                } else {
                    current[j] = 1 + Math.min(previous[j], Math.min(current[j - 1], previous[j - 1]));
                }
            }
            int[] temp = previous;
            previous = current;
            current = temp;
        }

        return previous[n];
    }

    public static void main(String[] args) {
        String word1 = "horse";
        String word2 = "ros";
        System.out.println("Minimum Edit Distance: " + minDistance(word1, word2)); // Output: 3
    }
}
```
#### Time Complexity: \(O(m \times n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a time complexity of \(O(m \times n)\) and space complexity of \(O(m \times n)\).
- The **space-optimized dynamic programming approach** reduces the space complexity to \(O(n)\) while maintaining the same time complexity[1](https://www.programcreek.com/2013/12/edit-distance-in-java/)[2](https://www.javacodegeeks.com/2014/03/easy-to-understand-dynamic-programming-edit-distance.html)[3](https://www.baeldung.com/java-levenshtein-distance).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Find all Anagram in String

Finding all anagrams of a given string within another string is a common problem. Here are different approaches to solve this problem in Java:

### Problem Statement
Given a string `s` and a non-empty string `p`, find all the start indices of `p`'s anagrams in `s`.

### Example
```java
Input: s = "cbaebabacd", p = "abc"
Output: [0, 6]
Explanation: The substring starting at index 0 ("cba") and the substring starting at index 6 ("bac") are anagrams of "abc".
```

### Different Approaches to Solve the Problem

#### 1. Sorting Approach
This approach involves sorting each substring of length `p` in `s` and comparing it with the sorted version of `p`.

#### Steps:
1. Sort the string `p`.
2. Iterate through each substring of length `p` in `s`.
3. Sort each substring and compare it with the sorted `p`.
4. If they match, record the starting index.

#### Code:
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class FindAllAnagrams {
    public static List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        if (s == null || p == null || s.length() < p.length()) return result;

        char[] pArray = p.toCharArray();
        Arrays.sort(pArray);
        String pSorted = new String(pArray);

        for (int i = 0; i <= s.length() - p.length(); i++) {
            String sub = s.substring(i, i + p.length());
            char[] subArray = sub.toCharArray();
            Arrays.sort(subArray);
            if (new String(subArray).equals(pSorted)) {
                result.add(i);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        String s = "cbaebabacd";
        String p = "abc";
        System.out.println(findAnagrams(s, p)); // Output: [0, 6]
    }
}
```
#### Time Complexity: \(O((n - m + 1) \cdot m \log m)\), where \(n\) is the length of `s` and \(m\) is the length of `p`.

#### 2. Sliding Window with Character Count
This approach uses a sliding window to maintain a count of characters and compares it with the count of characters in `p`.

#### Steps:
1. Create a frequency array for `p`.
2. Use a sliding window of length `p` to traverse `s`.
3. Maintain a frequency array for the current window in `s`.
4. Compare the frequency arrays to check for anagrams.

#### Code:
```java
import java.util.ArrayList;
import java.util.List;

public class FindAllAnagrams {
    public static List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        if (s == null || p == null || s.length() < p.length()) return result;

        int[] pCount = new int[26];
        int[] sCount = new int[26];

        for (char c : p.toCharArray()) {
            pCount[c - 'a']++;
        }

        for (int i = 0; i < s.length(); i++) {
            sCount[s.charAt(i) - 'a']++;
            if (i >= p.length()) {
                sCount[s.charAt(i - p.length()) - 'a']--;
            }
            if (Arrays.equals(sCount, pCount)) {
                result.add(i - p.length() + 1);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        String s = "cbaebabacd";
        String p = "abc";
        System.out.println(findAnagrams(s, p)); // Output: [0, 6]
    }
}
```
#### Time Complexity: \(O(n)\), where \(n\) is the length of `s`.

#### 3. Optimized Sliding Window with HashMap
This approach uses a sliding window and a `HashMap` to maintain the count of characters, allowing for efficient updates.

#### Steps:
1. Create a `HashMap` for the frequency of characters in `p`.
2. Use a sliding window of length `p` to traverse `s`.
3. Maintain a `HashMap` for the current window in `s`.
4. Compare the `HashMap`s to check for anagrams.

#### Code:
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class FindAllAnagrams {
    public static List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        if (s == null || p == null || s.length() < p.length()) return result;

        Map<Character, Integer> pMap = new HashMap<>();
        for (char c : p.toCharArray()) {
            pMap.put(c, pMap.getOrDefault(c, 0) + 1);
        }

        Map<Character, Integer> sMap = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            sMap.put(c, sMap.getOrDefault(c, 0) + 1);

            if (i >= p.length()) {
                char leftChar = s.charAt(i - p.length());
                if (sMap.get(leftChar) == 1) {
                    sMap.remove(leftChar);
                } else {
                    sMap.put(leftChar, sMap.get(leftChar) - 1);
                }
            }

            if (sMap.equals(pMap)) {
                result.add(i - p.length() + 1);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        String s = "cbaebabacd";
        String p = "abc";
        System.out.println(findAnagrams(s, p)); // Output: [0, 6]
    }
}
```
#### Time Complexity: \(O(n)\), where \(n\) is the length of `s`.

### Conclusion
Each approach has its own advantages and trade-offs:
- The **sorting approach** is straightforward but can be inefficient for long strings due to the sorting step.
- The **sliding window with character count** approach is efficient and easy to implement with linear time complexity.
- The **optimized sliding window with HashMap** approach is also efficient and handles character counts dynamically[1](https://www.youtube.com/watch?v=YKx-Lj0xlKk)[2](https://www.youtube.com/watch?v=-c0hUQHIkSY)[3](https://www.youtube.com/watch?v=4rAc8Oo0kpo).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Word Break

The Word Break problem involves determining if a given string can be segmented into a space-separated sequence of one or more dictionary words.

### Problem Statement
Given a string `s` and a dictionary of words `wordDict`, determine if `s` can be segmented into a space-separated sequence of one or more dictionary words.

### Example
```java
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: "leetcode" can be segmented as "leet code".
```

### Different Approaches to Solve Word Break

#### 1. Recursive Approach
This approach uses recursion and backtracking to explore all possible segmentations of the string.

#### Steps:
1. Check every possible prefix of the string.
2. If the prefix is found in the dictionary, recursively check the remaining substring.
3. If the entire string can be segmented, return true.

#### Code:
```java
import java.util.HashSet;
import java.util.List;
import java.util.Set;

public class WordBreak {
    public static boolean wordBreak(String s, List<String> wordDict) {
        return wordBreakRecur(s, new HashSet<>(wordDict), 0);
    }

    private static boolean wordBreakRecur(String s, Set<String> wordDict, int start) {
        if (start == s.length()) {
            return true;
        }
        for (int end = start + 1; end <= s.length(); end++) {
            if (wordDict.contains(s.substring(start, end)) && wordBreakRecur(s, wordDict, end)) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        String s = "leetcode";
        List<String> wordDict = List.of("leet", "code");
        System.out.println(wordBreak(s, wordDict)); // Output: true
    }
}
```
#### Time Complexity: \(O(2^n)\)

#### 2. Dynamic Programming Approach
This approach uses dynamic programming to store the results of subproblems and avoid redundant calculations.

#### Steps:
1. Create a boolean array `dp` where `dp[i]` indicates if the substring `s[0...i-1]` can be segmented.
2. Initialize `dp[0]` to true since an empty string can be segmented.
3. Iterate through the string and update the `dp` array based on the dictionary words.

#### Code:
```java
import java.util.HashSet;
import java.util.List;
import java.util.Set;

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
        List<String> wordDict = List.of("leet", "code");
        System.out.println(wordBreak(s, wordDict)); // Output: true
    }
}
```
#### Time Complexity: \(O(n^2)\)

#### 3. Breadth-First Search (BFS) Approach
This approach uses BFS to explore all possible segmentations of the string.

#### Steps:
1. Use a queue to store the starting indices of substrings.
2. Use a set to store visited indices to avoid redundant calculations.
3. For each index, check all possible substrings and add the end index to the queue if the substring is in the dictionary.

#### Code:
```java
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;
import java.util.Set;

public class WordBreak {
    public static boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordSet = new HashSet<>(wordDict);
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        queue.add(0);

        while (!queue.isEmpty()) {
            int start = queue.poll();
            if (visited.contains(start)) {
                continue;
            }
            visited.add(start);
            for (int end = start + 1; end <= s.length(); end++) {
                if (wordSet.contains(s.substring(start, end))) {
                    if (end == s.length()) {
                        return true;
                    }
                    queue.add(end);
                }
            }
        }
        return false;
    }

    public static void main(String[] args) {
        String s = "leetcode";
        List<String> wordDict = List.of("leet", "code");
        System.out.println(wordBreak(s, wordDict)); // Output: true
    }
}
```
#### Time Complexity: \(O(n^2)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a quadratic time complexity and is commonly used.
- The **BFS approach** is also efficient and can be easier to understand and implement[1](https://www.interviewbit.com/blog/word-break-problem/)[2](https://www.programcreek.com/2012/12/leetcode-solution-word-break/)[3](https://favtutor.com/articles/word-break-problem/).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Letter combination of phone number

The "Letter Combinations of a Phone Number" problem involves generating all possible letter combinations that a given string of digits could represent on a phone keypad. Each digit maps to a set of letters, similar to the old T9 text input on mobile phones.

### Problem Statement
Given a string containing digits from 2 to 9, return all possible letter combinations that the number could represent.

### Example
```java
Input: digits = "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

### Different Approaches to Solve the Problem

#### 1. Recursive Approach (Depth-First Search)
This approach uses recursion to explore all possible combinations by treating each digit as a node and each letter as a branch.

#### Steps:
1. Define a mapping of digits to letters.
2. Use a recursive function to build combinations.
3. For each digit, append each corresponding letter to the current combination and recursively call the function for the next digit.
4. When the end of the digit string is reached, add the current combination to the result list.

#### Code:
```java
import java.util.ArrayList;
import java.util.List;

public class LetterCombinations {
    private static final String[] KEYPAD = {
        "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
    };

    public static List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return result;
        }
        dfs(digits, 0, new StringBuilder(), result);
        return result;
    }

    private static void dfs(String digits, int index, StringBuilder path, List<String> result) {
        if (index == digits.length()) {
            result.add(path.toString());
            return;
        }
        String letters = KEYPAD[digits.charAt(index) - '0'];
        for (char letter : letters.toCharArray()) {
            path.append(letter);
            dfs(digits, index + 1, path, result);
            path.deleteCharAt(path.length() - 1);
        }
    }

    public static void main(String[] args) {
        String digits = "23";
        System.out.println(letterCombinations(digits)); // Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
    }
}
```
#### Time Complexity: \(O(4^n)\), where \(n\) is the length of the input string.

#### 2. Iterative Approach
This approach uses an iterative method to build combinations by processing each digit and adding the corresponding letters to the existing combinations.

#### Steps:
1. Define a mapping of digits to letters.
2. Initialize a list with an empty string.
3. For each digit, iterate through the current list of combinations and append each corresponding letter to each combination.
4. Update the list with the new combinations.

#### Code:
```java
import java.util.ArrayList;
import java.util.List;

public class LetterCombinations {
    private static final String[] KEYPAD = {
        "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
    };

    public static List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return result;
        }
        result.add("");
        for (char digit : digits.toCharArray()) {
            List<String> temp = new ArrayList<>();
            String letters = KEYPAD[digit - '0'];
            for (String combination : result) {
                for (char letter : letters.toCharArray()) {
                    temp.add(combination + letter);
                }
            }
            result = temp;
        }
        return result;
    }

    public static void main(String[] args) {
        String digits = "23";
        System.out.println(letterCombinations(digits)); // Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
    }
}
```
#### Time Complexity: \(O(4^n)\), where \(n\) is the length of the input string.

#### 3. Breadth-First Search (BFS) Approach
This approach uses a queue to perform a breadth-first search, generating combinations level by level.

#### Steps:
1. Define a mapping of digits to letters.
2. Initialize a queue with an empty string.
3. For each digit, dequeue the current combinations and enqueue new combinations by appending each corresponding letter.
4. Continue until all digits are processed.

#### Code:
```java
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Deque;
import java.util.List;

public class LetterCombinations {
    private static final String[] KEYPAD = {
        "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
    };

    public static List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return result;
        }
        Deque<String> queue = new ArrayDeque<>();
        queue.add("");
        for (char digit : digits.toCharArray()) {
            int size = queue.size();
            String letters = KEYPAD[digit - '0'];
            for (int i = 0; i < size; i++) {
                String combination = queue.poll();
                for (char letter : letters.toCharArray()) {
                    queue.add(combination + letter);
                }
            }
        }
        result.addAll(queue);
        return result;
    }

    public static void main(String[] args) {
        String digits = "23";
        System.out.println(letterCombinations(digits)); // Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
    }
}
```
#### Time Complexity: \(O(4^n)\), where \(n\) is the length of the input string.

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is intuitive and easy to implement but can be less efficient for large inputs.
- The **iterative approach** is straightforward and avoids the overhead of recursion.
- The **BFS approach** is efficient and processes combinations level by level[1](https://www.javatpoint.com/iterative-letter-combinations-of-a-phone-number)[2](https://blog.heycoach.in/letter-combinations-of-a-phone-number-solution-in-java/)[3](https://algo.monster/liteproblems/17).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Check Permutation

Checking if two strings are permutations of each other means determining if one string can be rearranged to form the other. Here are different approaches to solve this problem in Java:

### 1. Sorting Approach
This approach involves sorting both strings and comparing them. If the sorted versions of the strings are equal, then the strings are permutations of each other.

#### Steps:
1. Check if the lengths of the two strings are equal. If not, they cannot be permutations.
2. Convert both strings to character arrays and sort them.
3. Compare the sorted character arrays.

#### Code:
```java
import java.util.Arrays;

public class PermutationCheck {
    public static boolean arePermutations(String str1, String str2) {
        if (str1.length() != str2.length()) {
            return false;
        }
        char[] charArray1 = str1.toCharArray();
        char[] charArray2 = str2.toCharArray();
        Arrays.sort(charArray1);
        Arrays.sort(charArray2);
        return Arrays.equals(charArray1, charArray2);
    }

    public static void main(String[] args) {
        String str1 = "listen";
        String str2 = "silent";
        System.out.println("Are the two strings permutations of each other? " + arePermutations(str1, str2)); // Output: true
    }
}
```
#### Time Complexity: \(O(n \log n)\) for sorting.

### 2. Character Count Approach
This approach involves counting the frequency of each character in both strings and comparing these counts.

#### Steps:
1. Check if the lengths of the two strings are equal. If not, they cannot be permutations.
2. Use a `HashMap` to count the frequency of each character in the first string.
3. Decrement the count for each character in the second string.
4. If all counts are zero at the end, the strings are permutations of each other.

#### Code:
```java
import java.util.HashMap;

public class PermutationCheck {
    public static boolean arePermutations(String str1, String str2) {
        if (str1.length() != str2.length()) {
            return false;
        }
        HashMap<Character, Integer> charCountMap = new HashMap<>();
        for (char c : str1.toCharArray()) {
            charCountMap.put(c, charCountMap.getOrDefault(c, 0) + 1);
        }
        for (char c : str2.toCharArray()) {
            if (!charCountMap.containsKey(c)) {
                return false;
            }
            charCountMap.put(c, charCountMap.get(c) - 1);
            if (charCountMap.get(c) == 0) {
                charCountMap.remove(c);
            }
        }
        return charCountMap.isEmpty();
    }

    public static void main(String[] args) {
        String str1 = "apple";
        String str2 = "papel";
        System.out.println("Are the two strings permutations of each other? " + arePermutations(str1, str2)); // Output: true
    }
}
```
#### Time Complexity: \(O(n)\)

### 3. Array Count Approach
This approach uses an array to count the frequency of each character, assuming the character set is fixed (e.g., ASCII).

#### Steps:
1. Check if the lengths of the two strings are equal. If not, they cannot be permutations.
2. Use an integer array to count the frequency of each character in the first string.
3. Decrement the count for each character in the second string.
4. If all counts are zero at the end, the strings are permutations of each other.

#### Code:
```java
public class PermutationCheck {
    public static boolean arePermutations(String str1, String str2) {
        if (str1.length() != str2.length()) {
            return false;
        }
        int[] charCount = new int[128]; // Assuming ASCII
        for (char c : str1.toCharArray()) {
            charCount[c]++;
        }
        for (char c : str2.toCharArray()) {
            charCount[c]--;
            if (charCount[c] < 0) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        String str1 = "abc";
        String str2 = "bca";
        System.out.println("Are the two strings permutations of each other? " + arePermutations(str1, str2)); // Output: true
    }
}
```
#### Time Complexity: \(O(n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **sorting approach** is straightforward but involves sorting, which can be less efficient for large strings.
- The **character count approach** is efficient and works well for any character set.
- The **array count approach** is highly efficient but assumes a fixed character set (e.g., ASCII)[1](https://www.javacodegeeks.com/check-if-two-strings-are-permutations-of-each-other-in-java.html)[2](https://www.baeldung.com/java-check-permutations-two-strings)[3](https://www.javatpoint.com/check-string-are-permutation-of-each-other-in-java).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Minimum insertion to make Palindrome

To transform a given string into a palindrome by inserting the minimum number of characters, we can use several approaches. Here are different methods to solve this problem in Java:

### 1. Recursive Approach
This approach uses recursion to explore all possible ways to make the string a palindrome by inserting characters.

#### Steps:
1. If the string is empty or has one character, it is already a palindrome.
2. If the first and last characters of the string are the same, recursively check the substring excluding these characters.
3. If the first and last characters are different, consider two cases:
   - Insert the last character at the beginning.
   - Insert the first character at the end.
4. Return the minimum of the two cases plus one.

#### Code:
```java
public class MinInsertionPalindrome {
    public static int minInsertions(String s) {
        return minInsertionsHelper(s, 0, s.length() - 1);
    }

    private static int minInsertionsHelper(String s, int left, int right) {
        if (left >= right) {
            return 0;
        }
        if (s.charAt(left) == s.charAt(right)) {
            return minInsertionsHelper(s, left + 1, right - 1);
        } else {
            return 1 + Math.min(minInsertionsHelper(s, left + 1, right), minInsertionsHelper(s, left, right - 1));
        }
    }

    public static void main(String[] args) {
        String s = "abc";
        System.out.println("Minimum insertions to make palindrome: " + minInsertions(s)); // Output: 2
    }
}
```
#### Time Complexity: \(O(2^n)\)

### 2. Dynamic Programming Approach
This approach uses a 2D table to store the results of subproblems and avoid redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` represents the minimum insertions needed to make the substring `s[i...j]` a palindrome.
2. Initialize the table for substrings of length 1 (which are already palindromes).
3. Fill the table for substrings of increasing lengths.
4. Use the results of smaller subproblems to solve larger subproblems.

#### Code:
```java
public class MinInsertionPalindrome {
    public static int minInsertions(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];

        for (int length = 2; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[0][n - 1];
    }

    public static void main(String[] args) {
        String s = "abc";
        System.out.println("Minimum insertions to make palindrome: " + minInsertions(s)); // Output: 2
    }
}
```
#### Time Complexity: \(O(n^2)\)

### 3. Longest Palindromic Subsequence Approach
This approach leverages the fact that the minimum number of insertions needed to make a string a palindrome is equal to the length of the string minus the length of its longest palindromic subsequence (LPS).

#### Steps:
1. Find the length of the longest palindromic subsequence in the string.
2. Subtract the length of the LPS from the length of the string to get the minimum insertions needed.

#### Code:
```java
public class MinInsertionPalindrome {
    public static int minInsertions(String s) {
        int n = s.length();
        int lpsLength = longestPalindromicSubsequence(s);
        return n - lpsLength;
    }

    private static int longestPalindromicSubsequence(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];

        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

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
        String s = "abc";
        System.out.println("Minimum insertions to make palindrome: " + minInsertions(s)); // Output: 2
    }
}
```
#### Time Complexity: \(O(n^2)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a quadratic time complexity and is commonly used.
- The **longest palindromic subsequence approach** leverages the LPS to find the minimum insertions efficiently[1](https://www.javatpoint.com/minimum-insertion-to-form-a-palindrome-in-java)[2](https://www.javatpoint.com/minimum-insertions-to-form-a-palindrome)[3](https://algo.monster/liteproblems/1312).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Longest Valid Parenthesis

The "Longest Valid Parentheses" problem involves finding the length of the longest substring of well-formed parentheses in a given string. Here are different approaches to solve this problem in Java:

### Problem Statement
Given a string containing just the characters '(' and ')', return the length of the longest valid (well-formed) parentheses substring.

### Example
```java
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".

Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
```

### Different Approaches to Solve Longest Valid Parentheses

#### 1. Brute Force Approach
This approach involves generating all possible substrings and checking each one to see if it is a valid parentheses substring.

#### Steps:
1. Generate all possible substrings.
2. Check each substring to see if it is valid.
3. Keep track of the length of the longest valid substring found.

#### Code:
```java
public class LongestValidParentheses {
    public static int longestValidParentheses(String s) {
        int maxLength = 0;
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 2; j <= s.length(); j += 2) {
                if (isValid(s.substring(i, j))) {
                    maxLength = Math.max(maxLength, j - i);
                }
            }
        }
        return maxLength;
    }

    private static boolean isValid(String s) {
        int balance = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                balance++;
            } else {
                balance--;
            }
            if (balance < 0) {
                return false;
            }
        }
        return balance == 0;
    }

    public static void main(String[] args) {
        String s = "(()";
        System.out.println("Longest Valid Parentheses: " + longestValidParentheses(s)); // Output: 2
    }
}
```
#### Time Complexity: \(O(n^3)\)

#### 2. Dynamic Programming Approach
This approach uses a dynamic programming table to store the lengths of the longest valid parentheses substrings ending at each index.

#### Steps:
1. Create a `dp` array where `dp[i]` represents the length of the longest valid parentheses substring ending at index `i`.
2. Iterate through the string and update the `dp` array based on the characters and previous values in the array.
3. Keep track of the maximum value in the `dp` array.

#### Code:
```java
public class LongestValidParentheses {
    public static int longestValidParentheses(String s) {
        int maxLength = 0;
        int[] dp = new int[s.length()];
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == ')') {
                if (s.charAt(i - 1) == '(') {
                    dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
                } else if (i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                    dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
                }
                maxLength = Math.max(maxLength, dp[i]);
            }
        }
        return maxLength;
    }

    public static void main(String[] args) {
        String s = ")()())";
        System.out.println("Longest Valid Parentheses: " + longestValidParentheses(s)); // Output: 4
    }
}
```
#### Time Complexity: \(O(n)\)

#### 3. Stack Approach
This approach uses a stack to keep track of the indices of the characters and helps in finding the longest valid parentheses substring.

#### Steps:
1. Initialize a stack and push `-1` onto it to handle the base case.
2. Iterate through the string and push the index of each '(' onto the stack.
3. For each ')', pop the top of the stack and calculate the length of the valid substring.
4. Keep track of the maximum length found.

#### Code:
```java
import java.util.Stack;

public class LongestValidParentheses {
    public static int longestValidParentheses(String s) {
        int maxLength = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
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
        String s = ")()())";
        System.out.println("Longest Valid Parentheses: " + longestValidParentheses(s)); // Output: 4
    }
}
```
#### Time Complexity: \(O(n)\)

#### 4. Two-Pointer Approach
This approach uses two pointers to traverse the string from left to right and right to left, counting the number of '(' and ')' characters.

#### Steps:
1. Initialize two pointers and two counters for left-to-right and right-to-left traversals.
2. Traverse the string from left to right, counting the number of '(' and ')' characters.
3. If the counts are equal, update the maximum length.
4. If the count of ')' exceeds '(', reset the counters.
5. Repeat the process from right to left.

#### Code:
```java
public class LongestValidParentheses {
    public static int longestValidParentheses(String s) {
        int maxLength = 0;
        int left = 0, right = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                left++;
            } else {
                right++;
            }
            if (left == right) {
                maxLength = Math.max(maxLength, 2 * right);
            } else if (right > left) {
                left = right = 0;
            }
        }
        left = right = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == '(') {
                left++;
            } else {
                right++;
            }
            if (left == right) {
                maxLength = Math.max(maxLength, 2 * left);
            } else if (left > right) {
                left = right = 0;
            }
        }
        return maxLength;
    }

    public static void main(String[] args) {
        String s = ")()())";
        System.out.println("Longest Valid Parentheses: " + longestValidParentheses(s)); // Output: 4
    }
}
```
#### Time Complexity: \(O(n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **brute force approach** is simple but inefficient for large inputs due to its cubic time complexity.
- The **dynamic programming approach** is efficient with a linear time complexity and uses extra space.
- The **stack approach** is efficient and easy to implement with a linear time complexity.
- The **two-pointer approach** is also efficient with a linear time complexity and uses constant space[1](https://leetcode.com/problems/longest-valid-parentheses/)[2](https://github.com/cherryljr/LeetCode/blob/master/Longest%20Valid%20Parentheses.java)[3](https://kodeao.com/longest-valid-parentheses-leetcode-32-solution/).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Implement strStr

The `strStr` function, also known as `indexOf`, finds the first occurrence of a substring (needle) within another string (haystack). Here are different approaches to implement this function in Java:

### 1. Naive Approach
This approach involves checking each substring of the haystack to see if it matches the needle.

#### Steps:
1. Iterate through the haystack.
2. For each position, check if the substring starting at that position matches the needle.
3. If a match is found, return the starting index.
4. If no match is found, return -1.

#### Code:
```java
public class StrStr {
    public static int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;
        int haystackLength = haystack.length();
        int needleLength = needle.length();
        for (int i = 0; i <= haystackLength - needleLength; i++) {
            int j;
            for (j = 0; j < needleLength; j++) {
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    break;
                }
            }
            if (j == needleLength) {
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        String haystack = "hello";
        String needle = "ll";
        System.out.println("Index of first occurrence: " + strStr(haystack, needle)); // Output: 2
    }
}
```
#### Time Complexity: \(O((n - m + 1) \cdot m)\), where \(n\) is the length of the haystack and \(m\) is the length of the needle.

### 2. Knuth-Morris-Pratt (KMP) Algorithm
The KMP algorithm improves the naive approach by using a partial match table to skip unnecessary comparisons.

#### Steps:
1. Build the partial match table (also known as the "longest prefix suffix" table) for the needle.
2. Use the table to skip characters in the haystack when a mismatch occurs.

#### Code:
```java
public class StrStr {
    public static int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;
        int[] lps = buildLPS(needle);
        int i = 0, j = 0;
        while (i < haystack.length()) {
            if (haystack.charAt(i) == needle.charAt(j)) {
                i++;
                j++;
                if (j == needle.length()) {
                    return i - j;
                }
            } else if (j > 0) {
                j = lps[j - 1];
            } else {
                i++;
            }
        }
        return -1;
    }

    private static int[] buildLPS(String needle) {
        int[] lps = new int[needle.length()];
        int length = 0;
        int i = 1;
        while (i < needle.length()) {
            if (needle.charAt(i) == needle.charAt(length)) {
                length++;
                lps[i] = length;
                i++;
            } else if (length > 0) {
                length = lps[length - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
        return lps;
    }

    public static void main(String[] args) {
        String haystack = "hello";
        String needle = "ll";
        System.out.println("Index of first occurrence: " + strStr(haystack, needle)); // Output: 2
    }
}
```
#### Time Complexity: \(O(n + m)\)

### 3. Rabin-Karp Algorithm
This approach uses hashing to find the needle in the haystack. It computes a hash for the needle and compares it with the hash of substrings in the haystack.

#### Steps:
1. Compute the hash of the needle.
2. Compute the hash of each substring of the haystack of the same length as the needle.
3. Compare the hashes, and if they match, compare the actual substrings to confirm.

#### Code:
```java
public class StrStr {
    public static int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;
        int m = needle.length();
        int n = haystack.length();
        if (m > n) return -1;

        int base = 256;
        int mod = 101;
        int needleHash = 0, haystackHash = 0, h = 1;

        for (int i = 0; i < m - 1; i++) {
            h = (h * base) % mod;
        }

        for (int i = 0; i < m; i++) {
            needleHash = (base * needleHash + needle.charAt(i)) % mod;
            haystackHash = (base * haystackHash + haystack.charAt(i)) % mod;
        }

        for (int i = 0; i <= n - m; i++) {
            if (needleHash == haystackHash) {
                int j;
                for (j = 0; j < m; j++) {
                    if (haystack.charAt(i + j) != needle.charAt(j)) {
                        break;
                    }
                }
                if (j == m) {
                    return i;
                }
            }
            if (i < n - m) {
                haystackHash = (base * (haystackHash - haystack.charAt(i) * h) + haystack.charAt(i + m)) % mod;
                if (haystackHash < 0) {
                    haystackHash += mod;
                }
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        String haystack = "hello";
        String needle = "ll";
        System.out.println("Index of first occurrence: " + strStr(haystack, needle)); // Output: 2
    }
}
```
#### Time Complexity: \(O(n + m)\) on average, but can degrade to \(O(n \cdot m)\) in the worst case due to hash collisions.

### Conclusion
Each approach has its own advantages and trade-offs:
- The **naive approach** is simple but can be inefficient for large inputs due to its quadratic time complexity.
- The **KMP algorithm** is efficient with linear time complexity and is commonly used for string matching.
- The **Rabin-Karp algorithm** is efficient on average but can degrade in the worst case due to hash collisions[1](https://www.techiedelight.com/implement-strstr-function-java/)[2](https://www.thecodingshala.com/2019/08/implement-strstr-or-indexof-java.html)[3](https://dev.to/rohan2596/leetcode-implement-strstr-with-solution-474a).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Decode String

The "Decode String" problem involves decoding a string that contains encoded patterns. The encoded pattern follows the format `k[encoded_string]`, where the `encoded_string` inside the square brackets is repeated exactly `k` times. Here are different approaches to solve this problem in Java:

### 1. Recursive Approach
This approach uses recursion to decode the string by processing each encoded pattern from the innermost to the outermost.

#### Steps:
1. Define a recursive function to decode the string.
2. Iterate through the string and build the decoded result.
3. When encountering a digit, determine the repeat count.
4. When encountering a '[', recursively decode the substring inside the brackets.
5. Append the decoded substring repeated `k` times to the result.

#### Code:
```java
public class DecodeString {
    public static String decodeString(String s) {
        return decodeHelper(s, new int[]{0});
    }

    private static String decodeHelper(String s, int[] index) {
        StringBuilder result = new StringBuilder();
        int num = 0;
        while (index[0] < s.length()) {
            char c = s.charAt(index[0]);
            if (Character.isDigit(c)) {
                num = num * 10 + (c - '0');
                index[0]++;
            } else if (c == '[') {
                index[0]++;
                String decodedString = decodeHelper(s, index);
                for (int i = 0; i < num; i++) {
                    result.append(decodedString);
                }
                num = 0;
            } else if (c == ']') {
                index[0]++;
                return result.toString();
            } else {
                result.append(c);
                index[0]++;
            }
        }
        return result.toString();
    }

    public static void main(String[] args) {
        String s = "3[a2[c]]";
        System.out.println("Decoded String: " + decodeString(s)); // Output: "accaccacc"
    }
}
```
#### Time Complexity: \(O(n)\)

### 2. Stack Approach
This approach uses a stack to decode the string iteratively by processing each character and managing the encoded patterns.

#### Steps:
1. Initialize two stacks: one for numbers and one for strings.
2. Iterate through the string and build the decoded result.
3. When encountering a digit, determine the repeat count.
4. When encountering a '[', push the current result and repeat count onto the stacks.
5. When encountering a ']', pop from the stacks and append the decoded substring repeated `k` times to the result.

#### Code:
```java
import java.util.Stack;

public class DecodeString {
    public static String decodeString(String s) {
        Stack<Integer> countStack = new Stack<>();
        Stack<StringBuilder> resultStack = new Stack<>();
        StringBuilder current = new StringBuilder();
        int k = 0;

        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                k = k * 10 + (c - '0');
            } else if (c == '[') {
                countStack.push(k);
                resultStack.push(current);
                current = new StringBuilder();
                k = 0;
            } else if (c == ']') {
                StringBuilder decodedString = current;
                current = resultStack.pop();
                for (int i = countStack.pop(); i > 0; i--) {
                    current.append(decodedString);
                }
            } else {
                current.append(c);
            }
        }
        return current.toString();
    }

    public static void main(String[] args) {
        String s = "3[a2[c]]";
        System.out.println("Decoded String: " + decodeString(s)); // Output: "accaccacc"
    }
}
```
#### Time Complexity: \(O(n)\)

### 3. Iterative Approach
This approach uses an iterative method to decode the string by processing each character and managing the encoded patterns without recursion or explicit stacks.

#### Steps:
1. Initialize a result string and a repeat count.
2. Iterate through the string and build the decoded result.
3. When encountering a digit, determine the repeat count.
4. When encountering a '[', push the current result and repeat count onto temporary storage.
5. When encountering a ']', pop from the temporary storage and append the decoded substring repeated `k` times to the result.

#### Code:
```java
public class DecodeString {
    public static String decodeString(String s) {
        StringBuilder result = new StringBuilder();
        int k = 0;
        Stack<Integer> countStack = new Stack<>();
        Stack<StringBuilder> resultStack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                k = k * 10 + (c - '0');
            } else if (c == '[') {
                countStack.push(k);
                resultStack.push(result);
                result = new StringBuilder();
                k = 0;
            } else if (c == ']') {
                StringBuilder temp = result;
                result = resultStack.pop();
                for (int i = countStack.pop(); i > 0; i--) {
                    result.append(temp);
                }
            } else {
                result.append(c);
            }
        }
        return result.toString();
    }

    public static void main(String[] args) {
        String s = "3[a2[c]]";
        System.out.println("Decoded String: " + decodeString(s)); // Output: "accaccacc"
    }
}
```
#### Time Complexity: \(O(n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is intuitive and easy to implement but can be less efficient for deeply nested patterns.
- The **stack approach** is efficient and handles nested patterns well with linear time complexity.
- The **iterative approach** is also efficient and avoids the overhead of recursion[1](https://labex.io/tutorials/java-how-to-safely-decode-string-values-418194)[2](https://www.javaprogramto.com/2020/08/java-base64-encode-and-decode.html)[3](https://www.geeksforgeeks.org/java-string-manipulation-best-practices-for-clean-code/).

If you have any questions or need further clarification on any of these approaches, feel free to ask

## Regular Expression Matching

Regular expression matching is a common problem that involves determining if a given string matches a pattern that includes special characters like `.` and `*`. Here are different approaches to solve this problem in Java:

### Problem Statement
Implement regular expression matching with support for `.` and `*`.
- `.` matches any single character.
- `*` matches zero or more of the preceding element.

### Example
```java
Input: s = "aab", p = "c*a*b"
Output: true
Explanation: The pattern "c*a*b" matches the string "aab" because "c*" can be ignored, and "a*" matches "aa".
```

### Different Approaches to Solve Regular Expression Matching

#### 1. Recursive Approach
This approach uses recursion to match the string with the pattern by handling different cases for `.` and `*`.

#### Steps:
1. If the pattern is empty, return true if the string is also empty.
2. Check if the first character of the string matches the first character of the pattern or if the pattern starts with `.`.
3. If the pattern contains `*`, handle two cases:
   - The `*` matches zero characters.
   - The `*` matches one or more characters.
4. Recursively check the remaining string and pattern.

#### Code:
```java
public class RegexMatching {
    public static boolean isMatch(String s, String p) {
        if (p.isEmpty()) return s.isEmpty();
        boolean firstMatch = (!s.isEmpty() && (p.charAt(0) == s.charAt(0) || p.charAt(0) == '.'));
        if (p.length() >= 2 && p.charAt(1) == '*') {
            return (isMatch(s, p.substring(2)) || (firstMatch && isMatch(s.substring(1), p)));
        } else {
            return firstMatch && isMatch(s.substring(1), p.substring(1));
        }
    }

    public static void main(String[] args) {
        String s = "aab";
        String p = "c*a*b";
        System.out.println("Is Match: " + isMatch(s, p)); // Output: true
    }
}
```
#### Time Complexity: \(O(2^n)\)

#### 2. Dynamic Programming Approach
This approach uses a 2D table to store the results of subproblems and avoid redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` represents if the first `i` characters of the string match the first `j` characters of the pattern.
2. Initialize the table for base cases.
3. Fill the table using the following rules:
   - If the current characters match or the pattern has `.`, update the table based on the previous values.
   - If the pattern has `*`, consider zero or more occurrences of the preceding element.

#### Code:
```java
public class RegexMatching {
    public static boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;

        for (int j = 1; j <= n; j++) {
            if (p.charAt(j - 1) == '*') {
                dp[0][j] = dp[0][j - 2];
            }
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(j - 1) == '.' || p.charAt(j - 1) == s.charAt(i - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 2];
                    if (p.charAt(j - 2) == '.' || p.charAt(j - 2) == s.charAt(i - 1)) {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String s = "aab";
        String p = "c*a*b";
        System.out.println("Is Match: " + isMatch(s, p)); // Output: true
    }
}
```
#### Time Complexity: \(O(m \times n)\)

#### 3. Backtracking Approach
This approach uses backtracking to explore all possible ways to match the string with the pattern.

#### Steps:
1. Define a helper function to perform backtracking.
2. Check if the first character of the string matches the first character of the pattern or if the pattern starts with `.`.
3. If the pattern contains `*`, handle two cases:
   - The `*` matches zero characters.
   - The `*` matches one or more characters.
4. Recursively check the remaining string and pattern.

#### Code:
```java
public class RegexMatching {
    public static boolean isMatch(String s, String p) {
        return isMatchHelper(s, p, 0, 0);
    }

    private static boolean isMatchHelper(String s, String p, int i, int j) {
        if (j == p.length()) return i == s.length();
        boolean firstMatch = (i < s.length() && (p.charAt(j) == s.charAt(i) || p.charAt(j) == '.'));
        if (j + 1 < p.length() && p.charAt(j + 1) == '*') {
            return (isMatchHelper(s, p, i, j + 2) || (firstMatch && isMatchHelper(s, p, i + 1, j)));
        } else {
            return firstMatch && isMatchHelper(s, p, i + 1, j + 1);
        }
    }

    public static void main(String[] args) {
        String s = "aab";
        String p = "c*a*b";
        System.out.println("Is Match: " + isMatch(s, p)); // Output: true
    }
}
```
#### Time Complexity: \(O(2^n)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a quadratic time complexity and is commonly used.
- The **backtracking approach** is intuitive and handles complex patterns well[1](https://www.programcreek.com/2012/12/leetcode-regular-expression-matching-in-java/)[2](https://www.w3schools.com/java/java_regex.asp)[3](https://java8.info/apicontents/regexp.html).

If you have any questions or need further clarification on any of these approaches, feel free to ask!


# Justify Text

Text justification involves formatting a given text so that each line has exactly a specified number of characters and is fully justified (both left and right). Here are different approaches to solve this problem in Java:

### Problem Statement
Given an array of words and a length `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully justified. Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right. For the last line of text, it should be left-justified, and no extra space is inserted between words.

### Example
```java
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output: [
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

### Different Approaches to Solve Text Justification

#### 1. Greedy Approach
This approach packs as many words as possible into each line and then distributes the extra spaces evenly.

#### Steps:
1. Iterate through the words and pack as many words as possible into each line.
2. Calculate the number of spaces needed to fully justify the line.
3. Distribute the spaces evenly between the words.
4. Handle the last line separately to ensure it is left-justified.

#### Code:
```java
import java.util.ArrayList;
import java.util.List;

public class TextJustification {
    public static List<String> fullJustify(String[] words, int maxWidth) {
        List<String> result = new ArrayList<>();
        int index = 0;
        while (index < words.length) {
            int count = words[index].length();
            int last = index + 1;
            while (last < words.length) {
                if (count + words[last].length() + 1 > maxWidth) break;
                count += words[last].length() + 1;
                last++;
            }
            StringBuilder sb = new StringBuilder();
            int diff = last - index - 1;
            if (last == words.length || diff == 0) {
                for (int i = index; i < last; i++) {
                    sb.append(words[i]).append(" ");
                }
                sb.deleteCharAt(sb.length() - 1);
                while (sb.length() < maxWidth) {
                    sb.append(" ");
                }
            } else {
                int spaces = (maxWidth - count) / diff;
                int extraSpaces = (maxWidth - count) % diff;
                for (int i = index; i < last - 1; i++) {
                    sb.append(words[i]).append(" ");
                    for (int j = 0; j < spaces + (i - index < extraSpaces ? 1 : 0); j++) {
                        sb.append(" ");
                    }
                }
                sb.append(words[last - 1]);
            }
            result.add(sb.toString());
            index = last;
        }
        return result;
    }

    public static void main(String[] args) {
        String[] words = {"This", "is", "an", "example", "of", "text", "justification."};
        int maxWidth = 16;
        List<String> justifiedText = fullJustify(words, maxWidth);
        for (String line : justifiedText) {
            System.out.println(line);
        }
    }
}
```
#### Time Complexity: \(O(n)\), where \(n\) is the total number of characters in all words.

### 2. Dynamic Programming Approach
This approach uses dynamic programming to minimize the total cost of extra spaces in the lines.

#### Steps:
1. Define a cost function that penalizes lines with extra spaces.
2. Use dynamic programming to find the optimal way to split the words into lines.
3. Construct the justified text based on the optimal splits.

#### Code:
```java
import java.util.ArrayList;
import java.util.List;

public class TextJustification {
    public static List<String> fullJustify(String[] words, int maxWidth) {
        int n = words.length;
        int[] dp = new int[n + 1];
        int[] breaks = new int[n];
        for (int i = n - 1; i >= 0; i--) {
            dp[i] = Integer.MAX_VALUE;
            int len = -1;
            for (int j = i; j < n; j++) {
                len += words[j].length() + 1;
                if (len > maxWidth) break;
                int cost = (j == n - 1) ? 0 : (maxWidth - len) * (maxWidth - len) + dp[j + 1];
                if (cost < dp[i]) {
                    dp[i] = cost;
                    breaks[i] = j + 1;
                }
            }
        }
        List<String> result = new ArrayList<>();
        int i = 0;
        while (i < n) {
            int j = breaks[i];
            StringBuilder sb = new StringBuilder();
            int len = -1;
            for (int k = i; k < j; k++) {
                sb.append(words[k]).append(" ");
                len += words[k].length() + 1;
            }
            sb.deleteCharAt(sb.length() - 1);
            while (sb.length() < maxWidth) {
                sb.append(" ");
            }
            result.add(sb.toString());
            i = j;
        }
        return result;
    }

    public static void main(String[] args) {
        String[] words = {"This", "is", "an", "example", "of", "text", "justification."};
        int maxWidth = 16;
        List<String> justifiedText = fullJustify(words, maxWidth);
        for (String line : justifiedText) {
            System.out.println(line);
        }
    }
}
```
#### Time Complexity: \(O(n^2)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **greedy approach** is efficient and straightforward, making it suitable for most cases.
- The **dynamic programming approach** can provide an optimal solution but is more complex and may be slower for large inputs[1](https://www.programcreek.com/2014/05/leetcode-text-justification-java/)[2](https://leetcode.com/problems/text-justification/)[3](https://algodaily.com/challenges/text-justification/).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## 0/1 Knapsack

The 0/1 Knapsack problem is a classic problem in combinatorial optimization. It involves selecting items with given weights and values to maximize the total value without exceeding a given weight capacity. Each item can either be included in the knapsack or excluded (hence the name 0/1).

### Problem Statement
Given a set of items, each with a weight and a value, determine the number of each item to include in a collection so that the total weight is less than or equal to a given limit and the total value is as large as possible.

### Example
```java
Input: weights = [1, 3, 4, 5], values = [1, 4, 5, 7], capacity = 7
Output: 9
Explanation: The optimal solution is to take items with weights 3 and 4, which gives a total value of 9.
```

### Different Approaches to Solve 0/1 Knapsack

#### 1. Recursive Approach
This approach uses recursion to explore all possible combinations of items to find the maximum value.

#### Steps:
1. Define a recursive function that considers each item.
2. For each item, decide whether to include it in the knapsack or not.
3. Recursively compute the maximum value for both cases and return the maximum of the two.

#### Code:
```java
public class Knapsack {
    public static int knapsack(int[] weights, int[] values, int capacity) {
        return knapsackHelper(weights, values, capacity, weights.length);
    }

    private static int knapsackHelper(int[] weights, int[] values, int capacity, int n) {
        if (n == 0 || capacity == 0) {
            return 0;
        }
        if (weights[n - 1] > capacity) {
            return knapsackHelper(weights, values, capacity, n - 1);
        } else {
            return Math.max(
                values[n - 1] + knapsackHelper(weights, values, capacity - weights[n - 1], n - 1),
                knapsackHelper(weights, values, capacity, n - 1)
            );
        }
    }

    public static void main(String[] args) {
        int[] weights = {1, 3, 4, 5};
        int[] values = {1, 4, 5, 7};
        int capacity = 7;
        System.out.println("Maximum value: " + knapsack(weights, values, capacity)); // Output: 9
    }
}
```
#### Time Complexity: \(O(2^n)\)

#### 2. Dynamic Programming Approach
This approach uses a 2D table to store the maximum value that can be obtained for each subproblem, avoiding redundant calculations.

#### Steps:
1. Create a 2D array `dp` where `dp[i][j]` represents the maximum value that can be obtained with the first `i` items and a capacity of `j`.
2. Initialize the table for base cases.
3. Fill the table using the following rules:
   - If the current item's weight is less than or equal to the current capacity, consider including it.
   - Otherwise, exclude the item.

#### Code:
```java
public class Knapsack {
    public static int knapsack(int[] weights, int[] values, int capacity) {
        int n = weights.length;
        int[][] dp = new int[n + 1][capacity + 1];

        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= capacity; w++) {
                if (i == 0 || w == 0) {
                    dp[i][w] = 0;
                } else if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(values[i - 1] + dp[i - 1][w - weights[i - 1]], dp[i - 1][w]);
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
        System.out.println("Maximum value: " + knapsack(weights, values, capacity)); // Output: 9
    }
}
```
#### Time Complexity: \(O(n \times W)\), where \(n\) is the number of items and \(W\) is the capacity of the knapsack.

#### 3. Space Optimized Dynamic Programming
This approach optimizes the space complexity of the dynamic programming solution by using a 1D array instead of a 2D array.

#### Steps:
1. Use a 1D array `dp` where `dp[j]` represents the maximum value that can be obtained with a capacity of `j`.
2. Iterate through the items and update the `dp` array from right to left to avoid overwriting values.

#### Code:
```java
public class Knapsack {
    public static int knapsack(int[] weights, int[] values, int capacity) {
        int n = weights.length;
        int[] dp = new int[capacity + 1];

        for (int i = 0; i < n; i++) {
            for (int w = capacity; w >= weights[i]; w--) {
                dp[w] = Math.max(dp[w], values[i] + dp[w - weights[i]]);
            }
        }
        return dp[capacity];
    }

    public static void main(String[] args) {
        int[] weights = {1, 3, 4, 5};
        int[] values = {1, 4, 5, 7};
        int capacity = 7;
        System.out.println("Maximum value: " + knapsack(weights, values, capacity)); // Output: 9
    }
}
```
#### Time Complexity: \(O(n \times W)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a quadratic time complexity and is commonly used.
- The **space-optimized dynamic programming approach** reduces the space complexity while maintaining the same time complexity[1](https://www.javatpoint.com/0-1-knapsack-problem)[2](https://www.javatpoint.com/knapsack-problem-java)[3](https://www.javaguides.net/2023/12/0-1-knapsack-problem-java-solution.html).

If you have any questions or need further clarification on any of these approaches, feel free to ask!

## Coin Change 

The Coin Change problem involves finding the minimum number of coins needed to make up a specific amount of money, given coins of different denominations. Here are different approaches to solve this problem in Java:

### Problem Statement
Given an array of coins representing different denominations and an integer amount representing a total amount of money, determine the fewest number of coins needed to make up that amount. If it is not possible to make up the amount with the given coins, return -1.

### Example
```java
Input: coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

### Different Approaches to Solve Coin Change

#### 1. Recursive Approach
This approach uses recursion to explore all possible combinations of coins to find the minimum number of coins needed.

#### Steps:
1. Define a recursive function that considers each coin.
2. For each coin, decide whether to include it in the current amount or not.
3. Recursively compute the minimum number of coins for both cases and return the minimum of the two.

#### Code:
```java
public class CoinChange {
    public static int coinChange(int[] coins, int amount) {
        if (amount == 0) return 0;
        int result = coinChangeHelper(coins, amount);
        return result == Integer.MAX_VALUE ? -1 : result;
    }

    private static int coinChangeHelper(int[] coins, int amount) {
        if (amount < 0) return Integer.MAX_VALUE;
        if (amount == 0) return 0;
        int minCoins = Integer.MAX_VALUE;
        for (int coin : coins) {
            int res = coinChangeHelper(coins, amount - coin);
            if (res != Integer.MAX_VALUE) {
                minCoins = Math.min(minCoins, res + 1);
            }
        }
        return minCoins;
    }

    public static void main(String[] args) {
        int[] coins = {1, 2, 5};
        int amount = 11;
        System.out.println("Minimum coins needed: " + coinChange(coins, amount)); // Output: 3
    }
}
```
#### Time Complexity: \(O(2^n)\)

#### 2. Dynamic Programming Approach
This approach uses a 1D array to store the minimum number of coins needed for each amount from 0 to the given amount, avoiding redundant calculations.

#### Steps:
1. Create an array `dp` of size `amount + 1` to store the minimum number of coins needed for each amount.
2. Initialize each element in `dp` to a maximum value, and set `dp[0]` to 0.
3. Iterate through each coin, and for each coin, update the `dp` array for all amounts that can be reached using that coin.

#### Code:
```java
import java.util.Arrays;

public class CoinChange {
    public static int coinChange(int[] coins, int amount) {
        int max = amount + 1;
        int[] dp = new int[max];
        Arrays.fill(dp, max);
        dp[0] = 0;

        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }

    public static void main(String[] args) {
        int[] coins = {1, 2, 5};
        int amount = 11;
        System.out.println("Minimum coins needed: " + coinChange(coins, amount)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n \times W)\), where \(n\) is the number of coins and \(W\) is the amount.

#### 3. Breadth-First Search (BFS) Approach
This approach uses BFS to explore all possible combinations of coins level by level, ensuring the shortest path (minimum coins) is found first.

#### Steps:
1. Use a queue to store the current amount and the number of coins used.
2. Use a set to store visited amounts to avoid redundant calculations.
3. For each amount, add the next possible amounts (current amount + each coin) to the queue.
4. If the target amount is reached, return the number of coins used.

#### Code:
```java
import java.util.HashSet;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Set;

public class CoinChange {
    public static int coinChange(int[] coins, int amount) {
        if (amount == 0) return 0;
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        queue.add(amount);
        visited.add(amount);
        int steps = 0;

        while (!queue.isEmpty()) {
            int size = queue.size();
            steps++;
            for (int i = 0; i < size; i++) {
                int current = queue.poll();
                for (int coin : coins) {
                    int next = current - coin;
                    if (next == 0) return steps;
                    if (next > 0 && !visited.contains(next)) {
                        queue.add(next);
                        visited.add(next);
                    }
                }
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] coins = {1, 2, 5};
        int amount = 11;
        System.out.println("Minimum coins needed: " + coinChange(coins, amount)); // Output: 3
    }
}
```
#### Time Complexity: \(O(n \times W)\)

### Conclusion
Each approach has its own advantages and trade-offs:
- The **recursive approach** is simple but can be inefficient for large inputs due to its exponential time complexity.
- The **dynamic programming approach** is more efficient with a quadratic time complexity and is commonly used.
- The **BFS approach** is also efficient and ensures the shortest path (minimum coins) is found first[1](https://www.sourcecodeexamples.net/2023/12/coin-change-java-solution.html)[2](https://www.codespeedy.com/solve-coin-change-problem-in-java/)[3](https://www.sixmedium.com/coin-change/).

If you have any questions or need further clarification on any of these approaches, feel free to ask!


