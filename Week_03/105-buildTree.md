## 从前序与中序遍历序列构造二叉树

### 分析

* 前序遍历 根左右
* 中序遍历 左根右
* 没有重复的元素

### 题解

#### 递归1

``` php

class Solution {

    public $iMap;

    /**
     * @param Integer[] $preorder
     * @param Integer[] $inorder
     * @return TreeNode
     */
    function buildTree($preorder, $inorder) {
        $this->iMap = array_flip($inorder);
        $pCount = count($preorder);
        return $this->buildTreeHelper($preorder, $inorder, 0, $pCount - 1, 0, $pCount);
    }

    function buildTreeHelper($preorder, $inorder, $preorder_left, $preorder_right, $inorder_left, $inorder_right) {

        if ($preorder_left > $preorder_right) {
            return null;
        }

        $preorder_root = $preorder_left;
        $inorder_root = $this->iMap[$preorder[$preorder_root]];

        $tree = new TreeNode($preorder[$preorder_root]);

        $size_left_subtree = $inorder_root - $inorder_left;
        $tree->left = $this->buildTreeHelper($preorder, $inorder, $preorder_left + 1, $preorder_left + $size_left_subtree, $inorder_left, $inorder_root - 1);                         
        $tree->right = $this->buildTreeHelper($preorder, $inorder, $preorder_left + $size_left_subtree + 1, $preorder_right, $inorder_root + 1, $inorder_right);
        return $tree;
    }

}

```

* 时间复杂度 O(n)
* 空间复杂度 O(n)
