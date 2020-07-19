## 有效的字母异位词

### 分析

* 只包含小写
* 字母异位 - 拥有相同数量的字母，只是字符位置不同

### 题解

#### 排序对比

将字符按顺序排序，后对比两个数组
 
``` php

class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return Boolean
     */
    function isAnagram($s, $t) {
        
        $sLen = strlen($s);
        $tLen = strlen($t);
        if ($sLen != $tLen) {
            // 如果字符串不相等那便可能是异位词
            return false;
        }
    
        $s = str_split($s, 1);
        $t = str_split($t, 1);
        sort($s);
        sort($t);
        return $s == $t;
    }
}

```

#### 哈希表计数法

``` php


class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return Boolean
     */
    function isAnagram($s, $t) {

        $sLen = strlen($s);
        $tLen = strlen($t);
        if ($sLen != $tLen) {
            // 如果字符串不相等那便可能是异位词
            return false;
        }

        // 创建一个哈希表处理计数
        $sHashCount = [];
        for ($i = 0; $i < $sLen; $i ++) {
            if (!isset($sHashCount[$s[$i]])) {
                $sHashCount[$s[$i]] = 0;
            }
            $sHashCount[$s[$i]] += 1;
        }

        for ($i = 0; $i < $tLen; $i ++) {
            // 如果出现s字符串没有的字符，则不成立
            if (!isset($sHashCount[$t[$i]])) {
                return false;
            }

            $sHashCount[$t[$i]] -= 1;
            if (!$sHashCount[$t[$i]]) {
                unset($sHashCount[$t[$i]]);
            }
        }
        
        // 如果是空则是异位词
        return empty($sHashCount)
    }
}

```

* 算法复杂度 O(n)
* 空间复杂度 O(1)

#### PHP内置函数

思路与哈希表计数基本一致

``` php

class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return Boolean
     */
    function isAnagram($s, $t) { 

        // php 内置函数方法
        $sLen = strlen($s);
        $tLen = strlen($t);
        if ($sLen != $tLen) {
            return false;
        }
        
        // 函数返回字符串中所用字符的信息
        return count_chars($s,1) == count_chars($t,1)
    }
}

```
