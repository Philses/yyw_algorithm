# 1091. �����ƾ����е����·��
### ԭ��
��һ�� N �� N �ķ��������У�ÿ����Ԫ��������״̬���գ�0������������1����
һ�������Ͻǵ����½ǡ�����Ϊ k �ĳ�ͨ·�������������������ĵ�Ԫ��` C_1, C_2, ..., C_k` ��ɣ�
���ڵ�Ԫ�� `C_i` �� `C_{i+1} `�ڰ˸�����֮һ����ͨ����ʱ��`C_i `�� `C_{i+1} `��ͬ�ҹ���߻�ǣ�
`C_1 `λ�� (0, 0)������ֵΪ `grid[0][0]`��
`C_k` λ�� (N-1, N-1)������ֵΪ `grid[N-1][N-1]`��
��� `C_i` λ�� (r, c)���� `grid[r][c]` Ϊ�գ�����`grid[r][c] == 0`��
�������������Ͻǵ����½ǵ���̳�ͨ·���ĳ��ȡ����������������·�������� -1 �� 

ʾ�� 1��
���룺[[0,1],[1,0]]
�����2

ʾ�� 2��
���룺[[0,0,0],[1,1,0],[1,1,0]]
�����4

��ʾ��

```
1 <= grid.length == grid[0].length <= 100
grid[i][j] Ϊ 0 �� 1
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/shortest-path-in-binary-matrix)��https://leetcode-cn.com/problems/shortest-path-in-binary-matrix

### �ⷨ
```java
public class shortestPathBinaryMatrix {
    private static int[][] directions = {{0,1}, {0, -1}, {1, -1}, {1, 0}, {1, 1}, {-1, -1}, {-1, 0}, {-1, 1}};
    private int row, col;
    public int shortestPathBinaryMatrix(int[][] grid) {
        row = grid.length;
        col = grid[0].length;
        if(grid[0][0] == 1 || grid[row - 1][col - 1] == 1) return -1;
        Queue<int[]> pos = new LinkedList<>();
        grid[0][0] = 1; // ֱ����grid[i][j]��¼����㵽���������·�������������� ���Ҳ�г���1
        pos.add(new int[]{0,0});
        while(!pos.isEmpty() && grid[row - 1][col - 1] == 0){ // �����·�� ʹ��BFS
            int[] xy = pos.remove();
            int preLength = grid[xy[0]][xy[1]]; // ��ǰ���·������
            for(int i = 0; i < 8; i++){
                int newX = xy[0] + directions[i][0];
                int newY = xy[1] + directions[i][1];
                if(inGrid(newX, newY) && grid[newX][newY] == 0){
                    pos.add(new int[]{newX, newY});
                    grid[newX][newY] = preLength + 1; // ��һ�����·������Ҫ+1
                }
            }
        }
        return grid[row - 1][col - 1] == 0 ? -1 : grid[row - 1][col - 1]; // �������յ��ֵ����0��˵��û�е���
    }

    private boolean inGrid(int x, int y){
        return x >= 0 && x < row && y >= 0 && y < col;
    }
}

```
˼·������
* Ҫ�ҵ����Ͻǵ����½ǵ����·�������·�����Ȼ���뵽��ʹ��BFS��
* �ڶ�άƽ���ϣ��˸�������Խ����ƶ���ʹ��`int[][] directions`��ʾ�˸����򡣱���`{1,1}`�ͱ�ʾ���·��򡣶�άƽ�泣��������ʹ�ú���`boolean inGrid(int x, int y)`�ж�ĳ�����Ƿ��ھ��η�Χ�ڣ���ֹ����Խ�磩��
* ���Ƚ���Ա��������ʾ������������`row, col`��ʼ����Ȼ��������Ͻǻ������½�Ϊ1��һ���޷������Ͻǵ����½ǣ�ֱ�ӷ���-1��
* Ȼ��ʼʹ�ö���ģ��BFS��
    * ������Ҫȥ�ж���Щ·���Ѿ��߹����������ǻ���Ҫ֪���ߵ�ĳһ����ʱ�Ĳ����������Ŀ�涨0��ͨ�У�1�ǲ���ͨ�У��߹��ĵ�Ҳ���������൱�ڲ���ͨ�С��������ǿ�����`grid[newX][newY] == 0`��ʾû�з��ʹ��Ŀ�ͨ�еĵ㡣
    * �������⣬���Ҳ�г���1����������`grid[0][0] = 1;`����` pos.add(new int[]{0,0});`��
    * �ö���ģ���ѭ������`!pos.isEmpty() && grid[row - 1][col - 1] == 0`���ڶ�������������ʱ��˵���Ѿ���·���������½��ˣ��Ϳ���ֹͣ������
    * ����ĳ��������꣬ͨ��`int preLength = grid[xy[0]][xy[1]];`�õ�����õ�ĳ��ȣ�Ȼ�����8��������ͼ������һ���㣬����`inGrid(newX, newY) && grid[newX][newY] == 0`����Է��ʣ�Ȼ�󵽴���һ�����·�����Ⱦͱ�Ϊ`grid[newX][newY] = preLength + 1;`��Ȼ�������`grid[newX][newY] != 0`�ˣ��Ͳ��ᱻ�ظ����ʡ�
* ѭ�������󣬿�����������ɵ�û�е������½ǣ���ʱ`grid[row - 1][col - 1] == 0`��Ҳ�������Ѿ��ҵ��������½ǵ�·������BFS����ʱ`grid[row - 1][col - 1]`��Ϊ�𰸡�������󷵻�`grid[row - 1][col - 1] == 0 ? -1 : grid[row - 1][col - 1];`
* ʱ�临�Ӷ�Ϊ$O(n)$����Ϊÿ��Ԫ�ر�����һ�Σ�nΪԪ�صĸ������ռ临�Ӷ�Ϊ$O(k)$��kΪ�����ж��е����Ԫ�ظ�����

���н����

* ִ����ʱ :15 ms, ������ Java �ύ�л�����97.87%���û�
* �ڴ����� :42.3 MB, ������ Java �ύ�л�����100.00%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз