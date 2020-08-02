## 买卖股票的最佳时机 II

### 分析

你必须在再次购买前出售掉之前的股票

当前题目已经提供了所有时间的股票价格，根据贪心算法的思想，只考虑当前最优解，只要有利润就操作股票买卖

### 题解

``` php

class Solution {

    /**
     * @param Integer[] $prices
     * @return Integer
     */
    function maxProfit($prices) {
        $earning = 0;
        $len = count($prices);
        if ($len) {
            for ($i = 1; $i < $len; $i++) {
                // 贪心，只看当前最优解，有收益就抛掉
                if ($prices[$i] > $prices[$i - 1]) {
                    $earning += $prices[$i] - $prices[$i - 1];
                }
            }
        }
        return $earning;
    }
}

```