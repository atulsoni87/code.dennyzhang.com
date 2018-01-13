# Leetcode: Binary Search Tree Iterator     :BLOG:Medium:


---

Identity number which appears exactly once.  

---

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.  

Calling next() will return the next smallest number in the BST.  

Note: next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/majority-element-ii)  

Credits To: [Leetcode.com](https://leetcode.com/problems/majority-element-ii/description/)  

Leave me comments, if you know how to solve.  

    ## Basic Ideas: In-order traversal. Use a stack
    ## Complexity:
    ##
    # Definition for a  binary tree node
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class BSTIterator(object):
        def __init__(self, root):
            """
            :type root: TreeNode
            """
            self.stack = 
            if root is None:
                return
            p = root
            while p:
                self.stack.append(p)
                p = p.left
    
        def hasNext(self):
            """
            :rtype: bool
            """
            return len(self.stack) != 0
    
        def next(self):
            """
            :rtype: int
            """
            top_element = self.stack.pop()
            if top_element.right:
                p = top_element.right
                while p:
                    self.stack.append(p)
                    p = p.left
            return top_element.val
    
    # Your BSTIterator will be called like this:
    # i, v = BSTIterator(root), 
    # while i.hasNext(): v.append(i.next())