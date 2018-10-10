题目：将字符串 "PAYPALISHIRING" 以Z字形排列成给定的行数：

P   A   H   N
A P L S I I G
Y   I   R
之后从左往右，逐行读取字符："PAHNAPLSIIGYIR"

实现一个将字符串进行指定行数变换的函数:

string convert(string s, int numRows);
示例 1:

输入: s = "PAYPALISHIRING", numRows = 3
输出: "PAHNAPLSIIGYIR"
示例 2:

输入: s = "PAYPALISHIRING", numRows = 4
输出: "PINALSIGYAHRPI"
解释:

P     I    N
A   L S  I G
Y A   H R
P     I

解法：
法一，按行访问 O(n),n=len(s)
。  。0
。。。i
。  。numRows-1
共numRows行，第k列元素在s中的索引如下：k从0开始，while 索引<len(s)
第0行：k(2*numRows-2)
第i行：k(2*numRows-2)+i（直线上的元素） ，(k+1)(2*numRows-2)-i（斜线上的元素）
第numRows-1行：k(2*numRows-2)+numRows-1
令循环变量为cycle=2*numRows-2
python代码如下：
class Solution(object):
    def convert(self, s, numRows):
        cycle=2*numRows-2
        if len(s)==1:
            return s
        rstr=[]
        for i in range(numRows):
            j=0
            while j+i<len(s): 
                rstr.append(s[j+i])
                //内部行斜线元素
                if i!=0 and i!=numRows-1 and j+cycle-i<len(s):
                    rstr.append(s[j+cycle-i])  //j+cycle 即(k+1)*cycle
                j=j+cycle
        return "".join(rstr) //list转str
注意：在python中for循环的循环变量不能被改变，while可以。

java代码：
class Solution {
    public String convert(String s, int numRows) {
		if (numRows == 1) return s;
		        StringBuilder ret=new StringBuilder();
		        int cycle=2*numRows-2;
		        for(int i=0;i<numRows;i++){
		            for(int j=0;j+i<s.length();j+=cycle){
		                ret.append(s.charAt(j+i));
		                if(i!=0&&i!=numRows-1&&j+cycle-i<s.length()){
		                    ret.append(s.charAt(j+cycle-i));
		                }
		            }
    }
}
        }
        return ret.toString();
        
法二：按行排序
定义布尔变量down，
当i=0时，down=true，向下访问下一行，s的下一个元素放在i++行的字符串中
当i=numRows-1时，down=false，向上访问，s的下一个元素放在i--行的字符串中
数据结构，字符串数组rows=[""]*min(numRows,len(s)) 最多有min(numRows,len(s))行
每行保存一个字符串
python代码：
class Solution(object):
    def convert(self, s, numRows):
		if len(s)==1 or numRows==1:
		            return s
		        rows=[""]*min(numRows,len(s))
		        i=0
		        down=True
		        for j in range(len(s)):
		                rows[i]=rows[i]+s[j]
		                if down:
		                    i=i+1
		                else:
		                    i=i-1
		                if i==0 or i==numRows-1:
		                    down=not down
		        rstr=""
		        for k in range(len(rows)):
		            rstr=rstr+rows[k]
		        return rstr  或者return “”.join(rows)
