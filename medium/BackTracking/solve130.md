# 130. ��Χ�Ƶ�����
### ԭ��
����һ����ά�ľ��󣬰��� 'X' �� 'O'����ĸ O����
�ҵ����б� 'X' Χ�Ƶ����򣬲�����Щ���������е� 'O' �� 'X' ��䡣

ʾ��:

X X X X
X O O X
X X O X
X O X X
������ĺ����󣬾����Ϊ��

X X X X
X X X X
X X X X
X O X X
����:

��Χ�Ƶ����䲻������ڱ߽��ϣ����仰˵���κα߽��ϵ� 'O' �����ᱻ���Ϊ 'X'�� �κβ��ڱ߽��ϣ�����߽��ϵ� 'O' ������ 'O' ���ն��ᱻ���Ϊ 'X'���������Ԫ����ˮƽ��ֱ�������ڣ���������ǡ��������ġ�

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/surrounded-regions)��https://leetcode-cn.com/problems/surrounded-regions

### 2�ֽⷨ
##### 1.����˼ά��ȥ�ұ�XΧ�Ƶ�����
```java
	private int[][] direction = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    private Queue<Integer> pos = null;
    private boolean flag;
    private int row, col;
    private boolean[][] visited;
    public void solve(char[][] board) {
        if (board.length == 0 || board[0].length == 0)
            return;
        row = board.length;
        col = board[0].length;
        pos = new LinkedList<>();
        visited = new boolean[row][col];
        for (int i = 0; i < row; i++)
            for (int j = 0; j < col; j++) {
                if (!visited[i][j] && board[i][j] == 'O') {
                    flag = false;
                    searchO(board, i, j);
                    if (flag)
                        pos.clear();
                    else {
                        while (!pos.isEmpty())
                            board[pos.remove()][pos.remove()] = 'X';
                    }
                }
            }
    }

    private void searchO(char[][] board, int x, int y) {
        visited[x][y] = true;
        pos.add(x);
        pos.add(y);
        flag = flag || isEdge(x, y);
        for (int i = 0; i < 4; i++) {
            int newX = x + direction[i][0];
            int newY = y + direction[i][1];
            if (inArea(newX, newY) && !visited[newX][newY] && board[newX][newY] == 'O')
                searchO(board, newX, newY);
        }
    }

    private boolean inArea(int x, int y) {
        return x >= 0 && x < row && y >= 0 && y < col;
    }

    private boolean isEdge(int x, int y) {
        return x == 0 || y == 0 || x == row - 1 || y == col - 1;
    }
```
˼·������
* �������Ŀ�ĽǶȳ���������ֱ��ȥ�ұ�X��Χ��O��Ȼ������ΪX��
* ��ĳһ��ΪO�ĵ㿪ʼ������ȥ������һ��O�Ƿ�X��Χ��ʹ��dfs����������Ϊ`private void searchO(char[][] board, int x, int y)`
    * �����ڲ��ҹ����в�����ֱ�ӽ�O��ΪX����Ϊ��һƬ���Ի����ӵ��߽硣������Ҫ�Ƚ�������������������ɺ��ٸ����Ƿ�X��Χ��ȷ��Ҫ��Ҫ��ΪX��`pos.add(x);, pos.add(y);`����ʹ���˳�Ա����`Queue<Integer> pos`
    * ʹ�ó�Ա����`visited[x][y]`��ʾ��`x,y`�Ƿ񱻷��ʹ������Ե��ÿ�ʼʱ��`visited[x][y] = true;`��
    * �ڲ��ҹ�����Ҫ��ע��һƬ���Ƿ����ӵ��߽磬ʹ�ó�Ա����`boolean flag`��ʾ������ÿһ���㶼���и���`flag = flag || isEdge(x, y);`����������`boolean isEdge(int x, int y)`�ж�ĳ�����Ƿ�Ϊ�߽��ϵĵ㣬�߼� �� ��֤��һ�����ھ���߽�����һ��ĵ㶼���������߽�ġ�
    * Ȼ����Ƕ�άƽ�����������ĸ�����ȥ�����ĳ��������ˣ�Ҫ������һ���������Ҫ���㣺�ھ���Χ�ڣ�û�з��ʹ����Ҹõ���O��`inArea(newX, newY) && !visited[newX][newY] && board[newX][newY] == 'O'`
