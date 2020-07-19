## 二叉树的前序遍历

### 分析

* 前序遍历
* 与N叉树遍历规则基本一致

### 题解

#### 递归

``` php

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($value) { $this->val = $value; }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[]
     */
    function preorderTraversal($root) {
        $arr = [];
        if (!$root) {
            return $arr;
        }

        // 递归
        $thjs->recursive($arr, $root);
        return $arr;
    }
    
    function recursive(& $arr, $node) {
        $arr[] = $node->val;
        if ($node->left) {
            $this->recursive($arr, $node->left);
        }

        if ($node->right) {
            $this->recursive($arr, $node->right);
        }
    }
}

```

#### 栈

``` php

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($value) { $this->val = $value; }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[]
     */
    function preorderTraversal($root) {
        $arr = [];
        if (!$root) {
            return $arr;
        }

        // 栈 
        $stack = new SplStack();
        $stack->push($root);
        while (!$stack->isEmpty()) {
            $node = $stack->pop();
            $arr[] = $node->val;
            
            // 根据栈的特性，先push右边节点 [right, left] 此时left在栈顶符合前序遍历
            if ($node->right) {
                $stack->push($node->right);
            }

            if ($node->left) {
                $stack->push($node->left);
            }
        }
        return $arr;
    }

```