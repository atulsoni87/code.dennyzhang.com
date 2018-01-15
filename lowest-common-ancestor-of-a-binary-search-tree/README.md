# Leetcode: Lowest Common Ancestor of a Binary Search Tree     :BLOG:Basic:


---

Lowest Common Ancestor of a Binary Search Tree  

---

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.  

According to the definition of LCA on Wikipedia: "The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself)."  

         _______6______
        /              \
     ___2__          ___8__
    /      \        /      \
    0      _4       7       9
          /  \
          3   5

For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/lowest-common-ancestor-of-a-binary-search-tree)  

Credits To: [Leetcode.com](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)  

Leave me comments, if you know how to solve.  

    ## Basic Ideas: For BST, get min(p.val, q.val) and max(p.val, q.val)
    ##              Check from the root node
    ##              If both are smaller than root.val, move the left sub-tree
    ##              If both are bigger than root.val, move the right-tree
    ##              If one smaller and one bigger, the current node is what we want
    ## Assumption: No duplicate value in the BST
    ## Complexity: Time O(k), Space O(1). k is the height
    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class Solution(object):
        def lowestCommonAncestor(self, root, p, q):
            """
            :type root: TreeNode
            :type p: TreeNode
            :type q: TreeNode
            :rtype: TreeNode
            """
            stack = 
            r = root
            min_val = min(p.val, q.val)
            max_val = max(p.val, q.val)
            while r and (r.val > max_val or r.val < min_val):
                if r.val > max_val:
                    r = r.left
                else:
                    r = r.right
            return r