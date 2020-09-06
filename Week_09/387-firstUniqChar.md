## 字符串中的第一个唯一字符

### 题解

```php

class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function firstUniqChar($s) {
        
        // 给每个字符进行计数
        $hashMap = [];
        $len = strlen($s);
        for ($i = 0; $i < $len; $i ++) {
            $substring = $s[$i];
            $hashMap[$substring] += 1;
        }
   
        // 第一个计数唯一的字符为解
        for ($i = 0; $i < $len; $i ++) {
            if ($hashMap[$s[$i]] == 1) {
                return $i;
            }
        }
        // 算法复杂度 O(n)
        // 空间复杂度 O(n)
        return -1;
    }
}

```