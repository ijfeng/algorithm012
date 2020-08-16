## 最大正方形

## 分析

* 在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。
* 组成一个完整的正方形当前元素需要考虑 左、左上、上 三个位置

## 题解

``` php 

class Solution {

    /**
     * @param String[][] $matrix
     * @return Integer
     */
    function maximalSquare($matrix) {

        $res = 0;
        $row = count($matrix);
        $columns = count($matrix[0])
        if ($matrix == null || $row == 0 || $columns == 0) {
            return $res;
        }

       ;

        // dp # 1
        // $dp = [];
        // for ($i = 0; $i < $row; $i ++) {
        //     for ($j = 0; $j < $columns; $j ++) {
        //         // 当前位置是1
        //         if ($matrix[$i][$j] == "1") {
        //             if ($i == 0 || $j == 0) {
        //                 // 边缘位置
        //                 $dp[$i][$j] = 1;
        //             } else {
        //                 // 组成一个完整的正方形当前元素需要考虑 左、左上、上 三个位置，取最小值 + 1可得连续完整正方形尺寸，如果包含0则当前位置保持1。
        //                 $dp[$i][$j] = min($dp[$i - 1][$j], $dp[$i][$j - 1], $dp[$i - 1][$j - 1]) + 1;
        //             }
        //             $res = max($res, $dp[$i][$j]);
        //         }
        //     }
        // }
        // 时间复杂度 O($row * $columns) = O(nm);
        // 空间复杂度 O(nm) $dp 数组储存了$matrix二维矩阵大小的数据
        

        // dp #2
        for ($i = 0; $i < $row; $i ++) {
            for ($j = 0; $j < $columns; $j ++) {
                if ($matrix[$i][$j] == "1") {
                    if ($i != 0 && $j != 0) {
                        $matrix[$i][$j] = min(
                            $matrix[$i - 1][$j], 
                            $matrix[$i][$j - 1], 
                            $matrix[$i - 1][$j - 1]
                        ) + 1;
                    }
                    $res = max($res, $matrix[$i][$j]);
                }
            }
        }
        // 空间复杂度 O(1) 进一步优化内存空间，不用重新申请一个$dp数组，直接在原地操作

        return $res * $res;
    }
}

```