# Stacks description
 Stacks are LIFO structures
- stacks can be used to reverse directions (an array for an example)
- stacks can be used in conversion from recursion to iteration (recursion automatically uses stack frame)
### ADT Stack Elements:
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

## Code for stack using array
```

```
## Code for stack using list
NOTICE: is full function can be applied by trying to create a node and delete it, if it can be created then heap is not full or you can just ignore implementing the full checking function
```
#include <stdio.h>
#include <stdlib.h>
#include <assert.h>
#include <stdbool.h>
#include <string.h>

typedef struct Node{
    char data;
    struct Node *next;
}Node;

typedef struct Stack{
    Node *top;

}Stack;

void pushinStack(Stack *st , char _data){
    Node *ptr = (Node*)malloc(sizeof(Node));
    assert(ptr);
    ptr->data = _data;
    if(st->top == NULL){
        st->top = ptr;
        st->top->next = NULL;
    }
    else{
        ptr->next = st->top;
        st->top = ptr;
    }
    return;
}

char popfromStack(Stack *st){
    char ret = -1;
    if(!(st->top)){
        printf("empty stack\n");
    }
    else{
        Node *ptr = st->top;
        assert(ptr);
        st->top = st->top->next;
        ret = ptr->data;
        free(ptr);
    }
    return ret;
}

char topofStack(Stack *st){
    char ret = -1;
    if(!(st->top)){
        printf("empty stack\n");
    }
    else{
        ret = st->top->data;
    }
    return ret; 
}

void displayStack(Stack *st){
    Node *tmp = st->top;
    while(tmp){
        printf("%c\t",tmp->data);
        tmp = tmp->next;
    }
    return;
}

bool isStackEmpty(Stack *st){
    if(st->top){
        return false;
    }
    return true;
}

```
# One Application of stacks is solving math operations

equations can be written using 
1. infix format (a + b)
2. pre-fix format (+ a b)
3. post-fix format (a b +)
post-fix format is used to solve math equations in one go
### notice that to solve mathematical equations, the compiler implicitly parenthesis everything and turns it into postfix format

$a + b * c = abc*+$

| symbol  | precedence | Associativity |
| ------- | ---------- | ------------- |
| + -     | 1          | L->R          |
| * /     | 2          | L->R          |
| ^       | 3          | R->L          |
| - ! log | 4          | R->L          |
| ( )     | 5          | L->R          |
unary operators like negative , ! , log -> ex   $-a = a-$ ,  $log a = a  log$ , $a! = a!$

## Method one of solving using stack

you make a stack table and a postfix expression
- put any variable expression $a , b , c$ you meet in the postfix expression , while normally pushing any operation in the stack
- if the stack has an operator of same or higher precedence that operator to push, pop that operator and add to expression, else push to stack

example $a * b + c -d/e$ --> $a b c * + d e / -$


## Method two of solving using stack
same as previous method but variables are also added to the stack and they have the highest precedence among all operators

## Solving equation with brackets
brackets solving is a little different because you need to prioritize them,
so we use a different precedence and associativity table than the last one.

| symbol | precedence out of stack | precedence inside of stack |
| ------ | ----------------------- | -------------------------- |
| + -    | 1                       | 2                          |
| * /    | 3                       | 4                          |
| ^      | 6                       | 5                          |
| (      | 7                       | 0                          |
| )      | 0                       | N/A                        |
the reason for different precedence is
1. we transformed associativity into precedence
	- if L->R, then in stack would be higher so that you cant push the same operator twice
	- if R->L, then in stack would be lower so you can push same operator again and again.
2. we have a special scenario when we find a closing bracket.

so if we find an opening bracket we push it into the stack, but if we find a closing bracket (of lower precedence than everything) we pop out until we meet an opening bracket then we break the popping operations and continue.

## Evaluating post-fix expressions
we evaluate post-fix expressions by evaluating each element in the expression with the help of a stack
- if it is an operand we push it in the stack
- if it is operator, we pop out two operands and then evaluate them with operator and then push result in the stack
- after finishing expression, the result will be the final element in the stack.
notice that here we will need to use an integer stack while before we needed to user a char stack
notice that to convert from  a char to an integer for the operands , you can just minus '0' asci code for zero
### Code for calculator
```
#include <iostream>
#include <stack>
#include <cmath>

#define INSTACK 0
#define OUTSTACK 1

using namespace std;

bool isOperand(char a) {
    if (a == '+' || a == '-' || a == '*' || a == '/' || a == '^' || a == '(' || a == ')')
        return false;
    else
        return true;
}

int getPrecedence(char a, char stackStatus) {
    if (stackStatus == OUTSTACK) {
        switch (a) {
            case '+':
            case '-':
                return 1;
            case '*':
            case '/':
                return 3;
            case '^':
                return 6;
            case '(':
                return 7;
            case ')':
                return 0;
            default:
                return -1;
        }
    } else {
        switch (a) {
            case '+':
            case '-':
                return 2;
            case '*':
            case '/':
                return 4;
            case '^':
                return 5;
            case '(':
                return 0;
            case ')':
                return -1;
            default:
                return -1;
        }
    }
}

string infixToPrefix(string eq) {
    stack<char> st;
    string result;

    int i = 0;
    while (eq[i] != '\0') {
        if (isOperand(eq[i])) {
            result += eq[i++];
        } else {
            if (st.empty() || getPrecedence(st.top(), INSTACK) < getPrecedence(eq[i], OUTSTACK)) {
                st.push(eq[i++]);
            } else if (getPrecedence(eq[i], OUTSTACK) == 0) {
                while (getPrecedence(st.top(), INSTACK) != 0) {
                    result += st.top();
                    st.pop();
                }
                st.pop();
                i++;
            } else {
                result += st.top();
                st.pop();
            }
        }
    }
    while (!st.empty()) {
        result += st.top();
        st.pop();
    }
    return result;
}

int calculate(string postfix) {
    stack<int> st;
    int i = 0;
    while (postfix[i] != '\0') {
        if (isOperand(postfix[i])) {
            st.push(postfix[i++] - '0');
        } else {
            int operandTwo = st.top();
            st.pop();
            int operandOne = st.top();
            st.pop();
            int result = 0;
            switch (postfix[i++]) {
                case '+':
                    result = operandOne + operandTwo;
                    break;
                case '-':
                    result = operandOne - operandTwo;
                    break;
                case '*':
                    result = operandOne * operandTwo;
                    break;
                case '/':
                    result = operandOne / operandTwo;
                    break;
                case '^':
                    result = (int)pow(operandOne, operandTwo);
                    break;
                default:
                    break;
            }
            st.push(result);
        }
    }
    int result = st.top();
    st.pop();
    return result;
}

int main() {
    stack<char> st;
    string eq{"1+2*3"};

    cout << infixToPrefix(eq) << endl;
    // string infix = infixToPrefix(eq);
    string infix = "823^/23*+51*-";
    cout << calculate(infix) << endl;
    return 0;
}
```
