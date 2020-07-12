## 两速之和

### 分析

* nums是整数数组
* 每个输入只会有一个答案
* 同一元素不使用两边
* 返回数组下标

## 题解

### 暴力求解

把所有结果枚举得出结果

``` php

class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {

        // 暴力法
        $len = count($nums);
        for ($i = 0; $i < $len; $i++) {
            for ($j = $i + 1; $j < $len; $j++) {
                if ($nums[$i] + $nums[$j] == $target) {
                    return [$i, $j];
                }
            }
        }
        // 算法复杂度O(n^2)
        // 空间复杂度O(1)

    }
}

```

### 两次哈希表遍历

用空间换时间，将nums元素的值和下标存放到哈希表中（$nums[$i] = $i）, 在通过一次遍历求出目标值减去$i 的结果是否纯在与哈希表中

``` php

class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {

        // 两次哈希表
        $len = count($nums);
        $hash = [];
        // 将值存放进哈希表中
        for ($i = 0; $i < $len; $i++) {
            $hash[$nums[$i]] = $i;
        }

        for ($i = 0; $i < $len; $i++) {
            $res = $target - $nums[$i];
            if ($hash[$res] && $hash[$res] != $i) {
                return [$i, $hash[$res]];
            }
        }
        
        // 算法复杂度O(n)
        // 空间复杂度O(n)
    }
}

```

### 一遍hash表

基于两次哈希表的思路，简化而来。

题目数组中存在一个解，两个元素之间是存在先后顺序的，已知目标值减去当前元素的值，必定会存在于后面的nums中。

根据这个思路。把当前解和下标存放到哈希表中，如果匹配到后面的元素则得出解。

``` php

class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        // 一次哈希表
        $len = count($nums);
        $resArr = [];
        for ($i = 0; $i < $len; $i++) {
            $num = $nums[$i];
            if (!isset($resArr[$num])) {
                $res = $target - $num;
                $resArr[$res] = $i;
                continue;   
            }
            return [$resArr[$num], $i];
        }
        // 算法复杂度O(n)
        // 空间复杂度O(n)
    }
}

```


