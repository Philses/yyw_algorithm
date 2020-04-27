# 79. ��������
### ԭ��
����һ����ά�����һ�����ʣ��ҳ��õ����Ƿ�����������С�
���ʱ��밴����ĸ˳��ͨ�����ڵĵ�Ԫ���ڵ���ĸ���ɣ����С����ڡ���Ԫ������Щˮƽ���ڻ�ֱ���ڵĵ�Ԫ��ͬһ����Ԫ���ڵ���ĸ�������ظ�ʹ�á�

ʾ��:
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
���� word = "ABCCED", ���� true
���� word = "SEE", ���� true
���� word = "ABCB", ���� false


��ʾ��

```
board �� word ��ֻ������д��СдӢ����ĸ��
1 <= board.length <= 200
1 <= board[i].length <= 200
1 <= word.length <= 10^3
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/word-search)��https://leetcode-cn.com/problems/word-search

### �ⷨ
```java
public class exist {
    private static int[][] dires = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private int row, col;
    private boolean hasFind;
    private boolean[][] visited;
    public boolean exist(char[][] board, String word) {
        row = board.length;
        col = board[0].length;
        hasFind = false;
        if(row * col < word.length())
            return false;
        visited = new boolean[row][col];
        char[] chars = word.toCharArray();
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(board[i][j] == chars[0]){
                    backTrack(board, chars, 1, i, j);
                    if(hasFind)
                        return true;
                }
            }
        }
        return false;
    }

    private void backTrack(char[][] board, char[] word, int curIndex, int x, int y){
        if(hasFind)
            return;
        if(curIndex == word.length){
            hasFind = true;
            return;
        }
        visited[x][y] = true;
        for(int[] dire : dires){
            int newX = x + dire[0], newY = y + dire[1];
            if(isIn(newX, newY) && !visited[newX][newY] && board[newX][newY] == word[curIndex])
                backTrack(board, word, curIndex + 1, newX, newY);
        }
        visited[x][y] = false;
    }

    private boolean isIn(int x, int y){
        return x >= 0 && x < row && y >= 0 && y < col;
    }
}
```
˼·������
* ����һ����Ŀ���Ǵ�ĳ�����ӿ�ʼ���ߣ�ֻ�������������ĸ����򣬲����Ѿ��߹��ĸ��Ӳ������߽�ȥ��Ҫ�ж��Ƿ����߳�һ����˳���·�����պ���ĸ�����˸������ַ���`word`��
* ��άƽ����ÿ��λ���൱�ڶ����ĸ���·�����ĳ��·���������������ĸ������޷��ҵ�`word`����һ����Ӧ���ַ�����ô����߷����ԣ����ǲ���Ҫ��ͷ���ߡ�������Ѱ��`abcde`��ʱ�����£�
    * ��a���������ߵ���һ�е����е�dʱ�������ұ����±߶�����e������Խ�磬����Ѿ��߹�������ȥ��������·�����ԡ�
    * ����û��Ҫ��ͷ��ʼ�ң�ֻ��Ҫ�۷���c��Ȼ�������߼��ɡ���������ȻӦ��ʹ�û��ݡ�

```
a b c d d
h e d f f
```

* ���ڳ�Ա������˵����Ϊ�˱�����ݺ����д����鷳����
    * ��Ŀ��˵ͬһ����Ԫ���ڵ���ĸ�������ظ�ʹ�ã�������Ҫʹ��`boolean[][] visited`����ʾĳһ�����괦����ĸ��û�б�ʹ�á�
    * ��ά������ʹ�õ����꣬��Ҫ��ֹԽ�磬��������Ҳ��Ҫ֪����ά���ӵ�����`int row, col;`
    * ����Ϊ�˷����ʾ���������ĸ���������ʹ��`static int[][] dires = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};`����������������
    * ��α�ʾ�ڶ�ά�������ҵ���`word`�����ǿ�����`hasFind`����ʾ�Ƿ��ҵ���
* ��ά������ʹ�õ����꣬��Ҫ��ֹԽ�磬����Ҫ��������`boolean isIn(int x, int y)`�ж�`x, y`�����Ƿ��������ڡ�
* Ȼ�����������ݺ���`void backTrack(char[][] board, char[] word, int curIndex, int x, int y)`��
    * ������������ʾ**��һ��**Ҫ��`word`������Ϊ`curIndex`���ַ������ĵ���������ֱ��ʾ��ǰ�������ꡣ
    * ���`curIndex == word.length`���ʹ����������ַ����Ѿ���˳���ҵ�����ʱ�ͽ�`hasFind`����Ϊtrue�����ҷ��ء�
    * ���⣬���û��ݺ���ʱ�����`hasFind`Ϊ�棬˵���Ѿ��Ѿ��ҵ��˸õ����������У��Ͳ���Ҫ�ڱ��·�����в��ң�ֱ�ӷ��ء�
    * ���ݺ�������:
        * �����������ڷ��ʵ��ַ��Ѿ���ʹ�ã���`visited[x][y] = true;`��
        * Ȼ����������ҵ���һ������������������`isIn(newX, newY)`������û��ʹ�ù�����ĸ`!visited[newX][newY]`��������һ�������Ӧ����Ļ��`word`�ж�Ӧ��������ĸ`board[newX][newY] == word[curIndex]`�Ľ��еݹ�`backTrack(board, word, curIndex + 1, newX, newY);`��
        * ����ʱ��Ҳ�����۷�·��ʱ������ǰ����Ҫ���ˣ����Իָ�û��ʹ��״̬`visited[x][y] = false;`
* ���������У�
    * ���ȸ������Ա������ֵ��
    * Ȼ���ж���������������û��Ҫ�ҵ��ַ�����`row * col < word.length()`����ֱ�ӷ���`false`��
    * ����·�����Դ�����������һ��`chars[0]`��ʼ��������Ҫһ������ѭ�����������Կ��ܵ�·����㣬Ȼ�����`backTrack(board, chars, 1, i, j);`ע�����������������1����Ϊ�Ѿ��ҵ���ͷ��һ����ĸ����һ��Ҫ�ҵľ�������Ϊ1����ĸ����Ȼ�����ĳһ������Ѿ����������ҵ���`word`����ֱ�ӷ��ء�`if(hasFind) return true`
* ������û���ڱ����з��أ�˵��ÿһ��·���ĳ��Զ�ʧ���ˣ��ͷ���`false`��

���н����

  * ִ����ʱ :6 ms, ������ Java �ύ�л�����83.83%���û�
  * �ڴ����� :41.3 MB, ������ Java �ύ�л�����100.00%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз