题目：给定一个字符串，找出不含有重复字符的最长子串的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 无重复字符的最长子串是 "abc"，其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 无重复字符的最长子串是 "b"，其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 无重复字符的最长子串是 "wke"，其长度为 3。
     请注意，答案必须是一个子串，"pwke" 是一个子序列 而不是子串。

优化的滑动窗口方法：
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        <!-- """
        :type s: str
        :rtype: int
        """ -->
        start=maxlenth=0  //start记录滑动窗口目前的初始位置
        charset={}        //存放字符串的每个字符，有重复则覆盖，key为字符，value为下标，value表示的是一个字符的最大下标。
        for i in range(len(s)):
            if s[i] in charset and start<=charset[s[i]]:
                start=charset[s[i]]+1   //若s[i]与charset中的某字符重复，即字符串中对应下标为charset[s[i]]的字符，则直接跳过start-charset[s[i]]之间的字符串，从charset[s[i]]+1开始滑动
            else:
                maxlenth=max(maxlenth,i-start+1)
            charset[s[i]]=i
        return maxlenth

对于字符串s:pwkwaplkbx:
Start=maxlenth=0
见图片 Longest Substring Without Repeating Characters

charset c{}：
i=0    start=0  maxlenth=i-start+1=1   c[p]=0  
i=1    start=0  maxlenth=i-start+1=2   c[w]=1
i=2    start=0  maxlenth=i-start+1=3   c[k]=2
i=3    s[3]=w in c && start=0<c[w] start=c[w]+1=1+1=2  maxlenth=max(i-start+1=2,maxlenth)=3 目前最长的字符串为pwk  c[w]=3 过滤掉pw，下次从k开始
i=4    start=2  maxlenth=3   c[a]=4
i=5    p在集合中 start=2>c[p]=0 maxlenth=(maxlenth,i-start+1)=4 目前最长的字符串为kwap c[p]=5
i=6    start=2  maxlenth=5  目前最长的字符串为kwapl c[l]=6
i=7    k在集合中 start<=c[k]=2  start=c[k]+1=3 maxlenth=5  c[k]=7目前最长的字符串仍为kwapl  start过滤掉第一个k，下次从w开始
i=8    start=3  maxlenth=max(maxlenth,i-start+1)=6    目前最长的字符串为waplkb 
i=9    start=3 maxlenth=7 目前最长的字符串为waplkbx

！！！滑动窗口直接跳过 当前start 到 与当前字符重复的字符之间的字符串。从重复字符的下一个字符开始。
复杂度 O(n)

法二：暴力方法：
java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int maxl=0;
        for(int i=0;i<s.length();i++){
            for(int j=i+1;j<=s.length();j++){
                if(allunique(s,i,j)){
                    maxl=Math.max(maxl,j-i);
                }
            }
        }
        return maxl;
    }
    public boolean allunique(String s,int start,int end) {
        Set<Character> hm=new HashSet<>();
        for(int i=start;i<end;i++){
            if (hm.contains(s.charAt(i))){
                return false;
            }else{
             hm.add(s.charAt(i));
            }
        }
        return true;
    }
}

先将字符串s分为子字符串，然后检查每个子字符串是否为unique，若是，返回长度j-i
复杂度 O(n^3)

法三： 简单的滑动窗口方法
python 
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        charset={}
        maxlength=0
        i=j=0
        while i<len(s) and j<len(s):
            if not s[j] in charset:
                maxlength=max(maxlength,j-i+1)
                charset[s[j]]=j
                j=j+1
            else:
                charset.pop(s[i])
                i=i+1
        return maxlength

每次比较出现重复字符，仅向前移一位，i为滑动窗口的首位置，j为窗口末位置。 若出现与s[j]重复,则i++，不重复，j++ 复杂度O（2n）=O(n) 最坏情况每个字母被i，j访问两次。

注意：python中没有形如java的自增 i++,i-- 要用i=i+1表示 
因为 python 中，变量是以内容为基准而不是像 c 中以变量名为基准，所以只要你的数字内容是5，不管你起什么名字，这个变量的 ID 是相同的，同时也就说明了 python 中一个变量可以以多个名称访问，正确的自增操作应该 
a = a + 1 或者 a += 1，当此 a 自增后，通过 id() 观察可知，id 值变化了，即 a 已经是新值的名称
