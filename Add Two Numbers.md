# problem
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

# solution
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
/**
 * 首先初始化一个哑节点:{val:0,next:null}
 * 递归链表中需要用到的变量:l1.val,l2.val,carry(进位)
 * 最后返回哑节点的next
 */
var addTwoNumbers = function(l1, l2) {
    let curr = result = new ListNode(0)
    //初始的进位为0
    let carry = 0
    while(l1||l2||carry){
        let sum = 0
        if(l1){
            sum += l1.val
            l1=l1.next
        }
        if(l2){
            sum += l2.val
            l2=l2.next
        }
        if(carry>0){
            sum+=carry
        }
        curr.next = new ListNode(sum % 10)
        curr = curr.next
        carry = (sum > 9)? 1 : 0
    }
    return result.next
};
```

# complexity
time complexity: O(max(m,n))

space complexity: O(max(m,n))
