题目：给定两个非空链表来表示两个非负整数。位数按照逆序方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。
你可以假设除了数字 0 之外，这两个数字都不会以零开头。
示例：
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
	
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """

        l3=ListNode(0) //链表头插入0
        print l3.val // 0
        dummy=l3 //dumyy现在指向l3的链表头0 哑节点
        print dummy.val //0
        carry=0 //进位
        while l1!=None or l2!=None or carry!=0:
            sum=carry   //对于每一位相加都要初始化sum
            if l1!=None:
                sum+=l1.val
                l1=l1.next
            if l2!=None:
                sum+=l2.val
                l2=l2.next
            carry=sum/10
            l3.next=ListNode(sum%10)
            l3=l3.next
            print dummy.val
        return dummy.next 
注意：dummy=l3  链表内容为[0,7,0,8] dummy现在依然指向链表头0，因此要用next  指向剩下的[7,0,8]
     本题不要被“逆序”迷惑，相比于普通的加法，只是进位加在后位上了。 可以直接用链表进行顺位相加，复杂度低。若先逆序再相加，则需要遍历两次链表，一次逆序，一次相加。
