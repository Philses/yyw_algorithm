# ������04. ��ά�����еĲ���

### ԭ��
��дһ����Ч���㷨������ m x n ���� matrix �е�һ��Ŀ��ֵ target���þ�������������ԣ�
ÿ�е�Ԫ�ش������������С�
ÿ�е�Ԫ�ش��ϵ����������С�

ʾ��:
���о��� matrix ���£�
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
���� target = 5������ true��
���� target = 20������ false��

**ע�⣺**��������վ 240 ����ͬ��https://leetcode-cn.com/problems/search-a-2d-matrix-ii/

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)��https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/

### 3�ֽⷨ

�����Ž�ֱ�ӿ������ֽⷨ��

##### 1.����ʹ�ö��ֲ���
```java
public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
            return false;
        for (int i = 0; i < matrix.length; i++) {
            if (matrix[i][0] > target)
                return false;
            if (Arrays.binarySearch(matrix[i], target) >= 0)
                return true;
        }
        return false;
    }
```
˼·������
* Ҫ���Ҿ������Ƿ����ĳ��Ԫ�أ����ұ�ʾ����ÿһ�е����鶼������ģ����Զ�ÿһ�н��ж��ֲ��ң����ÿһ�ж�û�в��ҵ�������ͷ���`false`��
    * ʹ��java�⺯��`Arrays.binarySearch(matrix[i], target)`������ֵ�Ǹ�˵�����ҵ�`target`��
* ����Ҫ����һЩ���������
    * �����ľ���Ϊ`null`���߸����ľ��󲻴����κ�Ԫ��`matrix.length == 0 || matrix[0].length == 0`���϶��Ҳ���Ŀ��Ԫ�أ�ֱ�ӷ��ء�
    * �����ÿһ��Ҳ�Ǵ�С�������еģ������ڶ�ÿһ�н��ж��ֲ��ҵ�ѭ���ǣ����`matrix[i][0] > target`����һ�п϶�û��ָ��Ԫ�أ��������ÿһ�е�����Ԫ�ض�����`matrix[i][0]`Ҳһ���Ҳ���ָ��Ԫ�أ����Կ���ֱ�ӷ���`false`��
* ʱ�临�Ӷ�Ϊ$O(mlog(n))$���ռ临�Ӷ�Ϊ$O(1)$��

���н����
* ִ����ʱ :9 ms, ������ Java �ύ�л�����35.30%���û�
* �ڴ����� :49.6 MB, ������ Java �ύ�л�����5.03%���û�

##### 2.����ݹ�
```java
public boolean searchMatrix2(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0)
            return false;
        return search(matrix, target, 0, matrix[0].length - 1, 0, matrix.length - 1);
    }

    private boolean search(int[][] matrix, int target, int left, int right, int top, int bottom) {
        if (left > right || top > bottom) // ���޵�������
            return false;
        if (target < matrix[top][left] || target > matrix[bottom][right]) // Ŀ��ֵ�Ⱦ�������Ͻ�С���߱Ⱦ������С�Ǵ󣬿϶��޷������ھ������ҵ���ֵ
            return false;
        int mid = (left + right) / 2;
        int row = top;
        while (row <= bottom && matrix[row][mid] <= target) { // �����м����Ƿ����ҵ�target������Ҳ�����ʹrowͣ�ڸ����м�Ԫ�ر�target���λ��
            if (matrix[row][mid] == target)
                return true;
            row++;
        }
        return search(matrix, target, left, mid - 1, row, bottom) ||
                search(matrix, target, mid + 1, right, top, row - 1);
    }
```
˼·������
* ���ݾ����Ԫ�ص����й��ɣ����Ͻǵ�Ԫ��������������С��Ԫ�أ�������Ԫ�ش���`target`����ô���������һ��û��`target`�����½ǵ�Ԫ����������������Ԫ�أ�������Ԫ��С��`target`����ô���������һ��û��`target`��
* ������һ�����ۣ����`matrix[i][j] > target`�����ұ�֤`martix[i - 1][j] < target`����
    * ���ȣ���`j`��û��Ԫ�ص���`taget`��
    * ������`matrix[i - 1][j]`Ϊ���½ǵľ��������в�����`target`����`matrix[i][j]`Ϊ���Ͻǵľ�������Ҳ������`target`�����Կ��ܴ���`target`�������ֻ����`matrix[i][j - 1]`Ϊ���Ͻǵľ������������`matrix[i - 1][j + 1]`Ϊ���½ǵľ�������
