# 2022.11.30

## 剑指 Offer 09. 用两个栈实现队列

简单

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )

**示例 1：**

```
输入：
["CQueue","appendTail","deleteHead","deleteHead","deleteHead"]
[[],[3],[],[],[]]
输出：[null,null,3,-1,-1]
```

**示例 2：**

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

```java
class CQueue {
  LinkedList<Integer> A, B;
    public CQueue() {
        A = new LinkedList<Integer>();
        B = new LinkedList<Integer>();
    }
    
    public void appendTail(int value) {
        A.push(value);

    }
    
    public int deleteHead() {
     if (B.isEmpty()) {
            while (!A.isEmpty()) {
                B.push(A.pop());
            }
        } 
        if (B.isEmpty()) {
            return -1;
        } else {
            int deleteItem = B.pop();
            return deleteItem;
        }
    }
}
```

java写算法确实挺好做的

**CQUeue()**是创建了2个**栈**,**appendTail()**是**队列尾部插入整数**,所以直接**A.push()**,

删除头部的话,有2种情况。

根据**栈**后进先出的思想,将**A**的东西传到**B**中,实现了反转功能.

然后**第一种情况:**如果**B**里面为空、

那么返回-1

**第二种情况:**如果**B**里面不为空

返回**B弹出的东西**



## 剑指 Offer 30. 包含min函数的栈

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

**示例:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

```java
class MinStack {

​     LinkedList<Integer> A, B;

  /** initialize your data structure here. */

  public MinStack() {

​    A = new LinkedList<Integer>();

​    B = new LinkedList<Integer>();

  }

  public void push(int x) {

​    A.push(x);

​    if(B.isEmpty()){

​      B.push(x);

​    }

​    else{

​      if(B.peek()>=x){

​        B.push(x);

​      }

​    }

  }

  

  public void pop() {

​    if(A.pop().equals(B.peek())){

​      B.pop();

​    }

  }

  

  public int top() {

​    return A.peek();

  }

  

  public int min() {

​    return B.peek();

  }

}
```

唯一一个要注意的就是

**A.peek()**显示的是**A的栈顶元素**

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