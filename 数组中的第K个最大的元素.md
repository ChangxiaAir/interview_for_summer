[215.数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

## 通过partition减治
**借助partition操作定位到最终排定以后索引为len-k的那个元素**
分析：我们在快速排序中接触到的第一个操作就是partition，partition操作，使得：
- 对于某个j，nums[j]已经排定，即nums[j]经过partition操作以后会放置在它最终应该放置的地方
- nums[left]到nums[j-1]中的所有元素都不大于nums[j]
- nums[j+1]到nums[right]中的所有元素都不小于nums[j]

partition（切分）操作总是能排定一个元素，还能够知道这个元素它最终的位置，这样经过一次partition操作就能够缩小搜索范围，也就能够实现减而治之。

切分过程可以不借助额外的数组空间，仅通过交换数组元素实现

```python
class Solution:
	def findKthLargest(self,nums,k):
		size=len(nums)
		
		target=size-k
		left=0
		right = size-1
		while True:
			index=self.partition(nums,left,right)
			if index==target:
				return nums[index]
			elif index<target:
				left=index+1
			else:
				right=index-1
		
		# 循环不变量：[left+1,j]<pivot
		#(j,i)>=pivot
		def partition(self,nums,left,right):
			pivot=nums[left]
			j=left
			for i in range(left+1,right+1):
				if nums[i]<pivot:
					j+=1
					nums[i],nums[j]=nums[j],nums[i]
			nums[left],nums[j]=nums[j],nums[left]
			return j
```
