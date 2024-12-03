AVL tree (named after inventors Adelson-Velsky and Landis) is a self balancing binary search tree

# An AVL tree properties
- a tree is called balance if its balance factor is less or equal to one
- Balance Factor = $| height (left subtree) - height (right subtree) | <= 1$
- Rotations are always done on three nodes only
- 

- Imbalance have types 
	1. LL imbalance 
	2. LR imbalance
	3. RL imbalance
	4. RR imbalance
``` mermaid
graph TD
30 --> 20
30 --> -
20 --> 10
20 --> +
1 --> !
1 --> 3
3 --> *
3 --> 5
200 --> 100
200 --> #
100 --> `
100 --> 150
2000 --> &
2000 --> 4000
4000 --> 3000
4000 --> a
```
# Rotations for Insertions
1. Initial state
``` mermaid
graph TD
30 --> 20
30 --> -
```
2. after inserting 10 is having imbalance of 2  and it is called LL imbalance so we make "LL rotation or CW or Right Rotation" 
``` mermaid
graph TD
30 --> 20
20 --> 10
30 --> -
20 --> +
```
3. Perform "LL" Rotation
``` mermaid
graph TD
20 --> 10
20 --> 30
```

- Imagine the rotations as pulling a string to change the nodes places and height
- notice that LR rotation consists of 
  1. RR rotation
  2. LL Rotation
  3. and vice versa (LL then RR for RL imbalance case)

### Possible optimizations for my AVL tree code
- height function is called recursively for every node -> excessive function calling which can be saved by having a height parameter inside struct node
- this will lead to bad timings in large systems due to excessive call stacks being created and destroyed excessively
- LR Rotation and RL rotation consist of RR and LL rotations, this can also be optimized by assigning the pointers correctly manually instead of dividing the process into two calls
### Deleting from AVL tree
- deleting from AVL is similar to deleting from BST in replacing nodes by their predecessor and their in order successor and so on 
- when deleting we want to keep tree balanced so we check balance and take corrective action but
- a new case of imbalance appears that never appears when inserting 
``` mermaid
graph TD
5 --> -
5 --> 10
10 --> 7
10 --> 15
```
this never happens normally because we will never have an opportunity to insert the 15 with the 7 making this imbalance so we need to add a case for this imbalance that is not needed in insert
### Analysis for AVL tree height and number of nodes
- max number of nodes  = $n^{h+1}-1$
- min number of nodes = look into table

| height | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| ------ | --- | --- | --- | --- | --- | --- | --- |
| nodes  | 1   | 2   | 4   | 7   | 12  | 20  | 33  |
if given height 
1. if height => 0, min. nodes = 0
2. if height => 1, min. nodes = 1
3. otherwise, height = height(n-1) + height(n-2) + 1 -->(similar to Fibonacci series)

if given number of nodes
1. min height = $log2({n+1})$
2. max height = look at the table
   for example for 19 nodes max. height = 5
### Code for AVL tree (Insert & delete with different rotations) 
```
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <assert.h>
#include <math.h>

#define LL_IMBALANCE 0
#define LR_IMBALANCE 1 
#define RL_IMBALANCE 2
#define RR_IMBALANCE 3
#define BALANCED     4

typedef struct Node{
    int data;
    struct Node* left;
    struct Node* right;
}Node;
/**
 * @brief recursive function to find height of a certain subtree 
 */
int heightAvl(Node* p){
    if(!p)  return -1;
    if(!p->left && !p->right)   return 0;
    return ( heightAvl(p->left) > heightAvl(p->right) ? heightAvl(p->left) +1 : heightAvl(p->right) +1 );
}
/**
 * @brief returns balance state of AVL tree 
 */
int balanceAvl(Node*p){
    if(!p)
        return BALANCED;
    int height_left = heightAvl(p->left);
    int height_right = heightAvl(p->right);
    int height_left_left = (p->left)? heightAvl(p->left->left) : -2 ;
    int height_left_right = (p->left)? heightAvl(p->left->right): -2 ;
    int height_right_right = (p->right)? heightAvl(p->right->right): -2 ;
    int height_right_left = (p->right)? heightAvl(p->right->left): -2 ;

    if(         abs(height_left - height_right)  <= 1)
        return BALANCED;
    if(         (height_left - height_right == 2) && ( height_left_left - height_left_right == 1 )  )
        return LL_IMBALANCE;
    else if(    (height_left - height_right == 2) && (height_left_right - height_left_left == 1 )  )
        return LR_IMBALANCE;
    else if(    (height_left - height_right == -2) && (height_right_right - height_right_left == 1 )  )
        return RR_IMBALANCE;
    else if(    (height_left - height_right == -2) && (height_right_left - height_right_right == 1 )  )
        return RL_IMBALANCE;
    else if ((height_left - height_right == -2) && (height_right_left - height_right_right == 0 ))
        return RR_IMBALANCE;
    else if ((height_left - height_right == 2) && (height_right_left - height_right_right == 0 ))
        return LL_IMBALANCE;    
    else
        puts("ERROR ELSE STATE UNDEFINED");
        printf("heightAvl(p->left) - heightAvl(p->right) = %d \n" , heightAvl(p->left) - heightAvl(p->right) );
        printf("balanceAvl(p->left) = %d \n" , balanceAvl(p->left) );
        printf("balanceAvl(p->right) = %d \n" , balanceAvl(p->right) );
        exit(EXIT_FAILURE);
}
/**
 * @brief rotation shifting action taken in case of Left left imbalance
 */
