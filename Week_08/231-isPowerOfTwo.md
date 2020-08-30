## 2的幂

### 题解

```  php

class Solution {

    /**
     * @param Integer $n
     * @return Boolean
     */
    function isPowerOfTwo($n) {
        // 2 的幂二进制表示只含有一个 1。
        if ($n == 0) {
            return false;
        }
        return ($n & ($n - 1)) == 0
    }
}


```