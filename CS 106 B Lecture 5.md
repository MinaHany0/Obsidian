this lecture covered 
1.  idea of templates in C++ for data types such as vector , Linked list, map , ... to be non-specific to a data type but more generic
2. Vector Class
3. Grid class  is class used for tables , applications include : chess , matrices ,
   example use of grid would be in a XO game
4. Stack class and its use as a LIFO structure with its functions
   Push() and pop() and peek().
5. Queue class and its use a FIFO structure with itsr functions
   enqueue() , dequeue() and peek
6. Notice that the stack and queue are both a limited usage of the vector class but they provide an important aspect
   which is: reducing the complexity of the system :
   because we can use the vector anywhere but whenever a reader read that the code uses stack data structure he already knows the algorithm and the program method of working whereas if he saw a vector class; he needs to give the program that much more attention
7. the classes can be nested 
   for example: vector <vector <> >or stack<queue <> >
   but notice that the last >> need to have a space between them for syntax

