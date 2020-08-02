## 柠檬水找零

### 分析

* 面值有5、10、20
* 每杯柠檬水5块
* 每次只买1杯
* 一开始手头上没有零钱

因为面额没有超过20的，所以一旦有客人付款了20个，我们找零后无需记录

面额5时不需要找零

面额10时找5块钱

面额20是，我们优先找10块 + 5块的组合方案，如果无法达成则考虑选择3张5块来找零

### 题解

``` php

class Solution {

    /**
     * @param Integer[] $bills
     * @return Boolean
     */
    function lemonadeChange($bills) {
        $ten = $five = 0;
        $len = count($bills);
        for ($i = 0; $i < $len; $i ++) {
            $bill = $bills[$i];
            if ($bill == 5) {
                // 不用找零
                $five ++;
            } else if ($bill == 10) {
                // 只要5块零钱有充裕就可满足条件
                if ($five > 0) {
                    $five --;
                    $ten ++;
                } else {
                    return false;
                }
            } else {
                // 优先考虑10 + 5 的组合，如果没有则 5 * 3 的组合
                if ($five > 0 && $ten > 0) {
                    $five --;
                    $ten --;
                } else if ($five >= 3) {
                    $five -= 3;
                } else {
                    return false;
                }
            }
        }
        return true;
    }
}

```