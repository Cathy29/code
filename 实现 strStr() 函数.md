题目：实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例 1:

输入: haystack = "hello", needle = "ll"
输出: 2
示例 2:

输入: haystack = "aaaaa", needle = "bba"
输出: -1
说明:

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

解法：
暴力法，haystack指针为i，needle指针为j，haystack[i]和needle[j]不匹配，回溯i，到本次字符串匹配的最前面。

class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if needle=="":
            return 0
        if len(needle)>len(haystack):
            return -1
        i=0
        j=0
        while i<len(haystack) and j<len(needle):
            if haystack[i]==needle[j]:
                temp=i+1
                j+=1
                while temp<len(haystack) and j<len(needle) and haystack[temp]==needle[j]:
                    temp+=1
                    j+=1
                if j==len(needle):
                    return i
                else:
                    j=0
                    i+=1
            else:
                i+=1
                j=0
        return -1
解法二：kmp
i无需回溯，j需要用next[j]找到回溯的位置。
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if needle=="":
            return 0
        if len(needle)>len(haystack):
            return -1
        i=0
        j=0
        cnext=getnext(needle)
        while i<len(haystack) and j<len(needle):
            if j==-1 or haystack[i]==needle[j]:
                i+=1
                j+=1
            else:
                j=cnext[j]
            if j==len(needle): #每次都会j++
                return i-j
        if j==len(needle):
                return i-j
        else:
            return -1
def getnext(p):
    rnext=[]
    for i in range(len(p)):
        rnext.append(0)
    rnext[0]=-1
    j=0
    k=-1
    while j!=len(p)-1 and k!=len(p)-1:
        if k==-1 or p[j]==p[k]:
            j+=1
            k+=1
            if p[j]==p[k]:
                rnext[j]=rnext[k]
            else:
                rnext[j]=k
        else:
            k=rnext[k]
    return rnext
注：
当P[k] == P[j]时，
if p[++j] == p[++k]: next[j] = next[k] 
else: next[j]=k (此时的j,k已经在前面的判断语句++过了)
当P[k] != P[j]时，
有k = next[k]
具体的kmp算法见另一篇 “kmp详解”