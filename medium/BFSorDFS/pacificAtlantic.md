# 417. ̫ƽ�������ˮ������
### ԭ��
����һ�� m x n �ķǸ�������������ʾһƬ��½�ϸ�����Ԫ��ĸ߶ȡ���̫ƽ�󡱴��ڴ�½����߽���ϱ߽磬���������󡱴��ڴ�½���ұ߽���±߽硣
�涨ˮ��ֻ�ܰ����ϡ��¡������ĸ�������������ֻ�ܴӸߵ��ͻ�����ͬ�ȸ߶���������
���ҳ���Щˮ���ȿ�����������̫ƽ�󡱣������������������󡱵�½�ص�Ԫ�����ꡣ

��ʾ��
��������˳����Ҫ
m �� n ��С��150

ʾ����
��������� 5x5 ����:

```
  ̫ƽ�� ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * ������
```

����:
[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (��ͼ�д����ŵĵ�Ԫ).

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/pacific-atlantic-water-flow)��https://leetcode-cn.com/problems/pacific-atlantic-water-flow

### �ⷨ
```java
public class pacificAtlantic {
    private static int[][] dires = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    private int m, n;
    private int[][] matrix;

    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> res = new ArrayList<>();
        m = matrix.length;
        if (m == 0)
            return res;
        n = matrix[0].length;
        if (n == 0)
            return res;
        this.matrix = matrix;
        boolean[][] canReachP = new boolean[m][n];
        boolean[][] canReachA = new boolean[m][n];
        for (int i = 0; i < n; i++) {
            dfs(0, i, canReachP);
            dfs(m - 1, i, canReachA);
        }
        for (int i = 0; i < m; i++) {
            dfs(i, 0, canReachP);
            dfs(i, n - 1, canReachA);
        }
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(canReachA[i][j] && canReachP[i][j]){
                    List<Integer> temp = new ArrayList<>();
                    temp.add(i);
                    temp.add(j);
                    res.add(temp);
                }
            }
        }
        return res;
    }
    /**
     * ��һ��˼·���ӱ߽��������ߣ�ֻ���ߵ����Լ����߻��ߵȸߵĵط����߽����ߵ��ĵط��������������Ӧ����ĵط���
     */
    private void dfs(int x, int y, boolean[][] canReach) {
        canReach[x][y] = true;
        for (int i = 0; i < 4; i++) {
            int newX = x + dires[i][0];
            int newY = y + dires[i][1];
            if (isIn(newX, newY) && matrix[x][y] <= matrix[newX][newY] && !canReach[newX][newY]) {
                dfs(newX, newY, canReach);
            }
        }
    }

    private boolean isIn(int x, int y) {
        return x >= 0 && x < m && y >= 0 && y < n;
    }
}
```
˼·������
* ��άƽ���ϵ����������ĸ�����������ߣ�������������Ŀһ�����̶���д����
    * ��ʾ�ĸ����������`int[][] dires = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};`
    * ��ʾ��άƽ�������������`int m, n;`
    * �ж�ĳ������`x,y`�Ƿ��ھ��������ڵĸ�������`boolean isIn(int x, int y)`
* Ҫͬʱ������Ե����������̫ƽ������һ������Ҫ��������·�������ߣ�һ����̫ƽ��ΪĿ�꣬һ���Դ�����ΪĿ�ꡣ���ڲ��ĵ��Ա߽�ΪĿ��ȥ����·�����߱Ƚ��鷳�����������һ��˼·���ӱ�Ե�������ߡ���������[130. ��Χ�Ƶ�����](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/BackTracking/solve130.md)�ĵڶ��ֽⷨ��
* �ӱ�Ե�����߾��޸�ͨ�й���Ҫ���߶ȱȵ�ǰ��߻�����ȵĵ��ߡ�
* ���庯��`dfs(int x, int y, boolean[][] canReach)`���������������������/̫ƽ�����ڵĵ���Է��ʵ��ĵ㣬��Щ��Ҳ���ǿ���������Ӧ����ĵ㡣
    * ���Ƚ�`canReach[x][y] = true;`������ǰ������Ϊ�ѷ��ʡ�
    * Ȼ������������ĸ�����ĵ���б�����������㣺�ھ�����`isIn(newX, newY)`���߶ȱȵ�ǰ����߻������`matrix[x][y] <= matrix[newX][newY]`�һ�û�з��ʹ����Ͷ�����ʡ�
* �������У����Ƚ�������Ա������ʼ����Ȼ�����ɱ�ʾ������/̫ƽ�����״̬��` boolean[][] canReachP/canReachA = new boolean[m][n];`��Ȼ����ھ��ε��������������߽�ĵ�ֱ����`dfs()`�����дӴ�����/̫ƽ���ڲ��ķ��ʡ�
* ���Զ�άƽ���ڵ����е���б������ҵ�`canReachA[i][j] && canReachP[i][j]`�ĵ㣬���ǿ���ͬʱ������������
* ʱ�临�Ӷ�Ϊ$O(n)$����Ϊֻ��ÿһ���������������α�����n��ʾ�����ĸ������ռ临�Ӷȳ�ȥ�ݹ����ռ�õĿռ�Ϊ$O(n)$��

���н����

* ִ����ʱ :6 ms, ������ Java �ύ�л�����80.11%���û�
* �ڴ����� :43.1 MB, ������ Java �ύ�л�����22.92%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз