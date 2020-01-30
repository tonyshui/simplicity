---
subheadline: 'it\'s grind szn'
title: 'The Blind 75'
image: ''
fullwidth: true
embed: ''
youtube: ''
link: ''
quote: ''
#
# If you need a caption, just uncomment the following lines
#
# caption: ''
# caption_url: ''
---
Technical Prep
<!--more-->

1. Two Sum

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        

        #one pass
        value_index = {} #create map with key = array value, and value = index
        for index, array_val in list(enumerate(nums)): #(2,0), (7,1), (11,2), (15,3)
            if target - array_val in value_index:
                return [index, value_index[target - array_val]]
            else: #target - array_val is not yet in value_index
                value_index[array_val] = index
                continue
```
Complexity Analysis: 


- Time Complexity: O(n) to traverse list of n elements in nums
- Space Complexity: O(n) to create hash table


121. Best Time to Buy and Sell Stock
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) == 0:
            return 0
        max_profit = (0,0) #profit, day sold
        min_price = (prices[0], 0) #min price, day bought
        for day, price in list(enumerate(prices)): # (0,7), (1,1), (2, 5), (3, 3), (4,6), (5,4)
            if price < min_price[0]: #set new min price
                min_price = (price, day)
            if price - min_price[0] > max_profit[0] and day > min_price[1]:
                max_profit = (price - min_price[0], day)
        return max_profit[0]
```

Contains Duplicate easy
	set membership, .add (insertion complexity?)

Product of array except self
	geeks for geeks, range (start, stop, step)
	range is not necessarily stop - 1
	left subarray product * right subarray product

	constant space?
	initialize first, appending
	running right array product
	* operator is best way to initialize arrays vs. list comprehensions (unless for 2d arrays), for loops, and while loops


Maximum Subarray
	Kadane’s algorithm
	largest contiguous sum of array elements

Maximum product subarray
	track max and min, magnitude, or potential, realized with a negative factor

Minimum in rotated sorted array

	mid = left + (right - left) // 2 if concerned about overflow

Search in rotated sorted array
	first pass, find minimum
	binary searches on ‘two’ sorted subarrays
	hindsight: use helper functions, lots of code duplication
	challenge myself to implement it recursively with helper functions

3 sum
	modified 2 sum approach
	faster than only 5.02%, and used less memory than 9.61 percent
	yikes

Container with most water
	never move the longer leg
	if equal, arbitrary, only way it can be better is if there are two taller lines, which must eventually be reached

Sum of Two Integers
	back to back swe
	doesn’t take into account negative ints, challenge to go back to this one and do it

Number of 1 bits
	did I think I was swift for finding a O(logn^2) solution, yes sue me
	my trick was to just keep count of how many times I would subtract exponents of two, making sure to subtract the 	right one

	After looking at the solution, I now see that you can do other approaches
		loop with a continuously shifting mask

Counting bits of ‘I’ from 0 < I < n
	simple approach O(n) * O(k) where k is number of bits in integer, in python 32
	
	pop count, which utilizes the bit manipulation trick with the least significant bit and n = n & (n-1), the number of times 	you pop will be equal to the number of bits (each of which will at some point be the least significant bit in (n & n-1)

	Theres an extremely elegant solution, which I don’t quite understand, only knocking down the efficiency by a 	constant factor, so not an extreme upgrade, but may be worth looking into in the future

Missing-number

	Brute force approach is to sort the array, and when you are making a pass, if the next int is not equal to the previous 	int plus 1, then theres a gap. that gap is the missing number O(n log n)
        
        Another approach would be to use a set. This trades time complexity for space complexity. O(1) to check membership 	of a set, but you will need to store n - 1 items, so space complexity is O(n), while time complexity will be O(n).
        
        They are looking for constant extra space complexity, not linear extra space complexity....hmmmmmm
        
        Are there any properties with summing numbers from 0 to n? Looked it up, the summation of an arithmetic series is n/	2(a1 + an)
        
        That is, if n = 10, the summation of a series should be 5(1 + 10) = 55
        
        If one of the values was missing (i.e. 5), the sum of the array would be 50, short 5 of the actual needed summation! 	Ok let's do this

	After I looked at the solution, I understood why this question was filtered under ‘binary’
	if you xor every index and value (not needed to sort), take advantage of XOR’s commutative property, the missing 	value will bubble out, every index and value will match up with each other and xor to a 0, revealing the index 	without a matching value!!

reverse bits
	
	& gives you the least significant bit


Dynamic Programming my fav :D

Climbing Stairs

	Dynamic Programming (memoization)
	tabulation also works

	Optimal Substructure: A given problems has Optimal Substructure Property if optimal solution of the given problem can be obtained by using optimal solutions of its subproblems.

Coin Change
	
	dynamic programming
	top down complexities

	bottom up complexities

Longest Increasing Subsequence
	dynamic programming, no recursion
	O(n^2) time complexity


Merge k-sorted lists
	min heap
	challenge: try it recursively!


Graph valid tree
	DFS, adjacency matrix, 2 conditions

Rotate matrix
	transpose, flip
	discovered rule that the row index becomes the column index

Other:

Reverse Words in a string
	split method
	join method
	reversed (reverse iterator)

Reverse Words in a String III
	reversing a string
	string[::-1]

	zip and map w/lambda




Simple Database API
import copy
class Solution:
  
  '''
  1. create a db
  2. take snapshot on write --> update only the key that's been updated
  3. jkdlfjklfjkl
  4. jkaldfakl
  '''
  
  current_version = 0
  db = {}
  # create tracker dictionary that maps from key = item name, value = version with its last 
  def __init__(self):
    self.db[0] = {}
  def get_val(self, key):
    return self.db[self.current_version][key]
  def set_val(self, key, val):
    self.db[self.current_version][key] = val
  def take_snapshot(self):
    ssid = self.current_version
    self.current_version += 1
    self.db[self.current_version] = copy.deepcopy(db[self.current_version - 1])
    return ssid
  def get_snapshot_val(self, ssid, key):
    if ssid > self.current_version:
      return "invalid ssid"
    else:
      return self.db[ssid][key]
      
database = Solution()
database.set_val("name", "Vineet")
print(database.get_val("name"))






