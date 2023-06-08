# Leetcode-Python17

## 654. Maximum Binary Tree, 617. Merge Two Binary Trees, 700. Search in a Binary Search Tree

June 07, 2023  4h

Congratulations!\
This is the seventeenth day for leetcode python study. Today we will learn more about the Binary Tree!\
The challenges today are about ~~need to delete later~~.


##  654. Maximum Binary Tree
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0654.%E6%9C%80%E5%A4%A7%E4%BA%8C%E5%8F%89%E6%A0%91.md)\
[video](https://www.bilibili.com/video/BV1MG411G7ox/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
[leetcode](https://leetcode.com/problems/maximum-binary-tree/)\
最大二叉树, **构造二叉树都是 前序遍历**，先构造中间节点，再去递归构造左子树和右子树。最后返回最大二叉树根节点的指针。\
递归三部：
1.确定函数的参数和返回值。参数传入的是存放元素的数组，返回该数组构造的二叉树的头结点，返回类型是指向节点的指针。\
2.确定终止条件。当递归遍历时，如果传入的数组大小为1，说明遍历到叶子结点了。当数组大小为1时，构造一个新的节点，并返回。\
3.确定单层递归的逻辑。找到数组中最大值和对应的下标，构造根节点，下标用来下一步分割数组。最大值所在的下标左区间 构造左子树，最大值所在的下标右区间 构造右子树。\
优化方法：\
每次分割不用定义新的数组，而是通过下标索引直接在原数组上操作。
```python
# ways 1: use recursion and middleorder traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        #确定终止条件，传入的数组大小为1.
        if len(nums) == 1:
            return TreeNode(nums[0])
        
        # 找到数组中最大的值和对应的下标 中
        node = TreeNode(0)
        maxValue = 0
        maxValueIndex = 0
        for i in range(len(nums)):
            if nums[i] > maxValue:
                maxValue = nums[i]
                maxValueIndex = i
        node.val = maxValue
        #最大值所在的下标左区间 构造左子树  左
        if maxValueIndex > 0:
            new_list = nums[:maxValueIndex]
            node.left = self.constructMaximumBinaryTree(new_list)
        #最大值所在的下标右区间 构造右子树    右
        if maxValueIndex < len(nums) - 1:
            new_list = nums[maxValueIndex+1:]
            node.right = self.constructMaximumBinaryTree(new_list)
        return node
```
```python
# ways 2: use slicing
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> TreeNode:
        if not nums:
            return None
        max_val = max(nums)
        max_index = nums.index(max_val)
        node = TreeNode(max_val)
        node.left = self.constructMaximumBinaryTree(nums[:max_index])
        node.right = self.constructMaximumBinaryTree(nums[max_index+1:])
        return node
```


## 617. Merge Two Binary Trees
[leetcode](https://leetcode.com/problems/merge-two-binary-trees/)\
合并二叉树，优先掌握递归。同步遍历两个tree，前序遍历。
```python
# ways 1: use recursion and middleorder traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        #递归终止条件
        if not root1:
            return root2
        if not root2:
            return root1
        root1.val += root2.val  #middle
        root1.left = self.mergeTrees(root1.left, root2.left)    #left
        root1.right = self.mergeTrees(root1.right, root2.right)    #left
        return root1
```
```python
# ways 2: use recursion and middleorder traversal, build a new node
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        #递归终止条件
        if not root1:
            return root2
        if not root2:
            return root1
        root = TreeNode()   # 创建新节点
        root.val += root1.val + root2.val   #middle
        root.left = self.mergeTrees(root1.left, root2.left)  #left
        root.right = self.mergeTrees(root1.right, root2.right)  #right
        return root
```


## 700. Search in a Binary Search Tree
[leetcode](https://leetcode.com/problems/search-in-a-binary-search-tree/)\
二叉搜索树中的搜索，**递归和迭代** 都可以掌握以下，因为本题比较简单，了解二叉搜索树的特性。



## 98.
验证二叉搜索树，遇到 搜索树，一定想着中序遍历，这样才能利用上特性。但本题是有陷阱的，可以自己先做一做，然后在看题解，看看自己是不是掉陷阱里了。这样理解的更深刻。




