## 爬楼梯

### 分析

* 给定N是正整数
* 只能爬1阶梯或者2阶梯

### 题解

#### 递归1

``` php

class Solution {

    /**
     * @param Integer $n
     * @return Integer
     */
    function climbStairs($n) {
        if ($n == 1) {
            return 1;
        }

        if ($n == 2) {
            return 2;
        }
        return $this->climbStairs($n - 1) + $this->climbStairs($n - 2);
    }
}