* �����������ۣ����Զ���ݹ�Ĳ��Һ���`boolean search(int[][] matrix, int target, int left, int right, int top, int bottom)`����ʾ�ھ�������`[top, bottom]x[left, right]`���Ƿ����`target`��
    * �ݹ������������:
        * �������򲻴���`left > right || top > bottom`
        * ���߾����������Ͻ�Ԫ�ش���`target`�������½ǵ�Ԫ��С��`target`��`target < matrix[top][left] || target > matrix[bottom][right]`
    * �ö��ֵ��뷨����ѭ��ȥ�ж�`mid = (left + right) / 2`��һ���Ƿ����`target`��`while (row <= bottom && matrix[row][mid] <= target)`���ѭ��������ʹ��������Ҳ��ɹ���`row`��ֵ��������`matrix[row][j] > target`�����ұ�֤`martix[row - 1][j] < target`
    * ���ǾͿ��԰���֮ǰ˵�Ŀ��ܴ��ڵ�˼·���ݹ�ؽ��в��ң�����`search(matrix, target, left, mid - 1, row, bottom) ||search(matrix, target, mid + 1, right, top, row - 1);`
* �����������жϣ������Ƿ���ڻ����Ƿ���Ԫ�أ�Ȼ����õݹ麯����
* ʱ�临�Ӷ�Ϊ$O(mlog(n))$���ռ临�ӶȾ��Ǻ�������ջռ�õĿռ䡣

���н����
* ִ����ʱ :9 ms, ������ Java �ύ�л�����35.30%���û�
* �ڴ����� :50.8 MB, ������ Java �ύ�л�����5.03%���û�

##### 3.�̶���������
```java
public boolean searchMatrix3(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
            return false;
        int x = matrix[0].length - 1, y = 0;
        while(y < matrix.length && x >= 0){
            if(matrix[y][x] < target)
                y++;
            else if (matrix[y][x] > target)
                x--;
            else return true;
        }
        return false;
    }
```
˼·������
* �̶��������ߣ�������þ���������ԡ���������Ŀ[378. ��������е�KС��Ԫ��](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/ArrayAndMatrix/kthSmallest.md)�еĽⷨ2��
* �ھ��������ߣ����ݵ�ǰԪ�صĴ�Сѡ�����߷���
    * �������ѡ�����Ͻ�Ϊ��㣬��ô��`matrix[y][x] < target`ʱ��Ҫȥ����һ�������Ԫ����`target`�Ƚϣ����º����Ҷ��п��ܣ���֪�����ı��ߡ�ͬ�������½�Ϊ���Ҳ����ȷ�����߷���
    * ѡ������Ͻǿ�ʼ�����`matrix[y][x] < target`��ȥ����һ�������Ԫ�أ���ֻ�������ߡ���֮Ҫȥ�ұȵ�ǰ��С��Ԫ�أ���ѡ�������ߡ���ѡ������½ǿ�ʼҲ�ǿ��еģ�
    * ��������߹����������Ԫ�أ��ͷ���`true`��������곬�����η�Χ��˵��û���ҵ�������`false`��
* ����ͼ�۲������������߹��̣�

![searchMatrixͼʾ.png](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/ArrayAndMatrix/searchMatrix%E5%9B%BE%E7%A4%BA.png?raw=true)

* �����Ͻǳ��ǣ��������η�Χ��ֹͣѭ����ѭ������Ϊ`y < matrix.length && x >= 0`��Ȼ�󷵻�`false`�������߾���������`y++`�������߾���������`x--`��
* �������m+n�ξͻᳬ������Χ�������ҵ���Ŀ�꣬����ʱ�临�Ӷ�Ϊ$O(m + n)$���ռ临�Ӷ�Ϊ$O(1)$��

���н����
* ִ����ʱ :7 ms, ������ Java �ύ�л�����86.14%���û�
* �ڴ����� :50.5 MB, ������ Java �ύ�л�����5.03%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз