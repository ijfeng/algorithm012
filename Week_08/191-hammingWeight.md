## 位1的个数

### 题解

```php

class Solution {
    /**
     * @param Integer $n
     * @return Integer
     */
    function hammingWeight($n) {
        
        // #1 
        // 通过位移每次判断最后一位是否是1
        // 一共32位
        //$sum = 0;
        //$mask = 1;
        //for ($i = 0; $i < 32; $i++) {
        //    if ($n & $mask) {
        //        $sum ++;
        //    }             
        //    $mask <<= 1;     
        //} 
         
        // #2
        // 把最后一个1反转，答案+1 ，当数字变成0的时候就没有1的位了
        $sum = 0;
        while ($n != 0) {
            $sum++;
            $n &= ($n - 1);
        }
        return $sum;
    }
}

```