Node* LL_Rotate(Node* p){
    Node *right = p->left->right;
    Node *origin = p;
    p = p->left;
    p->right = origin;
    origin->left = right;
    return p;
}
/**
 * @brief rotation shifting action taken in case of right right imbalance
 */
Node* RR_Rotate(Node *p){
    Node *left = p->right->left;
    Node *origin = p;
    p = p->right;
    p->left = origin;
    origin->right = left;
    return p;
}
/**
 * @brief rotation shifting action taken in case of Left right imbalance
 */
Node* LR_Rotate(Node *p){
    p->left = RR_Rotate(p->left);
    p = LL_Rotate(p);
    return p;
}
/**
 * @brief rotation shifting action taken in case of right left imbalance
 */
Node* RL_Rotate(Node *p){
    p->right = LL_Rotate(p->right);
    p = RR_Rotate(p);
    return p;
}
/**
 * @brief insert node to the AVL tree
 */
Node* InsertAvlTree(Node* p , int data){
    /*  if NULL create and assign then return at end */
    if(NULL == p){
        Node* p = (Node*)malloc(sizeof(Node));
        p->data = data;
        p->left = NULL;
        p->right = NULL;
        return p;
    }
    else if(data < p->data){
        p->left = InsertAvlTree(p->left , data);
    }
    else if(data > p->data){
        p->right = InsertAvlTree(p->right , data);
    }
    else if(data == p->data){
        return p;
    }
    /*  accommodate for different imbalances */
    if(balanceAvl(p) == LL_IMBALANCE)
        p = LL_Rotate(p);
    else if(balanceAvl(p) == RR_IMBALANCE)
        p = RR_Rotate(p);
    else if(balanceAvl(p) == LR_IMBALANCE)
        p = LR_Rotate(p);
    else if(balanceAvl(p) == RL_IMBALANCE)
        p = RL_Rotate(p);
    return p;
}
/**
 * @brief display tree in order traversal
 */
void inorder(Node* p){
    if(!p)
        return;
    inorder(p->left);
    printf("%d\t" , p->data);
    inorder(p->right);
}

Node* inorderPredecessor(Node *p){
    if(!p || (!p->left && !p->right) )
        return NULL;
    p = p->left;
    while(p->right)
        p = p->right;
    return p;
}
Node* inorderSuccessor(Node *p){
    if(!p || (!p->left && !p->right) )
        return NULL;
    p = p->right;
    while(p->left)
        p = p->left;
    return p;
}
/**
 * @brief deletes a node from AVL tree, replaces node with successor \ predecessor , frees , ...
 */
Node* deleteNodeAvlTree(Node *p , int key){
    Node* tmp = NULL;
    if(!p)
        return NULL;
    if(key < p->data)
        p->left = deleteNodeAvlTree(p->left , key);
    else if(key > p->data)
        p->right = deleteNodeAvlTree(p->right , key);
    else {
        if(!p->left && !p->right){
            free(p);
            return NULL;
        }
        else{
            if(heightAvl(p->left) >= heightAvl(p->right)){
                tmp = inorderPredecessor(p);
                p->data = tmp->data;
                p->left = deleteNodeAvlTree(p->left , tmp->data);
            }
            else{
                tmp = inorderSuccessor(p);
                p->data = tmp->data;
                p->right = deleteNodeAvlTree(p->right , tmp->data);
            }
        }
    }
    /*  accommodate for different imbalances */
    int balance = balanceAvl(p);
    if(balance == LL_IMBALANCE)
        p = LL_Rotate(p);
    else if(balance == RR_IMBALANCE)
        p = RR_Rotate(p);
    else if(balance == LR_IMBALANCE)
        p = LR_Rotate(p);
    else if(balance == RL_IMBALANCE)
        p = RL_Rotate(p);
    return p;
}
/**
 * @brief program start
 */
int main(){
    Node *n = NULL;
    n = InsertAvlTree(n , 20);
    n = InsertAvlTree(n , 17);
    n = InsertAvlTree(n , 50);
    n = InsertAvlTree(n , 18);
    n = InsertAvlTree(n , 10);
    
    

    printf("height of tree is %d\n" , heightAvl(n));
    inorder(n); puts(" ");

    n = deleteNodeAvlTree(n, 50);
    printf("height of tree is %d\n" , heightAvl(n));
    inorder(n); puts(" ");

    return 0;
}
```