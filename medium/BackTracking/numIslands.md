# 200. ��������
### ԭ��
����һ���� '1'��½�أ��� '0'��ˮ����ɵĵĶ�ά����������������е����������
�������Ǳ�ˮ��Χ������ÿ������ֻ����ˮƽ�������ֱ���������ڵ�½�������γɡ�
���⣬����Լ��������������߾���ˮ��Χ�� 

ʾ�� 1:
����:
11110
11010
11000
00000
���: 1

ʾ�� 2:
����:
11000
11000
00100
00011
���: 3

����: ÿ������ֻ����ˮƽ��/����ֱ���������ڵ�½�����Ӷ��ɡ�

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/number-of-islands)��https://leetcode-cn.com/problems/number-of-islands

### �ⷨ
```java
public class numIslands {
    private int[][] direction = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    private int row, col;
    public int numIslands(char[][] grid) {
        if(grid.length == 0 || grid[0].length == 0)
            return 0;
        row = grid.length;
        col = grid[0].length;
        int count = 0;
        for(int i = 0; i < row; i++){
            for (int j = 0; j < col; j++)
                if(grid[i][j] == '1'){
                    count++;
                    searchLand(grid, i, j);
                }
        }
        return count;
    }

    private boolean inArea(int x, int y){
        return x >= 0 && x < row && y >= 0 && y < col;
    }

    private void searchLand(char[][] grid, int x, int y){
        grid[x][y] = 0;
        for(int i = 0; i < 4; i++){
            int newX = x + direction[i][0];
            int newY = y + direction[i][1];
            // ��2����������Ϊ����Ҫ��������½����һ�εݹ��ж��ҵ��ұ�ע�ѷ��ʣ�������һ�о��ǽ��б�ע����ô�Ѿ�����ע�ľͲ����ٷ��ʡ�
            if(inArea(newX, newY) && grid[newX][newY] == '1')
                searchLand(grid, newX, newY);
        }
    }
}
```
˼·������
* ������[695. �����������](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/BackTracking/maxAreaOfIsland.md)����һ�£�ֱ�Ӳ���695�⡣
* ����Ҫ�ҵ��ж��ٸ�����ֻ���ҵ�����ĳһ���㣬Ȼ��`count++`��������㿪ʼ������������Ȼ����ȥ������һ�����������ѷ��ʹ��ĵ�ķ�ʽ��695��һ�£���`gird[x][y]`����Ϊ0���ɡ�
* ʱ�临�Ӷ�Ϊ$O(n)$����Ϊ����ÿһ������������η��ʡ��ռ临�Ӷ�ȡ���ڵݹ������ռ�Ŀռ䡣

���н����

 * ִ����ʱ :3 ms, ������ Java �ύ�л�����55.11%���û�
 * �ڴ����� :41.6 MB, ������ Java �ύ�л�����8.21%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз