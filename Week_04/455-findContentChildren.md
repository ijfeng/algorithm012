## 分发饼干

### 分析

* 一个小朋友拥有一块
* 所有小朋友的胃口为正数

### 题解

#### 暴力法

遍历两次

``` php

class Solution {

    /**
     * @param Integer[] $g
     * @param Integer[] $s
     * @return Integer
     */
    function findContentChildren($g, $s) {
         // 暴力法
         $count = 0;
         sort($g);
         sort($s);
         foreach ($g as $gi) {
             foreach ($s as $k => $si) {
                 if ($si >= $gi) {
                     unset($s[$k]);
                     $count ++;
                     break;
                 }
             }
         }
         return $count;
    }
}


```

#### 双指针遍历

```php

class Solution {

    /**
     * @param Integer[] $g
     * @param Integer[] $s
     * @return Integer
     */
    function findContentChildren($g, $s) {
         if (empty($g) || empty($s)) {
                 return 0;
          }
          sort($g);
          sort($s);
          $sl = count($s);
          $gi = 0;
          for ($si = 0; $si < $sl; $si ++) {
              // 两组数据是有序的。
              // 根据贪心算法原则，最近一次满足就 count ++
              if (isset($g[$gi]) && $s[$si] >= $g[$gi]) {
                  $gi ++;
              }
          }
          return $gi;
    }
}

```