题目：给定一个整数数组和一个目标值，找出数组中和为目标值的两个数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]

class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        # method 1 暴力
        # l=[] //list 数组
        # for i in range(len(nums)):
        #     for j in range(i+1,len(nums)):
        #         if nums[i]+nums[j]==target:
        #             l.append(i)
        #             l.append(j)
        #             return l
        
        # method 2 最佳 一次hash
        dt={} //字典dict，就是java中的hashmap
        for i,value in enumerate(nums):
             
             match=target-value
             print match
             if match in dt.keys() and dt[match]!=i:
                    return [dt[match],i]
             dt[value]=i //要最后再插入字典赋值，否则容易造成同样的key插入导致错误。
            
        #method 3 python dict不允许key相同或重复，两次hash不可用。
        #dt={}
        #for i,value in enumerate(nums):
        #   dt[value]=i
                    
        #for key in dt.keys():
        #   match=target-key
        #   if match in dt.keys() and dt[match]!=dt[key]:
        #       return [dt[key],dt[match]]
注意：本题中使用hash 要用value作为键，下标作为值，因为dict无法根据值返回键，最终结果要的是下标。