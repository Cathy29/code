题目：
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：

给定的 n 保证是有效的。
解法：
法一：
遍历两遍：
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        p=head
        lenth=0 #链表长度
        while p!=None:
            p=p.next
            lenth+=1 #第一次遍历，计算链表长度
        index=lenth-n #得到待删除元素的下标
        rlist=ListNode(0)
        result=rlist
        temp=head
        j=0
        while j<lenth:
            if j!=index:
                j+=1
                rlist.next=ListNode(temp.val) #！！！此处不能写作rlist.next=temp ,因为temp是指一个链表，temp连着的所有节点都会被挂在rlist后面
                rlist=rlist.next
                temp=temp.next
            else:
                j+=1
                temp=temp.next
        return result.next （rlist开头是0，要跳过）
                
法二：
遍历一遍：
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        x1=ListNode(0)
        x2=ListNode(0)
        x1.next=head
        x2.next=head
        res=x2
        for i in range(n):
            x1=x1.next
        while x1.next!=None:
            x1=x1.next
            x2=x2.next
        temp=x2.next
        x2.next=temp.next
        return res.next
思想：
遍历一次链表，让x1先向前走n步，然后x2开始前进，x1与x2之间永远相差n，当x1走到最后的时候，x2就指向倒数第n个数字，让x2.next=x2.next.next即可。
注意：
要先给x1一个哑节点，然后再连接head，以防出现head只有一个，x1没有next的问题。这样无论如何，x1都有大于等于2个元素，永远保证x1有next。（x2同理）