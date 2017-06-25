## 题目 ##

有一个单链表，请设计一个算法，使得每K个节点之间逆序，如果最后不够K个节点一组，则不调整最后几个节点。例如链表1->2->3->4->5->6->7->8->null，K=3这个例子。调整后为，3->2->1->6->5->4->7->8->null。因为K==3，所以每三个节点之间逆序，但其中的7，8不调整，因为只有两个节点不够一组。

给定一个单链表的头指针head,同时给定K值，返回逆序后的链表的头指针。

## 我的解法 ##

采用一个辅助栈来实现逆序的操作。

```java
import java.util.*;

/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class KInverse {
    public ListNode inverse(ListNode head, int k) {
        // write code here
        ArrayDeque<ListNode> stack=new ArrayDeque<ListNode>();
        ListNode lastEnd=null,cur,resHead=null;
        cur=head;
        while(cur!=null){
            if(stack.size()!=k){
                stack.push(cur);
                if(stack.size()==k){
                    if(lastEnd!=null){
                        lastEnd.next=cur;
                    }else{
                        resHead=cur;
                    }
                }
                cur=cur.next;
                if(cur!=null){
                   continue;
                }

            }
            if(cur!=null||stack.size()==k){
                while(!stack.isEmpty()){
                //最后一个元素保存到lastEnd
                	if(stack.size()==1){
                    	lastEnd=stack.peek();
                	}
                	stack.pop().next=stack.peek();
            	}
            }else if(cur==null&&stack.size()!=k){
                while(!stack.isEmpty()){
                	if(stack.size()==1){
                    	lastEnd.next=stack.peek();
                	}
                	stack.pop();
            	}
            }

        }
        return resHead;
    }
}
```


