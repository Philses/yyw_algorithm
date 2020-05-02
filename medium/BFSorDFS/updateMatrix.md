# 542. 01 ����
### ԭ��
����һ���� 0 �� 1 ��ɵľ����ҳ�ÿ��Ԫ�ص������ 0 �ľ��롣
��������Ԫ�ؼ�ľ���Ϊ 1 ��

ʾ�� 1:
����:
0 0 0
0 1 0
0 0 0
���:
0 0 0
0 1 0
0 0 0

ʾ�� 2:
����:
0 0 0
0 1 0
1 1 1
���:
0 0 0
0 1 0
1 2 1

ע��:
���������Ԫ�ظ��������� 10000��
����������������һ��Ԫ���� 0��
�����е�Ԫ��ֻ���ĸ�����������: �ϡ��¡����ҡ�

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/01-matrix)��https://leetcode-cn.com/problems/01-matrix

### �ⷨ
```java
public class updateMatrix {
    private int row, col;
    private int[][] dires = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    public int[][] updateMatrix(int[][] matrix) {
        row = matrix.length;
        col = matrix[0].length;
        return bfs(matrix,  new int[row][col]);
    }

    private int[][] bfs(int[][] matrix, int[][] res) {
        Queue<int[]> queue = new LinkedList<>();
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (matrix[i][j] == 0) {
                    queue.add(new int[]{i, j});
                }
            }
        }
        while (!queue.isEmpty()) {
            int[] pos = queue.remove();
            for (int[] dire : dires) {
                int newX = pos[0] + dire[0];
                int newY = pos[1] + dire[1];
                if (inArea(newX, newY) && matrix[newX][newY] != 0 && res[newX][newY] == 0) {
                    res[newX][newY] = res[pos[0]][pos[1]] + 1;
                    queue.add(new int[]{newX, newY});
                }
            }
        }
        return res;
    }

    private boolean inArea(int x, int y) {
        return x >= 0 && x < row && y >= 0 && y < col;
    }
}
```
˼·������
* 0��������ľ���Ϊ0��Ҫ�ҵ�1�������0�ľ��룬��һ���ǶȾ������е�0��ĳ��1����̾�������С���Ǹ����롣
* ��Ȼ��Ҫ������0��ĳ��1����̾��룬����һ����Դbfs��������bfs�Ĺ�����ĳ��1��һ�α���������룬����������С���Ǹ����룬��Ϊ�����0���������Ҫ��ͬ���߸���Ĳ�����
* ��άƽ�棬ֻ�������������ĸ����򣬾��ǹ̶�д���ġ�`int row, col`����ʾ����߽硣`int[][] dires = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};`�������ĸ�����`boolean inArea(int x, int y)`���ж�ĳ�������Ƿ��ھ����ڲ���
* ����`int[][] bfs(int[][] matrix, int[][] res)`��
    * �ڶ���������Ϊ��ʾ�𰸵ľ������`res[x][y] == 0`Ҫô�������0��Ҫô�������1����û�б����ʹ���
    * ��Դbfs������ͨ������ѭ��������0�������������С�
    * �������bfs��ģ��д���Լ���άƽ���ĸ������ģ��д��������Ҫע����ǣ�����ĳ��Ԫ�ص�������Ҫ�������㣺1.�ھ���������`inArea(newX, newY)`��2.�õ㲻��0��0��Դͷ�Ͳ��÷�����`matrix[newX][newY] != 0`��3.`res[x][y] == 0`����������2˵���õ㲻��0����ô�������ǻ�û�з��ʵ�1��Ӧ��ȥ���ʡ�
    * �ڵݹ����֮ǰ��`res[newX][newY] = res[pos[0]][pos[1]] + 1;`���õ㵽0�ľ�����Ǵ�����һ���㵽0�ľ���+1����ֵ֮����������̾����������ˡ�
* ��������ʼ����Ա������Ȼ�󷵻ص��ý����
* ʱ�临�Ӷ�Ϊ$O(n)$��n��ʾԪ����������Ϊ�����˾����е�ÿ��Ԫ�ء��ռ临�Ӷ�ҲΪ$O(n)$

���н����

 * ִ����ʱ :23 ms, ������ Java �ύ�л�����42.73%���û�
 * �ڴ����� :43.6 MB, ������ Java �ύ�л�����100.00%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз