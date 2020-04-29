# 695. �����������
### ԭ��
����һ��������һЩ 0 �� 1 �ķǿն�ά���� grid ��
һ�� ���� ����һЩ���ڵ� 1 (��������) ���ɵ���ϣ�����ġ����ڡ�Ҫ������ 1 ������ˮƽ������ֱ���������ڡ�����Լ��� grid ���ĸ���Ե���� 0������ˮ����Χ�š�
�ҵ������Ķ�ά���������ĵ��������(���û�е��죬�򷵻����Ϊ 0 ��) 

ʾ�� 1:

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

�������������������Ӧ���� 6��ע��𰸲�Ӧ���� 11 ����Ϊ����ֻ�ܰ���ˮƽ��ֱ���ĸ������ 1 ��

ʾ�� 2:
[[0,0,0,0,0,0,0,0]]
����������������ľ���, ���� 0

ע��: �����ľ���grid �ĳ��ȺͿ�ȶ������� 50��

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/max-area-of-island)��https://leetcode-cn.com/problems/max-area-of-island

### �ⷨ
```java
public class maxAreaOfIsland {
     private static int[][] dires = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    private int curArea;
    private int row, col;
    public int maxAreaOfIsland(int[][] grid) {
        row = grid.length;
        if(row == 0)
            return 0;
        col = grid[0].length;
        int maxArea = 0;
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(grid[i][j] != 0){
                    curArea = 0;
                    backTrack(grid, i, j);
                    maxArea = Math.max(maxArea, curArea);
                }
            }
        }
        return maxArea;
    }

    private void backTrack(int[][] grid, int x, int y){
        grid[x][y] = 0;
        curArea++;
        for(int[] dire : dires){
            int newX = x + dire[0];
            int newY = y + dire[1];
            if(isIn(newX, newY) && grid[newX][newY] != 0)
                backTrack(grid, newX, newY);
        }
    }

    private boolean isIn(int x, int y){
        return x >= 0 && x < row && y >= 0 && y < col;
    }
}

```
˼·������
* ��άƽ�棬������Ϊ���ھ������������ĸ�������һ���άƽ�棬���������ƶ����ⶼ��ͬ��һ����·��
    * �ж�ĳ�������Ƿ��������ڣ���֤���鲻��Խ�磬�ó�Ա����`private int row, col;`�ֱ��ʾ������к��С���������`boolean isIn(int x, int y)`�ж�����`x,y`�Ƿ��ھ��������ڣ�ֱ�ӷ���`return x >= 0 && x < row && y >= 0 && y < col;`
    * ��ʾ���������ƶ�������` private static int[][] dires = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};`
    * ���������Ҫ�����ѷ��ʵ����꣬���������Ŀ�в�ͬ�Ĵ���취��
* ����Ҫ��������������������ڵ�1����ж��ٸ�����Դdfs�ҵ�ÿһ�������ж��ٸ�1��������˵���ǻ���Ҳ���ԡ�
* ������ݺ���`void backTrack(int[][] grid, int x, int y)`��
    * ����˼����������ô����ĳ�������ѷ��ʣ���Ϊ����ֻ��ҪȥѰ�����ڵ�1������Ҫȥ����0�������Ƿ��ʹ�ĳһ��1��Ҳ������ȥ�����������Խ�`gird[x][y]`����Ϊ0���ɣ�������һ��Ҫ���ʵĵ�ʱ���ж�`gird[x][y] != 0`��ȥ���ʡ����Ի��ݺ���һ��ʼ����`grid[x][y] = 0;`
    * ����Ҫ��¼��ǰ����������������Ե�����`x, y`�����ʱ���������`curArea++;`
    * Ȼ��forѭ�����ֱ�ȥ�������������ĸ���������`isIn(newX, newY) && grid[newX][newY] != 0`�������һ����`newX, newY`��
* �������У����Ƚ�`row, col`���и�ֵ�����`row == 0`˵��û���κ�Ԫ�أ�ֱ�ӷ��ء�Ȼ�����������ÿ��Ԫ�أ�������һ��Ԫ����1ʱ��˵������һ����Ҫ��������ĵ������Դ˵�Ϊ��㿪ʼ����dfs��
    * ����Ҫ`curArea = 0;`���õ�ǰ�������Ϊ0��
    * Ȼ�����`backTrack(grid, i, j);`
    * �����굱ǰ��������`maxArea = Math.max(maxArea, curArea);`
* ʱ�临�Ӷ�Ϊ$O(n)$����Ϊ����ÿһ������������η��ʡ��ռ临�Ӷ�ȡ���ڵݹ������ռ�Ŀռ䡣

���н����

  * ִ����ʱ :3 ms, ������ Java �ύ�л�����82.11%���û�
  * �ڴ����� :40.8 MB, ������ Java �ύ�л�����92.44%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз