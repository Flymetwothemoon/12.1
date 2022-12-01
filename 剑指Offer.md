

# 2022.12.1

## 剑指 Offer 06. 从尾到头打印链表

简单

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

**限制：**

```
0 <= 链表长度 <= 10000
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
      LinkedList<ListNode>list =  new LinkedList<ListNode>();
      ListNode temp = head;
      int i = 0;
      while(temp!=null){
          list.push(temp);
          temp = temp.next;
          i++;
      }
      int a[] = new int[i];
      for(int j = 0;j<i;j++){
          a[j] = list.pop().val;
      }
      return a;
    }
}
```

记得,用**LinkedList**不要用**ArrayList**

## 剑指 Offer 24. 反转链表

简单

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

**限制：**

```
0 <= 节点个数 <= 5000
```

```java
class Solution {
    public ListNode reverseList(ListNode head) {
          ListNode prev = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        return prev;


    }
}
```

双指针





## 53.最大子数组和

中等

给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**子数组** 是数组中的一个连续部分。



**示例 1：**

```
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
```

**示例 2：**

```
输入：nums = [1]
输出：1
```

**示例 3：**

```
输入：nums = [5,4,-1,7,8]
输出：23
```

---

```java
class Solution {
    public int maxSubArray(int[] nums) {
       int dp[] = new int[nums.length];
       int max = nums[0];
       dp[0] = nums[0];
       for(int i =1;i<nums.length;i++){
           if(dp[i-1]>0){
               dp[i] = nums[i]+dp[i-1];
           }
           else{
               dp[i] = nums[i];
           }
       }
       for(int i = 0;i<nums.length;i++){
           max = max>dp[i]?max:dp[i];
       }
        return max;
    }
}
```

感觉是一种状态转移,感觉看代码就可以理解,但还是举一个例子吧



index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 ? ?  ?   ?  ?  ?  ?  ?



**index为1时**

index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 1 ?  ?   ?  ?  ?  ?  ?



**index 为2**

index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 1 -2 ?   ?  ?  ?  ?  ?



**index 为3**

index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 1 -2 2   ?  ?  ?  ?  ?



**index 为4**

index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 1 -2 2  1  ?  ?  ?  ?



**index 为5**

index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 1 -2 2  1  3  ?  ?  ?



**index 为6**

index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 1 -2 2  1  3  4  ?  ?



**index 为7**

index:0  1 2  3  4 5 6 7 8  

​          -2,1,-3,4,-1,2,1,-5,4

dp:     -2 1 -2 2  1  3  4  -1  ?



**index 为8**

index:0  1 2  3  4 5    6  7    8  

​          -2, 1,-3, 4, -1,2,1,-5,  4

dp:     -2 1 -2 2  1  3  4  -1  4

所以最大就是4
