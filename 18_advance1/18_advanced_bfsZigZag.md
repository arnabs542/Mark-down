## Advanced 1 BFS ZigZag Print Binary Tree

* Table of Content
    * 隔板题(Two/N pointers)
    * Minimize #comparsion
    * 剥洋葱
    * BFS print binary tree
    * LCA

> 做题要求
> A complete answer will include the following:
> 1. Document your assumption
> 2. Explain your approach and how you intent to solve the problem
> 3. Provide code comment where applicable
> 4. explain the big-O complexity of your solution. justify your answer
> 5. indentity any additional data structure you used and justify why you used them.
> 6. only provide your best answer to each part of the question.

## Q4.2
```java
/*
 * Get Keys In Binary Tree Layer By Layer Zig-Zag Order
Get the list of keys in a given binary tree layer by layer in zig-zag order.

Examples

        5

      /    \

    3        8

  /   \        \

 1     4        11

the result is [5, 3, 8, 11, 4, 1]

Corner Cases
What if the binary tree is null? Return an empty list in this case.

How is the binary tree represented?
We use the level order traversal sequence with a special symbol "#" denoting the null node.

For Example:
The sequence [1, 2, 3, #, #, 4] represents the following binary tree:

    1

  /   \

 2     3

      /

    4
   	*/

public class KeysInBinartreeZigZag {
	  // 0. keypoints
	  // binary tree ; layer by layer; zig-zag;
	  
	  // 1. assumption
	  // if the root is null, return an empty list
	  
	  // 2. approach
	  // since we can use a queue to print a binary tree layer by layer with the 
	  // normal order, with the BFS method;
	  // we consider use a deque to print it in zig-zag way. We assign a number to 
	  // each layer, say the root is level 1, 
	  // for level with odd number, we expand and generate nodes from right to left, 
	  // corresponding to deque is poolFirst, offerLast
	  // fro level with even number, we expand and generate nodes from left to right,
	  // corresponding to deque is poolLast, offerFirst
	  
	  // 3. data structure
	  // use deque to help us 
	  
	  // 4. comments
	  
	  // 5. big o complexity
	  // n nodes
	  // time: O(n)
	  // space: O(n) 
	  
	  public List<Integer> zigZag(TreeNode root) {
			List<Integer> res = new ArrayList<>();
			
			if (root == null) {
			  return res;
			}
			
			Deque<TreeNode> myDeque = new LinkedList<>();
			myDeque.offerFirst(root);
			int level = 1;
			while (!myDeque.isEmpty()) {
			  int size = myDeque.size();
			  for (int i = 0; i < size; i++) {
			    if (level % 2 == 1) {
			      TreeNode cur = myDeque.pollFirst();
			      res.add(cur.key);
			      if (cur.right != null) {
			        myDeque.offerLast(cur.right);
			      }
			      if (cur.left != null) {
			        myDeque.offerLast(cur.left);
			      }
			    }
			    if (level % 2 == 0) {
			      TreeNode cur = myDeque.pollLast();
			      res.add(cur.key);
			      if (cur.left != null) {
			        myDeque.offerFirst(cur.left);
			      }
			      if (cur.right != null) {
			        myDeque.offerFirst(cur.right);
			      }
			    }
			  }
			  level++;
			}
			return res;
	  }
}
```
