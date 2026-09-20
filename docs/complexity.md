# Complexity Analysis and Performance Report

This lab compares two correct approaches to the same problem. The goal is not simply to get the right answer, but to observe how algorithmic design changes runtime.

The benchmark output is written in CSV format and can be analyzed in Python, Excel, or a plotting tool.

## Tie-breaking rule for the frequency problem

When two values have the same frequency, the implementation returns the smaller numeric value.

This rule is used in both the naive and efficient implementations so the results are comparable.

## Problem 1 — Duplicate detection

### Algorithm A: Brute force

- Description: compare every pair of values in the array.
- Time complexity: O(n^2)
- Space complexity: O(1)
- Why: for each of n values, the code may compare against up to n - 1 other values.

### Algorithm B: Hash set

- Description: insert each value into a hash set; if a value is already present, a duplicate exists.
- Time complexity: O(n) average case
- Space complexity: O(n)
- Why: each value is inserted and looked up in expected constant time.

### Experimental comparison

1. The hash set implementation was much faster than the brutw force implementation at all tested input size.
2. At 1000 elements, the brute force implementation took about 1.7 ms, while the hash set implementation took about 0.12 ms.
3. At 10,000 elements, the brute force implementation took about 118 ms, while the hash set took about 0.82 ms.
4. At 100,000 elements, the brute force implementation took about 11,798 ms, while hash set implementation took about 8.5 ms.
5. The brute force runtime increased much more rapidly as the input size increased, which is consistent with its O(n^2) time complexity. The hash set implementation uses extra memory, but its average case O(n) runtime makes it much faster for large inputs.


## Problem 2 — Most frequent value

### Algorithm A: Naive counting

- Description: for each value, scan the whole array and count occurrences.
- Time complexity: O(n^2)
- Space complexity: O(1)
- Why: each value may require a full pass through the array.

### Algorithm B: Hash table counts

- Description: count frequencies in one pass and then inspect the counts.
- Time complexity: O(n) average case
- Space complexity: O(n)
- Why: hash table operations are expected to be constant time per value.

### Experimental comparison

1. The hash table implementation was much faster than naive implementation at all tested input sizes.
2. At 1000 elements, naive implementation took about 2.0 ms, while the efficient implementation took about 0.043 ms.
3. At 10,000 elements, naive implementation took about 192 ms, while the efficient implementation took about 0.36 ms.
4. At 100,000 elements, the completed trials for the naive implementation took about 19,153 ms, while the efficient implementation took about 3.4 ms. The benchmark was stopped before all five trials could finish because the naive implementation became very slow.
5. The large increase in runtime for the naive implementation is consistent with its O(n²) time complexity. The efficient implementation uses extra memory for the frequency table, but its average case O(n) runtime reduces the amount of repeated work alot.


## Problem 3 — Common elements between two arrays

### Algorithm A: Naive scan

- Description: take each value from the first array and scan the second array to see whether it appears there.
- Time complexity: O(n × m)
- Space complexity: O(k), where k is the number of distinct values found in common
- Why: each of the n values in the first array may require checking all m values in the second.

### Algorithm B: Hash-based lookup

- Description: construct a hash set from the second array, then examine each value in the first array.
- Time complexity: O(n + m) average case
- Space complexity: O(m)
- Why: set construction and lookup are each expected constant time per element.

### Experimental comparison

1. Naive scan and hash based lookup implementations had similar measured runtimes at the smaller input sizes tested.
2. At 1000 elements, naive implementation took about 0.09–0.11 ms, while the efficient implementation took about 0.08 ms.
3. At 10,000 elements, naive implementation took about 0.80–0.91 ms, while the efficient implementation took about 0.66–0.90 ms.
4. The benchmark did not complete the 100,000-element test for this problem because the overall benchmark was stopped while the naive frequency experiment was running.
5. The theoretical complexities are still different: the naive approach is O(n × m), while the hash based approach is O(n + m) on average. The hash based approach also uses additional memory to store the values from the second array and the common values.


## Observations

The efficient versions are empirically faster because they reduce repeated work. The naive versions do the same comparisons again and again, which scales poorly as input size increases. The faster algorithm usually uses extra memory, which is the standard tradeoff in algorithm design.

The benchmark used input sizes up to 100,000 elements for the naive algorithms. The 1,000,000-element test was not completed because the naive implementations became very slow at 100,000 elements. For example, the duplicate naive algorithm took about 11.8 seconds per trial, and the frequency naive algorithm took about 19 seconds per completed trial at 100,000 elements. The README file allows a smaller maximum when the naive algorithm becomes too slow.

