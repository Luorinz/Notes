# Reverse linked list
1. corner case
```
dummy->1->null
dummy->null
```
> just return
2. general case
```
dummy-> 1 ->   2      -> 3 -> null
pre    cur  nextNode

dummy ->  2   -> 1 -> 3 -> null
pre     nextNode cur  

dummy ->  2   -> 1 ->   3   -> null
pre             cur  nextNode

dummy ->  3   -> 2 ->   1   -> null
pre                    cur      nextNode
```
____
  1. link cur to the next node `cur.next = nextNode.next`
  2. link nextNode to the head of the reversed part `nextNode.next = pre.next`
  3. link pre to the nextNode `pre.next = nextNode`
  4. update nextNode to next `nextNode = cur.next`
  5. when nextNode gets to the end, exit
___
> cur represents the tail, and pre represents the the dummy, nextNode represents the node waiting to be added to the head of the list.
  
