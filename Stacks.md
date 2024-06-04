- Stacks are LIFO structures
- stacks can be used to reverse directions (an array for an example)
- stacks can be used in conversion from recursion to iteration (recursion automatically uses stack frame)
## ADT Stack 
Data:
1. space for element
2. top pointer
Operation:
1. push()
2. pop()
3. peek()
4. stackTop()
5. isEmpty()
6. isFull()

### Note:
time complexity for push and pop is O(1).
when creating stack using linked list you need to insert and delete at head position because this is where O(1) is for pushing and popping
### Note:
when using array based stack, the size is determined at start (whether you allocate array in stack or heap is irrelevant)
however when using list based stack , the size of stack is unlimited.
so when do we say that stack is full ? when heap is full and we fail to create another node.