# What is BST?
a binary search tree is a tree where all elements are put in sorted order
- a BST has no duplicate elements
- elements are in ascending order when a BST is traversed in order
- with a number of nodes , Catalan number of BSTs can be formed
- BST is mostly done using list representation, but can be done with array too
``` mermaid
graph TD
30 --> 20
30 --> 40
20 --> 10
20 --> 25
40 --> 35
40 --> 45
```
### Code for searching in a BST using recursive function
```
============================RECURSIVE FUNCTIONS================================
Node* searchBST(Node *pNode , int key){
	if(pNode == NULL) return NULL;
	if(pNode->data == key) return pNode;
	else if(pNode->data > key)
		return searchBST(pNode->leftchild , key);
	else if(pNode->data < key)
			return searchBST(pNode->rightchild , key);
}
============================ITERATIVE FUNCTIONS================================
Node* searchBST(Node *pNode, int key){
	while(pNode != NULL){
		if(pNode->data == key)
			return pNode; 	
		else if(pNode->data > key)
			pNode = pNode->leftchild;
		else
			pNode = pNode->rightchild;
	}
	return NULL;
}
```

## Creation for binary search tree
- creation of BST is very easy , you navigate and create a node at the same time
- step 1: navigate to the place where the node should be inserted
- step 2: create a node and put key value in it
- step 3: link created node to the tree
#### Code for recursive insert in BST
```
Node *insertBST(Node* ptr , int key){
    if(ptr == NULL){
        ptr = (Node*)malloc(sizeof(Node));
        ptr->data = key;
        ptr->left = NULL;
        ptr->right = NULL;
        return ptr;
    }
    else if(ptr->data == key){
        return ptr;
    }
    else if(ptr->data > key){
        ptr->left = insertBST(ptr->left , key);
    }
    else{
        ptr->right = insertBST(ptr->right , key);
    }
    return ptr;
}
```
#### Code for iterative insert in BST
```
void insertIterativeBST(Node *ptr , int key){
    Node *tmp= NULL;
    Node *trail = NULL;
    while(ptr != NULL){
        trail = ptr;
        if(ptr->data == key){
            return;
        }
        else if(key < ptr->data){
            ptr = ptr->left;
        }
        else{
            ptr = ptr->right;
        }
    }
    tmp = (Node*)malloc(sizeof(Node));
    assert(tmp);
    tmp->data = key;
    tmp->left = NULL;
    tmp->right = NULL;
    if(key < trail->data){
        trail->left = tmp;
    }
    else{
        trail->right = tmp;
    }
}
```
#### Time complexity for creating a BST
is the time taken for adding all nodes, where each node needs to search for the location to be added to the tree
- time needed for search of location is log(n) {search through height of tree}
- time needed to add all n nodes
- TOTAL TIME  = O(n log(n)).
## Deletion from BST
cases:
- deleting leaf node
  -> search for node , if found then delete
- deleting node with one child
  -> search for node , assign its only child in its place and then delete node
-  <font color = "yellow">Notice that we are REPLACING nodes data as an act of deleting intermediate node , actual delete (FREE) happens only on lead nodes </font>
- deleting root node
  -> root node replacing can be very complex on many levels if replaced by any non-leaf node
	  -> this is why we replace it by its in order predecessor or in order successor because they are leaf nodes who won't disturb the rest of the tree
		  1. in order predecessor: right most node in the left subtree
		  2. in order successor: left most node in the right subtree
	if predecessor or successor are not leaf nodes then the process is repeated for them also.
### Generating a BST from preorder traversal
Unlike a normal binary tree, we can generate a BST without the need for two traversal because the BST has an extra characteristic which is sorted order

so how we can generate it ?
- we use the idea of stack
- imagine you have this traversal `30,20,10,15,25,40,45`
- first we create the root node 
- then we check if new element in array will go to left or right child
- if element < node
	- create node with element data and assign as left child and push parent to stack <font color = "yellow">because we still need to go back to make right child </font>
	- then make node = left child and check next array element
