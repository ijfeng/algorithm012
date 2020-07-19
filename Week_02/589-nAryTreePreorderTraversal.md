## N叉树的前序遍历

### 题解

#### 递归


``` php

/**
 * Definition for a Node.
 * class Node {
 *     public $val = null;
 *     public $children = null;
 *     function __construct($val = 0) {
 *         $this->val = $val;
 *         $this->children = array();
 *     }
 * }
 */

class Solution {
    /**
     * @param Node $root
     * @return integer[]
     */
    function preorder($root) {
        // 从根节点开始最左优先
        if (!$root) {
            return [];
        }

        $resArr = [];
        $this->recursive($resArr, $root);
        // 用递归的方式处理。 只需要考虑单个节点的的顺序输出。
        return $resArr;
    }

    function recursive(& $resArr, $node) {
        $resArr[] = $node->val;
        foreach ($node->children as $childrenNode) {
            $this->recursive($resArr, $childrenNode);
        }
    }


```

#### 栈遍历

``` php

/**
 * Definition for a Node.
 * class Node {
 *     public $val = null;
 *     public $children = null;
 *     function __construct($val = 0) {
 *         $this->val = $val;
 *         $this->children = array();
 *     }
 * }
 */

class Solution {
    /**
     * @param Node $root
     * @return integer[]
     */
    function preorder($root) {
        // 从根节点开始最左优先
        if (!$root) {
            return [];
        }

        stack 栈遍历
        $stack = new SplStack();
        $resArr = [];
        $stack->push($root);
        while (!$stack->isEmpty()) {
            $node = $stack->pop();
            $resArr[] = $node->val;
            $childrenCount = count($node->children);
            if ($childrenCount) {
                // 根据前序遍历规则，应该依次从左开始遍历
                // 从最又节点开始入栈，依次出栈处理时就满足了前序遍历
                for ($i = $childrenCount - 1; $i >= 0; $i--) {
                    $stack->push($node->children[$i]);
                }
            }
        }
        return $resArr;
    }

}

```
