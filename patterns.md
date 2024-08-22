# Problem Solving Patterns

To be effective at solving a given algorithmic problem, or to have a wider creative vision when it comes to algorithm design, it helps to understand various approaches to problem solving. Knowing common patterns

- makes it easier to find solutions
- helps with efficient space/time complexity
- boosts confidence in problem solving
- allows you to see more than one solution to a problem

This file contains several known patterns with examples. Examples are written in Python.

- [Three Pointer Technique](#three-pointer-technique)
- [Frequency Counter](#frequency-counter)
- [Sliding Window](#sliding-window)
- [Divide and Conquer](#divide-and-conquer)

</br>

# Three pointer technique

This technique is useful for tracking multiple indices in multiple lists, such as merging 2 arrays into a single sorted array. For this example, sorting begins in reverse, starting at the end of the array.

Given this sample problem, how can this technique be employed?

<pre>
<i>You are given two integer arrays <code>nums1</code> and <code>nums2</code>, sorted in non-decreasing order, 
and two integers m and n, representing the number of elements in <code>nums1</code> and <code>nums2</code> respectively.</i>

<i>Merge <code>nums1</code> and <code>nums2</code> into a single array sorted in non-decreasing order.</i>

<i>The final sorted array should not be returned by the function, but instead be stored inside the array <code>nums1</code>. 
To accommodate this, <code>nums1</code> has a length of m + n, where the first m elements denote the elements that should 
be merged, and the last n elements are set to 0 and should be ignored. <code>nums2</code> has a length of n.</i>
</pre>

- 3 pointers are used

  - <code>p1 = m - 1</code>
  - <code>p2 = n - 1</code>
  - <code>p = m + n - 1</code>

- Given the following function signature:

<code>def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:</code>

- and input:

<code>merge([1, 2, 3, 0, 0, 0], 3, [2, 5, 6], 3)</code>

- how can we use these pointers?

### How it works

<code>nums1 = [1, 2, 3, 0, 0, 0]</code></br>
<code>nums2 = [2, 5, 6]</code></br>
<code>m = 3</code></br>
<code>n = 3</code></br>

<pre>
<code>
    [1, 2, 3, 0, 0, 0]
           ^        ^
           p1       p

    [2, 5, 6]
           ^
           p2
</code>
</pre>

- While there are still elements to sort in <code>nums2</code>, compare <code>p1</code> and <code>p2</code> and update <code>p</code> as required

<pre>
<code>
    while p2 >= 0:
        if p1 >= 0 and nums1[p1] > nums2[p2]:
            nums1[p] = nums1[p1]
            p1 -= 1
            p -= 1
        else:
            nums1[p] = nums2[p2]
            p2 -= 1
            p -= 1 
</code>
</pre>

- Is 6 > 3? Yes, so we update <code>p</code> and decrement <code>p</code> and <code>p2</code>:

<pre>
<code>
    [1, 2, 3, 0, 0, 6]
           ^     ^
           p1    p

    [2, 5, 6]
        ^
        p2
</code>
</pre>

- Is 5 > 3? Yes, so we update <code>p</code> and decrement <code>p</code> and <code>p2</code>:

<pre>
<code>
    [1, 2, 3, 0, 5, 6]
           ^  ^
           p1 p

    [2, 5, 6]
     ^
     p2
</code>
</pre>

- Is 2 > 3? No, so we update <code>p</code> and decrement <code>p</code> and <code>p1</code>:

<pre>
<code>
    [1, 2, 3, 3, 5, 6]
        ^  ^
        p1 p

    [2, 5, 6]
     ^
     p2
</code>
</pre>

- Is 2 > 2? No, so we update <code>p</code> and decrement <code>p</code> and <code>p1</code>:

<pre>
<code>
    [1, 2, 2, 3, 5, 6]
     ^  ^
     p1 p

    [2, 5, 6]
     ^
     p2
</code>
</pre>

- Is 2 > 1? Yes, so we update <code>p</code> and decrement <code>p</code> and <code>p2</code>:

<pre>
<code>
    [1, 2, 2, 3, 5, 6]
     ^
    p1/p

    [2, 5, 6]
  ^
  p2   <i># p2 is now less than 0, breaking the loop and leaving nums1 sorted</i>
</code>
</pre>

</br>

# Frequency Counter

This technique is useful for comparing values when frequency of occurrence is an important factor.

Given this sample problem, how can this technique be employed?

<pre>
<i>Write a function called <b>same(arr1, arr2)</b> that accepts 2 lists as input and returns True if every value in arr2 corresponds to the square of each value in arr1. The ordering is not important.</i>
</pre>

- Given the following function signature:

<code>def same(arr1: List[int], arr2: List[int]) -> bool:</code>

- and input:

<code>same([1, 2, 3], [9, 1, 4])</code>

### How it works

Consider the following implementation

<pre>
<code>
def same(arr1, arr2) -> bool:
    # check if either list is None or lengths do not match
    if arr1 is None or arr2 is None or (len(arr1) != len(arr2)):
        return False
    
    # declare x2 dictionaries to store counts
    nums1 = same_helper(arr1)
    nums2 = same_helper(arr2)
    
    # check to see if each key in nums1 has the value squared as a key in nums2
    for key in nums1:
        if key ** 2 not in nums2:
            return False
    
    # check to see if the value count is equal in both dictionaries
    for key, value in nums1.items():
        if value != nums2[key ** 2]:
            return False
    
    # return True if everything passes
    return True


def same_helper(arr) -> dict:
    # create a dictionary of list values and their frequency
    nums = {}
    for el in arr:
        if el not in nums:
            nums[el] = 1
        else:
            nums[el] += 1
    return nums
</code>
</pre>

# Sliding Window

</br>

# Divide and Conquer
