- is a LIFO data structure
- can be implemented using physical data structures (arrays or linked list)
# Queue ADT
has data 
1. space for elements.
2. pointer for first element for delettion
3. pointer for last element for insertion
4. if using array, we need a "size element" because array needs to be of fixed size
has operations
1. enqueue()
2. dequeue()
3. isEmpty()
4. isFull()
5. first()
6. last()

## Queue implementation using array physical DT
### 1. using one pointer
using a rear pointer to point to last element , but dequeuing requires moving all the elements of the array one step back, so adding an element takes O(1) but deleting an element takes O(n)
### 2. using two pointers
 using two pointers
 one for rear index
 one for front index: two cases (caries first element index or first element index -1)
 - if(front carries first element index)-> then condition for empty queue becomes that front index must be larger than rear index because if they equal this means queue has one element
 - if(front carries first element index -1 ) -> then condition for empty queue is if( front == rear)
 adding an element has order O(1)
 deleting an element has order O(1)

Drawbacks of using array based queue:
1. the queue size cannot increase or decrease
2. the queue elements can not be reused.

this is why we have two solutions:
#### 1. resetting pointers
if at any stage, the queue is empty then, reset the front and rear pointers to the start position
#### 2. circular queue
if queue has space in front position we move the rear back to front we can implement a circular queue
- we can make use of the modulus operation when comparing positions of front and rear regardless if rear is after or before front pointer
#### Code for Array Queue 
```
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <assert.h>

typedef struct queue{
    int *q;
    int front;
    int rear;
    int size;
}queue;

void createQ(queue **q, int _size){
    *q = (queue*)malloc(sizeof(queue));
    assert(*q);
    (*q)->front = 0;
    (*q)->rear = 0;
    (*q)->size = _size;
    (*q)->q = (int*)malloc(_size * sizeof(int));
}

bool isFull(queue *q){
    if((q->rear+1)%q->size == q->front%q->size)
        return true;
    return false;
}

bool isEmpty(queue *q){
    if((q->rear)%q->size == q->front%q->size)
        return true;
    return false;
}

void enqueue(queue *q, int data){
    if(isFull(q)){
        printf("can not enqueue cause full\n");
    }
    else{
        q->rear = q->rear + 1;
        q->q[(q->rear)] = data;
    }
}

int dequeue(queue *q){
    int ret = -1;
    if(isEmpty(q)){
        printf("can not dequeue cause empty\n");
    }
    else{
        ret = q->q[1 + q->front++];
    }
    return ret;
}

int main(){
    queue *qu;
    createQ(&qu, 3);
    enqueue(qu, 1);
    enqueue(qu, 2);
    enqueue(qu, 3);
    enqueue(qu, 4);
    enqueue(qu, 5);
    return 0;
}
```

## DEQueue (Double Ended Queue)
| Normal Queue | Insert | Delete |     | DEQueue | Insert | Delete |
| ------------ | ------ | ------ | --- | ------- | ------ | ------ |
| Front        | no     | yes    |     | Front   | yes    | yes    |
| Rear         | yes    | no     |     | Rear    | yes    | yes    |

Restricted Double ended queues (Input Restricted or Output Restricted)

