# Terminology
- Edge: the line connecting between two nodes
		note: tree has n nodes and (n-1) edges
- Root: parent of tree
- Parent: parent of a group of children nodes
- child: the node linked to by a certain parent node
- siblings: nodes linked to by the same parent node
- descendant / ancestors
- Degree of a node: the number of children of a certain node
- Internal (non-Leaf) (non-Terminal) / External (Leaf) (Terminal) Nodes:
		nodes of zero degree are called leaf nodes / external nodes: E, F, J, K, ..
		
- Levels:  start from one onward
		root node is level 1, its child is level 2 and so on.
- Height: height starts from root and counts the edges
		root has height zero , its child has height 1 and so on.
- Forest: a group of tree having no common root node
		if you add a head node for the forest, you turn it into a tree
		
## Screen Shot from Terminology Part:
	![[Pasted image 20240526175826.png]]

## Binary Tree
a tree where each node has at max 2 children (can have less but no more than 2 children), its children are called right and left child

## Properties of Binary Trees
![[Pasted image 20240526180803.png]]

if we have 3 unlabeled nodes , max no of possible binary trees is 5
if we have 4 unlabeled nodes , max no of possible binary trees is 14

the formula for max no of possible trees is $((2n C n)/(n+1))$

also, max possible no of binary trees with maximum height =  $2^(n-1)$

## Catalan Number
![[Pasted image 20240526182310.png]]

the max no of trees formed from n number of unlabeled nodes is calculated by Catalan Number $$((2n C n)/(n+1))$$ 

and also can be formed by the formula 
$$ SUM from  i->n :  T(i-1) + T(n-i)$$
## Labeled Nodes
no of trees formed from labeled nodes is greater than unlabeled nodes because of the possibilities of different labels in same tree shape
![[Pasted image 20240526184236.png]]

the number of trees for labeled nodes is : Catalan number * factorial n
$2nCn / (n+1) * n!$

for height = h: 
	min no of nodes = $h+1$
	max no of nodes = $2^{(h+1)} - 1$

![[Pasted image 20240526185941.png]]
for no of nodes = n
	max height  = $n-1$
	min height = $log(n+1) -1$
![[Pasted image 20240526193044.png]]

# Conclusion
## Height of binary tree -> $O(log(n)) <= h <= n-1$
## No of nodes in binary tree -> $h+1 <= n <= 2^{h+1} -1$

## Binary Tree Note:
- no of Nodes with deg(0) = no of Nodes with deg(2) +1

## Strict Binary Tree
- are binary trees which only have nodes of degree (0,2) no Unary nodes of deg(1)
- external nodes  = internal nodes + 1

# n-ary Trees (where n is degree)
- n-ary tree is a tree where nodes can't be of degree more than n
- a degree of a tree cannot be deduced, it's pre-decided
- strict n-ary tree is where trees can have 0 or exactly n children.
## strict n-ary trees
![[Pasted image 20240526201419.png]]

External vs Internal Nodes in strict n-ary trees
![[Pasted image 20240526201701.png]]

# Notice
these equations will be used in the analysis when using the trees

