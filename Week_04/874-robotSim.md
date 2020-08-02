## 模拟行走机器人

### 分析

* -2：向左转 90 度
* -1：向右转 90 度
* 1 <= x <= 9：向前移动 x 个单位长度
* 有障碍物

### 题解

```php

class Solution {

    /**
     * @param Integer[] $commands
     * @param Integer[][] $obstacles
     * @return Integer
     */
    function robotSim($commands, $obstacles) {
        $actions = [
            0 => [0, 1],  // 北
            1 => [1, 0],  // 东
            2 => [0, -1], // 南
            3 => [-1, 0]  // 西
        ];

        // 用哈希表来存储障碍点的关键信息，拿空间换时间
        $obstacleMaps = [];
        foreach ($obstacles as $obstacle) {
            $key = implode(',', $obstacle);
            $obstacleMaps[$key] = true;
        }

        $posX = 0;
        $posY = 0;
        $area = 0;
        $direction = 0;
        foreach ($commands as $command) {
            if ($command == -2) {
                // 向左转90度
                $directjon = ($direction + 3) % 4;
            } else if ($command == -1) {
                // 向右转90度每次 +1 mod 4 
                $direction = ($direction + 1) % 4;
            } else {
                for ($i = 0; $i < $command; $i++) {
                    $action = $actions[$direction];
                    $tmpX = $posX + $action[0];
                    $tmpY = $posY + $action[1];
                    if (!isset($obstacleMaps["{$tmpX},{$tmpY}"])) {
                        $posX = $tmpX;
                        $posY = $tmpY;
                        $area = max($area, $posX * $posX + $posY * $posY);
                    } else {
                        break;
                    }
                }
               
            }
        }
        return $area;
    }
}


```
