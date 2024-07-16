# step1
ノードに着目するポインタを複数用意して、それらを入れ替えればいいと思ったが、完成させられなかった  
そのコードは残すのを忘れていた  
swap を使うのを思いつかなかった   
```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
       // ガード句
       if(!list1) {
        return list2;
       }
       if(!list2){
        return list1;
       }
       if(list1->val > list2->val) {
        swap(list1, list2);
       }

       ListNode* head = list1;

       while(list1 && list2) {
            ListNode* temp_tail;
            while(list1 && list1->val <= list2->val) {
                temp_tail = list1;
                list1 = list1->next;
            }
            temp_tail->next = list2;
            swap(list1, list2);
       }
       return head;
    }
};
```

# step2
dummy node を使うやり方  
参照  
https://www.youtube.com/watch?v=GfRQvf7MB3k&ab_channel=BackToBackSWE  
https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/  
https://www.geeksforgeeks.org/merge-two-sorted-lists-place/  
https://github.com/colorbox/leetcode/pull/5  
https://github.com/NobukiFukui/Grind75-ProgrammingTraining/pull/8  
https://github.com/Kitaken0107/GrindEasy/pull/6  
```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode dummy_head(0); 
        ListNode* tail = &dummy_head;

        while (list1 && list2) {
            if (list1->val < list2->val) {
                tail->next = list1;
                list1 = list1->next;
            } else {
                tail->next = list2;
                list2 = list2->next;
            }
            tail = tail->next; 
        }

        // list1またはlist2の残りの要素を添付
        if (list1) {
            tail->next = list1;
        } else if (list2) {
            tail->next = list2;
        }

        return dummy_head.next; 
    }
};
```

# step2-2
自分が最初に考えた iterative アプローチを step1 のコードを使って無理やり実装した  
実用性がないと思う  
```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
       // 必要ならガード節、その後のwhile次第
       if(!list1) {
        return list2;
       }
       if(!list2) {
        return list1;
       }
       if(list1->val > list2->val) {
        swap(list1, list2);
       }
       ListNode* head = list1;

       while(list1 && list2) {
            ListNode* temp_tail = list1;
            while(list1 && list1->val <= list2->val) {
                temp_tail = list1;
                list1 = list1->next;
            }
            temp_tail->next = list2;
            list2 = list2->next;
            temp_tail = temp_tail->next;
            if(!list1) {
                list1 = temp_tail;
                break;
            } else {
                temp_tail->next = list1;
                list1 = temp_tail;
            }
       }
       if(list2) {
        list1->next = list2;
       }

       return head;
    }
};
```

# step3
```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
       ListNode dummy_node(0);  
       ListNode* tail = &dummy_node;

       while(list1 && list2) {
            if(list1->val < list2->val) {
                tail->next = list1;
                list1 = list1->next;
            } else {
                tail->next = list2;
                list2 = list2->next;
            }
            tail = tail->next;
       }
       if(list1) {
        tail->next = list1;
       }
       if(list2) {
        tail->next = list2;
       }
       return dummy_node.next;
    }
};
```