* ���������У���ʼ����Ա�����󣬾ͱ���ÿһ���㣬���û�з�Χ������O����ʼdfs��
    * ����Ҫ����ʾ�ÿ��Ƿ����ӵ��߽�ı�ʶ`flag = false`��
    * ����`searchO(board, i, j);`�����`flag == true`��ֱ����ն����е����꣬��Ϊ�������ӵ��߽�û�б�X��Χ������ÿ�ε���x��y���꣬����ת��` board[pos.remove()][pos.remove()] = 'X';`ֱ������Ϊ�ա�

���н����
* ִ����ʱ :10 ms, ������ Java �ύ�л�����15.20%���û�
* �ڴ����� :50.4 MB, ������ Java �ύ�л�����5.03%���û�

##### 2.����˼ά��ȥ��û�б�XΧ�Ƶ�����
```java
	private int[][] direction = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};	
	private int row, col;
	private boolean[][] linkedEdge = null;
    public void solve2(char[][] board) {
        if(board.length == 0 || board[0].length == 0)
            return;
        row = board.length;
        col = board[0].length;
        linkedEdge = new boolean[row][col];
        for(int i = 0; i < row; i++){
            if(board[i][0] == 'O' && !linkedEdge[i][0])
                search2(board, i, 0);
            if(board[i][col - 1] == 'O' && !linkedEdge[i][col - 1])
                search2(board, i, col - 1);
        }
        for(int j = 1; j < col - 1; j++){
            if(board[0][j] == 'O' && !linkedEdge[0][j])
                search2(board, 0, j);
            if(board[row - 1][j] == 'O' && !linkedEdge[row - 1][j])
                search2(board, row - 1, j);
        }

        for(int i = 0; i < row; i++)
            for (int j = 0; j < col; j++)
                if(!linkedEdge[i][j])
                    board[i][j] = 'X';
    }

 	private boolean inArea(int x, int y){
        return x >= 0 && x < row && y >= 0 && y < col;
    }	

    private void search2(char[][] board, int x, int y){
        linkedEdge[x][y] = true;
        for(int i = 0; i < 4; i++){
            int newX = x + direction[i][0];
            int newY = y + direction[i][1];
            if(inArea(newX, newY) && !linkedEdge[newX][newY] && board[newX][newY] == 'O')
                search2(board, newX, newY);
        }
    }
```
˼·������
* �����ڷ���1������һ��˼·���ǣ��ӱ߽��O������ȥ�ҵ�������߽��O������O�������Щλ�á���ô������������ɺ�û�б���ǵĵط��������ֿ��ܣ�
    * ԭ������X
    * ԭ����O������û����߽��O��������ôҪ��ת��ΪX
    * ����ֻҪû�б�ǵĵط�������ΪX�Ϳ��ԡ�
* ���������Ǵӱ߽��O������ȥ������֮������O������`void search2(char[][] board, int x, int y)`.
    * ��Ա����`linkedEdge[x][y]`��ʾ�Ƿ���߽��ϵ�O������
    * ���Ƚ�`linkedEdge[x][y] = true;`��Ȼ�����������ĸ�����ȥ���ԡ�Ҫ������һ���������Ҫ���㣺�ھ���Χ�ڣ�û�з��ʹ����Ҹõ���O����������û�з��ʹ�������`!linkedEdge[newX][newY]`����ʶ����Ϊ���ʹ��Ķ�����߽�O������O��
* ��������
    * ��ʼ����Ա������
    * ���ǶԾ������������ĸ��ߣ��ҵ��߽��ϵ�O���һ�û�б����ʹ���`!linkedEdge[i][0]`����DFS��
    * Ȼ�����ÿһ���㣬���û�б���ǣ�ͳͳ��ΪX���ɡ�

���н����
* ִ����ʱ :2 ms, ������ Java �ύ�л�����97.69%���û�
* �ڴ����� :42.1 MB, ������ Java �ύ�л�����32.57%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз