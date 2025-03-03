A peak element is an element that is strictly greater than its neighbors.

Given a 0-indexed integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in O(log n) time.

____________________________________________________________________________________________________

Intuition & Thoughts:   
  This is an example of a problem that is worded in a confusing way to throw off the solver. We are asked to find any peak element. A peak
  is any element that is higher than both its neighbors. Now notice that we can return ANY peak. In other words, we are looking for any local
  maximum. The third line is also confusing (nums[-1] = nums[n] = -∞). All this means is that the ground behind index 0 and ahead of index n
  should be treated as -∞.

  Now we can simply return the max of the array, but this leads to a TLE, and the question states clearly that a O(log n) time solution is 
  required. We know that linear search (finding the max) does not work, and that a O(log n) solution does work, so it is obvious that we use 
  binary search here.

  Now the wierd thing here is that the input is NOT sorted, so how do we apply binary search to find a peak? Well, the way to look at this
  problem is to imagine a drawing. We start with the left pointer at index 0, and right pointer at index n. Now go to the middle.

  In the middle there are three possibilities. 
    1 - The middle element is on a hill. This means that on one side of it we are going down, and the other side we are going up (meaning 
        that the peak is on the side that is going up)
    2 - The middle element is a relative minumum (meaning there is a peak if we go torwards either side)
    3 - The middle element is the relative maximum itself (meaning both sides are lower and we should return)
  
  This drawing shows all three possibilities:
  ![All Possible Options for Middle Node](https://github.com/AsgharKazmi2005/Algorithmic-Study/blob/main/Images/LCM162-Diagram.png)
  
  So simply in out binary search we get the middle between the left and right pointer, and handle it conditionally based on the above rules.
  Rules 1 and 2 can be combines as we can user >= to explicitly choose left or right in the case where we could go either way. We continue
  looping using the above conditionals until both the left and right pointers arrive on the same node. This is guaranteed to be a local maximum.
  (Note that no two adjacent nodes have the same height value, so plateaus do not exist.)
_______________________________________________________________________________________________________________________________________

Implementation:

    class Solution:
      def findPeakElement(self, nums: List[int]) -> int:
          l,r = 0, len(nums)-1
    
          while l<r:
              m=(l+r)//2
              
              if nums[m] > nums[m+1]:
                  r=m
              else:
                  l=m+1
          return r
                              
                        
                                                        

