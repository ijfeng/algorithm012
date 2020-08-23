## 朋友圈

### 分析

* 1 <= N <= 200
* M[i][i] == 1
* M[i][j] == M[j][i]

### 题解

``` php

class Solution {
    /**
     * @param Integer[][] $M
     * @return Integer
     */
    function findCircleNum($m) {
        $count = 0;
        $vis = array_fill(0,sizeof($m),0);
        $queue = [];
        for ($i = 0;$i< sizeof($m);$i++){
            if($vis[$i] == 0){
                array_push($queue,$i);
                while (!empty($queue)){
                    $s = array_shift($queue);//出队
                    $vis[$s] = 1;
                    for ($j = 0;$j<sizeof($m);$j++){
                        if($m[$s][$j] == 1 && $vis[$j] == 0){
                            array_push($queue,$j);//元素入队-继续搜索
                        }
                    }
                }
                $count++;
            }
        }
        return $count;
    }
 }
 //时间复杂度：O(n^3)
 //空间复杂度：O(n)
 
```
