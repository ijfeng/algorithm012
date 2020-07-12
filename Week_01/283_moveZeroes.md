## 移动零


### 分析

* 非零元素的相对顺序
* 原地操作



## 题解

### 两次遍历

``` php
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function moveZeroes(&$nums) {
        // 边界判断
        if (empty($nums) || !count($nums)) {
            return null;
        }

        $len = count($nums);
        $j = 0; // 记录非零下标
        for ($i = 0; $i < $len; $i++) {
            // 当前数非0
            if ($nums[$i] != 0) {
                // 将非0元素以$j为下标依次插入数组
                $nums[$j] = $nums[$i];
                $j ++;
            }
        }

        // 所有非0元素处理完成后，从$j可得当前非零数据数量
        for ($i = $j; $i < $len; $i++) {
            // $len - $j 等于0 的数量，将数组后面数据设为0
            $nums[$i] = 0;
        }
        return $nums;
    }
}

```

时间复杂度：O(n)
空间复杂度：O(1)

*** 

#### 一次遍历

``` php
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function moveZeroes(&$nums) {
        // 边界判断
        if (empty($nums) || !count($nums)) {
            return null;
        }

        $len = count($nums);
        $j = 0;  // 记录非零下标
        for ($i = 0; $i < $len; $i ++) {
            if ($nums[$i] != 0) {
                // 当前数非0
                if ($i > $j) {
                    // 如果当前元素是非 0 的，那么它的正确位置最多可以是当前位置或者更早的位置。
                    $nums[$j] = $nums[$i];
                    // 用0填充当前位置，它可能是最终可能被非零0或者0占据。
                    $nums[$i] = 0;
                }
                 $j ++;
            }
        }
        return $nums;
    }
}

```

时间复杂度：O(n)
空间复杂度：O(1)


