# Leetcode: Mini Parser     :BLOG:Basic:


---

Mini Parser  

---

Given a nested list of integers represented as a string, implement a parser to deserialize it.  

Each element is either an integer, or a list &#x2013; whose elements may also be integers or other lists.  

Note: You may assume that the string is well-formed:  

-   String is non-empty.
-   String does not contain white spaces.
-   String contains only digits 0-9, [, - ,, ].

    Example 1:
    
    Given s = "324",
    
    You should return a NestedInteger object which contains a single integer 324.

    Example 2:
    
    Given s = "[123,[456,[789]]]",
    
    Return a NestedInteger object containing a nested list with 2 elements:
    
    1. An integer containing value 123.
    2. A nested list containing two elements:
        i.  An integer containing value 456.
        ii. A nested list with one element:
             a. An integer containing value 789.

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/mini-parser)  

Credits To: [leetcode.com](https://leetcode.com/problems/mini-parser/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: https://brain.dennyzhang.com/mini-parser
    # """
    # This is the interface that allows for creating nested lists.
    # You should not implement it, or speculate about its implementation
    # """
    #class NestedInteger(object):
    #    def __init__(self, value=None):
    #        """
    #        If value is not specified, initializes an empty list.
    #        Otherwise initializes a single integer equal to value.
    #        """
    #
    #    def isInteger(self):
    #        """
    #        @return True if this NestedInteger holds a single integer, rather than a nested list.
    #        :rtype bool
    #        """
    #
    #    def add(self, elem):
    #        """
    #        Set this NestedInteger to hold a nested list and adds a nested integer elem to it.
    #        :rtype void
    #        """
    #
    #    def setInteger(self, value):
    #        """
    #        Set this NestedInteger to hold a single integer equal to value.
    #        :rtype void
    #        """
    #
    #    def getInteger(self):
    #        """
    #        @return the single integer that this NestedInteger holds, if it holds a single integer
    #        Return None if this NestedInteger holds a nested list
    #        :rtype int
    #        """
    #
    #    def getList(self):
    #        """
    #        @return the nested list that this NestedInteger holds, if it holds a nested list
    #        Return None if this NestedInteger holds a single integer
    #        :rtype List[NestedInteger]
    #        """
    class Solution(object):
        ## Basic Ideas: Stack
        ##     Whenever we found '[', DO NOT push. 
        ##         We initialize a empty NestedInteger as place holder
        ##     Whenever we found ']', we combine the last 2 place holers
        ##     Whenever we found digits/'-', look ahead to get what we need. 
        ##               Then construct NestedInteger, then combine it into last place holder
        ##
        ## Complexity: Time O(n), Space O(n)
        def deserialize(self, s):
            """
            :type s: str
            :rtype: NestedInteger
            """
            if len(s) == 0: return None
            if s.find('[') == -1: return NestedInteger(int(s))
    
            stack = []
            for word in s.split(','):
                i = 0
                while i< len(word):
                    if word[i] == '[':
                        stack.append(NestedInteger())
                        i += 1
                    elif word[i] == ']':
                        n1 = stack.pop()
                        n2 = stack.pop()
                        stack.append(n2+n1)
                        i += 1
                    else:
                        # keep looking ahead until we get an non-digits
                        string = ''
                        while i<len(word) and (word[i].isdigit() or word[i] == '-'):
                            string = "%s%s" % (string, word[i])
                            i += 1
                        n = stack.pop()
                        stack.append(n + NestedInteger(int(string)))
            return stack[0]
    
        ## Basic Ideas: Stack
        ##              Whenever we found '[', push
        ##              Whenever we found ']', we keep poping until we find a '['
        ##
        ## Complexity: Time O(n), Space O(n)
        def deserialize(self, s):
            """
            :type s: str
            :rtype: NestedInteger
            """
            if len(s) == 0: return None
            if s.find('[') == -1: return NestedInteger(int(s))
    
            stack = []
            for word in s.split(','):
                num_str = ''
                for ch in word:
                    if ch == '[':
                        stack.append(ch)
                        continue
                    if ch != ']':
                        num_str = '%s%s' % (num_str, ch)
                    else:
                        if num_str != '':
                            stack.append(NestedInteger(int(num_str)))
                            num_str = ''
                        # The sequence we get is right from left, but we need left from right.
                        l = []
                        while True:
                            element = stack.pop()
                            if element == '[':
                                break
                            l.insert(0, element)
                        n = NestedInteger() 
                        for element in l: n.add(element)
                        stack.append(n)
                if num_str != '':
                    stack.append(NestedInteger(int(num_str)))
            return stack[0]

---

Similar Problems:  
-   [Leetcode: Flatten Nested List Iterator](https://brain.dennyzhang.com/flatten-nested-list-iterator)
-   [Review: Stack Problems](https://brain.dennyzhang.com/review-stack)