| I/P Restricted Queue | Insert | Delete |     | O/P Restricted Queue | Insert | Delete |
| -------------------- | ------ | ------ | --- | -------------------- | ------ | ------ |
| Front                | yes    | yes    |     | Front                | yes    | yes    |
| Rear                 | no     | yes    |     | Rear                 | yes    | no     |
### Code for DEQueue
```
/**
 * @file dequeue.c
 * @author Mina
 * @brief Double ended queue iplementation using circular array
 * @version 0.1
 * @date 2024-06-08
 *
 * @copyright Copyright (c) 2024
 *
 */

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <assert.h>

/**
 * @brief dqueue struct
 * @param q is pointer to array
 * @param front points to the index before the first element
 * @param rear points to the index of the last element
 * @param size indicated the size of the array ( = actual size + empty index for front)
 */
typedef struct dqueue{
    int *q;
    int front;
    int rear;
    int size;
}dqueue;

void createQ(dqueue **q, int _size){
    *q = (dqueue*)malloc(sizeof(dqueue));
    assert(*q);
    (*q)->front = 0;
    (*q)->rear = 0;
    (*q)->size = _size;
    (*q)->q = (int*)malloc(_size * sizeof(int));
}

/**
 * @brief returns true if front precedes the rear pointer by one index only
 */
bool isFull(dqueue *q){
    if(((q->rear+1)%q->size) == q->front)
        return true;
    return false;
}

/**
 * @brief returns true if front and rear pointers on same index
 */
bool isEmpty(dqueue *q){
    if((q->rear) == q->front)
        return true;
    return false;
}

void enqueueFront(dqueue *q, int data){
    if(isFull(q)){
        printf("OVERFLOW !!\n");
    }
    else{
        q->q[q->front] = data;
        q->front = (q->front-1+q->size)%q->size;
    }
}

void enqueueRear(dqueue *q, int data){
    if(isFull(q)){
        printf("OVERFLOW !!\n");
    }
    else{
        q->rear = (q->rear+1)%q->size;
        q->q[q->rear] = data;
    }
}

int dequeueFront(dqueue *q){
    int ret = -1;
    if(isEmpty(q)){
        printf("UNDERFLOW !!\n");
    }
    else{
        q->front = (q->front+1)%q->size;
        ret = q->q[q->front];
    }
    return ret;
}

int dequeueRear(dqueue *q){
    int ret = -1;
    if(isEmpty(q)){
        printf("UNDERFLOW !!\n");
    }
    else{
        ret = q->q[q->rear];
        q->rear = (q->rear-1+q->size)%q->size;
    }
    return ret;
}

void display(dqueue *q){
    if(isEmpty(q)){
        printf("Empty Double Ended Queue !!\n");
    }
    else{
        int tmp = (q->front+1)%q->size;
        while(tmp != q->rear){
            printf("%d\t", q->q[tmp]);
            tmp++;
            if(tmp == q->size){
                tmp = 0;
            }
        }
        printf("%d\t", q->q[tmp]);
    }
    return;
}

int main(){
    dqueue *qu;
    createQ(&qu, 5);
    enqueueFront(qu, 1);
    enqueueRear(qu, 2);
    enqueueFront(qu, 3);
    enqueueRear(qu, 4);
    enqueueFront(qu, 5);
    enqueueRear(qu, 6);
    display(qu);
    puts("++++++++++++++++++++");
    printf("%d\n", dequeueRear(qu));
    printf("%d\n", dequeueFront(qu));
    printf("%d\n", dequeueRear(qu));
    printf("%d\n", dequeueFront(qu));
    printf("%d\n", dequeueRear(qu));
    display(qu);
    puts("++++++++++++++++++++");
    return 0;
}
```

## Priority Queue
Priority queue can be implemented using two ways
- Limited number of priorities
- Element priority
### 1. Limited Set of Priorities
- as in operating systems, there will be multiple queues, each with its own priority, element id high priority go to high priority queue, mid to mid , low to low and so on
- but when executing from queue, you must execute from the highest available priority first, then comes mid after and so on...
- Element each have a priority assigned to it as in the example 

| A   | B   | C   | D   | E   | F   | G   |
| --- | --- | --- | --- | --- | --- | --- |
| 1   | 2   | 1   | 3   | 2   | 1   | 3   |

2 Ways of Implementing priority queue
	1. Insert in same order and delete max priority by searching it
	2. Insert in increasing order and of priority and delete last element of array 
### Way 1 : Insert in same order and delete max by search
ex:

| 1   | 5   | 7   | 9   | 2   | 6   |
| --- | --- | --- | --- | --- | --- |
this way insert takes O(1) and deletion is done by searching for highest priority and then deleting this element and shifting all remaining element in the queue to refill deleted element  O(2n) = O(n) 
#### Way 2 : Inserting in increasing order and delete last element of queue
or you can insert in sorted order

| 1   | 2   | 3   | 4   | 5   | 8   |
| --- | --- | --- | --- | --- | --- |
In this insertion is done by putting each priority in its place and shifting all elements to accommodate the newest priority. so Insertion takes O(n)
but deletion is done only from one side (high priority side) so deletion takes time order of O(1)
## Implementing Queue using two stacks
- by having two stack you enqueue elements in the first stack
- when dequeuing, pop the elements from the first stack and push into the second stack
- dequeue the element (pop from second stack)
- keep pushing elements into first stack
- keep popping elements from second stack
- when second stack  is empty, pop from first stack and push into second stack and so on ...