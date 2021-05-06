[922.按照奇偶排序数组II](https://leetcode-cn.com/problems/sort-array-by-parity-ii/solution/an-qi-ou-pai-xu-shu-zu-ii-by-leetcode-solution/)

方法一中用一个新的数组来接收，通过两次遍历实现

方法二中的话用双指针，用i和j分别维护奇数和偶数的情况

```python
class Solution:
	def sortArrayByParity(self,nums):
		n=len(nums)
		j=1
		for i in range(0,n,2):
			if nums[i]%2==1:
				while nums[j]%2==1:
					j+=2
			nums[j],nums[i]=nums[i],nums[j]
		return nums
```
