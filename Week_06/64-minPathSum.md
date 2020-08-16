## 最小路径和

### 分析

* 每个单元格只能往左走往右走
* 那么选择往左走往右走只要对比哪个更小即可

### 题解

``` php

class Solution {

    /**
     * @param Integer[][] $grid
     * @return Integer
     */
    function minPathSum($grid) {
        
        // 每个单元格只能往左走往右走
        // 那么选择往左走往右走只要对比哪个更小即可
        // 每一个格子都这样计算最后可得结果
        $rowLen = count($grid);
        $columnLen = count($grid[0]);

        // dp #1
        // $dp = [];
        // $dp[0][0] = $grid[0][0]; // 第一项数据不用变化
        // for ($ri = 1; $ri < $rowLen; $ri ++) {
        //     $dp[$ri][0] = $dp[$ri - 1][0] + $grid[$ri][0];
        // }
        // for ($ci = 1; $ci < $columnLen; $ci ++) {
        //     $dp[0][$ci] = $dp[0][$ci - 1] + $grid[0][$ci];
        // }
        // for ($ri = 1; $ri < $rowLen; $ri ++) {
        //     for ($ci = 1; $ci < $columnLen; $ci ++) {
        //         $dp[$ri][$ci] = min($dp[$ri - 1][$ci], $dp[$ri][$ci - 1]) + $grid[$ri][$ci];
        //     }
        // }
        // 算法复杂度 O(nm) 
        // 空间复杂度 O(nm)
        // return $dp[$rowLen - 1][$columnLen - 1];
      

        // dp #2
        for ($i = 0; $i < $rowLen; $i ++) {
            for ($j = 0; $j < $columnLen; $j ++) {
                if ($i == 0 && $j != 0) {
                    // 处理第一行
                    $grid[$i][$j] = $grid[$i][$j] + $grid[$i][$j - 1];
                } else if ($i != 0 && $j == 0) {
                    // 处理第一列
                    $grid[$i][$j] = $grid[$i][$j] + $grid[$i - 1][$j];  
                } else if ($i == 0 && $j == 0) {
                    // 第一项
                    $grid[$i][$j] = $grid[$i][$j];
                } else {
                    $grid[$i][$j] = min($grid[$i][$j - 1], $grid[$i - 1][$j]) + $grid[$i][$j];
                }
            }
        }
        // 算法复杂度 O(nm)
        // 空间复杂度 O(1)
        return $grid[$rowLen - 1][$columnLen - 1];
    }
}

```