- if element > node but smaller than parent node at top of stack
	- then pop one node and assign new element as node in right child of node
	- <font color = "yellow">No need to push same node to stack again because left and right child have both been created </font>
	- then we make node = right child and check next element in the array
- if element > node and stack is empty
	- that means we are at the most right track of the tree
	- create node with data and assign as right child of node
	- make node as right child and check next element in the array

Generating a BST from post order traversal is the same as pre order traversal but we work array elements from end to start index and check that element are greater than node instead of smaller

### Code for binary search tree program
```
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <assert.h>

typedef struct Node{
    int data;
    struct Node *left;
    struct Node *right;
}Node;

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <assert.h>

#ifndef STACH_H__
#define STACK_H__

typedef struct NodeStack{
    Node* data;
    struct NodeStack *next;
}NodeStack;

typedef struct Stack{
    NodeStack *top;
}Stack;

Stack* createStack(void){
    Stack *st = (Stack*)malloc(sizeof(Stack));
    assert(st);
    st->top = NULL;
    return st;
}
bool isStackEmpty(Stack *pStack){
    return (pStack->top == NULL);
}
void pushStack(Stack *pStack , Node* data){
        NodeStack *pNode = (NodeStack*)malloc(sizeof(NodeStack));
        assert(pNode);
        pNode->data = data;
        pNode->next = NULL;
    if(isStackEmpty(pStack)){
        pStack->top = pNode;
    }
    else{
        pNode->next = pStack->top;
        pStack->top = pNode;
    }
    return;
}
Node* popStack(Stack *pStack){
    NodeStack *pNode = NULL;
    Node* ret;
    if(isStackEmpty(pStack)){
        puts("STACK UNDERFLOW !!");
        return 0;
    }
    else{
        pNode = pStack->top;
        pStack->top = pStack->top->next;
        ret = pNode->data;
        free(pNode);
        return ret;
    }

}
Node* topStack(Stack *pStack){
    Node* ret;
    if(isStackEmpty(pStack)){
        puts("STACK UNDERFLOW !!");
        return 0;
    }
    else{
        ret = pStack->top->data;
        return ret;
    }

}
int countStack(Stack *pStack){
    int ret = 0;
    NodeStack *pNode = pStack->top;
    if(isStackEmpty(pStack)){
        return ret;
    }
    else{
        while(pNode!= NULL){
            ret++;
            pNode = pNode->next;
        }
        return ret;
    }
}

#endif

/**
 * @brief   Insert a node in a subtree with loop recursive fashion
 * @note    This function can be used to create a root node
 */
Node *insertRecursiveBST(Node* ptr , int key){
    if(ptr == NULL){
        ptr = (Node*)malloc(sizeof(Node));
        ptr->data = key;
        ptr->left = NULL;
        ptr->right = NULL;
        return ptr;
    }
    else if(ptr->data == key){
        return ptr;
    }
    else if(ptr->data > key){
        ptr->left = insertRecursiveBST(ptr->left , key);
    }
    else{
        ptr->right = insertRecursiveBST(ptr->right , key);
    }
    return ptr;
}
/**
 * @brief   Insert a node in a subtree with loop iterative fashion
 * @note    This function can't be used to create a root node
 */
void insertIterativeBST(Node *ptr , int key){
    Node *tmp= NULL;
    Node *trail = NULL;
    while(ptr != NULL){
        trail = ptr;
        if(ptr->data == key){
            return;
        }
        else if(key < ptr->data){
            ptr = ptr->left;
        }
        else{
            ptr = ptr->right;
        }
    }
    tmp = (Node*)malloc(sizeof(Node));
    assert(tmp);
    tmp->data = key;
    tmp->left = NULL;
    tmp->right = NULL;
    if(key < trail->data){
        trail->left = tmp;
    }
    else{
        trail->right = tmp;
    }
}
/**
 * @brief   displays tree in in order fashion
 */
void inorder(Node* pNode){
    if(pNode){
        inorder(pNode->left);
        printf("%d\t" , pNode->data);
        inorder(pNode->right);
    }
}
/**
 * @brief   returns height of a tree
 */
int heightTree(Node* pNode){
    int x = 0 , y = 0;
    if(pNode == NULL){
        return -1;
    }
    if(pNode->left == NULL && NULL == pNode->right){
        return 0;
    }
    x = heightTree(pNode->left);
    y = heightTree(pNode->right);
    return (x>y? x+1 : y+1);
}
/**
 * @brief   pinpoints the in order traverser Predecessor.
 */
Node* inorderPredecessor(Node* pNode){
    if(NULL == pNode->left || NULL == pNode)
        return pNode;
    pNode = pNode->left;
    while(pNode->right)
        pNode = pNode->right;
    return pNode;
}
/**
 * @brief   pinpoints the in order traverser successor.
 */
Node* inorderSuccessor(Node* pNode){
    if(NULL == pNode->right|| NULL == pNode)
        return pNode;
    pNode = pNode->right;
    while(pNode->left)
        pNode = pNode->left;
    return pNode;
}
/**
 * @brief   deletes a node from binary search tree and frees its node
 * 
 * @param pNode pointer to root node of certain subtree to search
 * @param key   integer to search up
 * @param root  address of root node in case it's needed to delete
 * @return      Node* pNode pointer to same certain subtree after tree changes
 */
Node* deleteNode(Node* pNode , int key, Node** root){
    Node *tmp = NULL;

    if(pNode == NULL)   
        return NULL;
    if(key == pNode->data && pNode->left == NULL && pNode->right == NULL){
        if(key == (*root)->data){
            *root = NULL;
        }
        free(pNode);
        return NULL;
    }

    if(key < pNode->data){
        pNode->left = deleteNode(pNode->left , key , root);
    }
    else if(key > pNode->data){
        pNode->right = deleteNode(pNode->right , key , root);
    }
    else{
        if(heightTree(pNode->left) > heightTree(pNode->right)){
            tmp = inorderPredecessor(pNode);
            pNode->data = tmp->data;
            pNode->left = deleteNode(pNode->left, tmp->data , root);
        }
        else{
            tmp = inorderSuccessor(pNode);
            pNode->data = tmp->data;
            pNode->right = deleteNode(pNode->right, tmp->data , root);
        }
    }
    return pNode;
}
/**
 * @brief Create a binary search tree from preorder traversal
 */
Node* createFromPreOrder(int arr[] , int len){
    Stack *st = createStack();
    int i = 0;
    Node *tmp = NULL;
    Node *root = NULL;
    /*  create root node    */
    Node* pNode = (Node*)malloc(sizeof(Node));
    assert(pNode);
    pNode->data = arr[i++];
    pNode->left = NULL;
    pNode->right = NULL;
    root = pNode;
    /*   create rest of binary search tree   */
    while(i < len){
        /* if element is smaller -> make as left child of current node  */
        if(arr[i] < pNode->data){
            tmp = (Node*)malloc(sizeof(Node));
            assert(tmp);
            tmp->data = arr[i++];
            tmp->left = NULL;
            tmp->right = NULL;
            pNode->left = tmp;
            /*  push current node into stack, for popping when time for right child */
            pushStack(st , pNode);
            pNode = tmp;
        }
        /*  if element is larger than pNode but still smaller than parent node -> assign as right child but no push to stack */
        else if(arr[i] > pNode->data && !isStackEmpty(st) && arr[i] < (topStack(st)->data) ){
            tmp = (Node*)malloc(sizeof(Node));
            assert(tmp);
            tmp->data = arr[i++];
            tmp->left = NULL;
            tmp->right = NULL;
            /*  assign pNode as right child but no need to push to stack because else we are going two steps back not only one */
            pNode->right = tmp;
            pNode = tmp;
        }
        /*  if element is larger than pNode and larger than element in stack and stack is not empty
        then go step back (pop) to recheck with new pNode */
        else if(arr[i] > pNode->data && (!isStackEmpty(st)) && arr[i] > (topStack(st)->data) ){
            pNode = popStack(st);
        }
        /*  else means element is larger than pNode and larger than element in stack and stack is  empty
        so this means that is the largest element yet so it is to be pushed to right most way*/
        else{
            tmp = (Node*)malloc(sizeof(Node));
            assert(tmp);
            tmp->data = arr[i++];
            tmp->left = NULL;
            tmp->right = NULL;
            /*  assign pNode as right child but no need to push to stack because we never need to back to a node
            that has its left and right child filled already */
            pNode->right = tmp;
            pNode = tmp;
        }
    }
    return root;
}
/**
 * @brief Create a binary search tree from postorder traversal
 */
Node* createFromPostOrder(int arr[] , int len){
    int i = len-1;
    Stack *st = createStack();
    Node *tmp = NULL;
    Node *root = NULL;
    /* create root node and assign its data as arr[0] */
    Node *pNode = (Node*)malloc(sizeof(Node));
    assert(pNode);
    pNode->data = arr[i--];
    pNode->left = NULL;
    pNode->right = NULL;
    root = pNode;

    while(i >= 0){
        /*  if element is larger in postorder traversal then it's right child */
        if(arr[i] > pNode->data){
            tmp = (Node*)malloc(sizeof(Node));
            assert(tmp);
            tmp->data = arr[i--];
            tmp->left = NULL;
            tmp->right = NULL;
            /* assign tmp as pNode right child as push pNode into stack (to pop and make left child) and then assign pNode as tmp */
            pNode->right = tmp;
            pushStack(st, pNode);
            pNode = tmp;
        }
        /*  if element is smaller than pNode but still larger than parent node then assign as left child 
            but no need to push into stack because left child of this node ha already been created  */
        else if(arr[i] < pNode->data && !isStackEmpty(st) && arr[i] > topStack(st)->data){
            tmp = (Node*)malloc(sizeof(Node));
            assert(tmp);
            tmp->data = arr[i--];
            tmp->left = NULL;
            tmp->right = NULL;
            /* assign tmp as pNode right child and don't push pNode into stack */
            pNode->left = tmp;
            pNode = tmp;
        }
        /*  if element is smaller than both pNode and parent node then pop */
        else if(arr[i] < pNode->data && !isStackEmpty(st) && arr[i] < topStack(st)->data ){
            pNode = popStack(st);
        }
        /*  if element is smaller than pNode and stack is empty then assign as left child */
        else if(arr[i] < pNode->data && isStackEmpty(st)){
            tmp = (Node*)malloc(sizeof(Node));
            assert(tmp);
            tmp->data = arr[i--];
            tmp->left = NULL;
            tmp->right = NULL;
            /* assign tmp as pNode right child and don't push pNode into stack */
            pNode->left = tmp;
            pNode = tmp;
        }
    }
    return root;
}
/*  Main program code   */
int main(){
    Node *root = NULL;
    root = insertRecursiveBST(root , 25);
    insertIterativeBST(root , 20);
    insertIterativeBST(root , 30);
    insertIterativeBST(root , 40);
    insertIterativeBST(root , 10);
    puts("First in order display");
    puts("===================================");
    inorder(root);

    root = deleteNode(root , 20 , &root);
    puts("\n\nIn order display after deleting 20");
    puts("===================================");
    inorder(root);

    puts("creating a new BST from pre order traversal : ");
    int arr[] = {5,3,1,2,4,9,8,6,7};
    Node* newBST = createFromPreOrder(arr, 9);
    puts("\n\nIn order display for new pre Order generated BST");
    puts("===================================");
    inorder(newBST);
    puts("");

    puts("creating a new BST from post order traversal : ");
    int newarr[] = {1,4,3,2,6,7,9,8,5};
    Node* newNewBST = createFromPostOrder(newarr, 9);
    puts("\n\nIn order display for new post Order generated BST");
    puts("===================================");
    inorder(newNewBST);

    return 0;
}
```



### Drawbacks of binary search tree
the inability to control the user input for binary search tree makes the search time complexity ranges from 
- O(log(n)) to O(n)
- if user inputs elements as 1,2,3,4,5,6 then this takes O(n) because height is n
- but if user enters as 42,1,3,6,5 then this takes O(log(n))  because height is Log(n)