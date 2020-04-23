# 378. ��������е�KС��Ԫ��
### ԭ��
����һ�� n x n ��������ÿ�к�ÿ��Ԫ�ؾ������������ҵ������е�kС��Ԫ�ء�
��ע�⣬���������ĵ� k СԪ�أ������ǵ� k ����ͬ��Ԫ�ء� 

ʾ��:
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

���� 13��

��ʾ��
����Լ��� k ��ֵ��Զ����Ч��, 1 �� k �� n2 ��

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix)��https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix

### 2�ֽⷨ
##### 1.���ȶ��е�ʹ��
```java
public int kthSmallest(int[][] matrix, int k) {
        PriorityQueue<Integer> MaxPQ = new PriorityQueue<>(Collections.reverseOrder());
        for (int[] row : matrix) {
            for (int num : row) {
                if (MaxPQ.size() == k && num > MaxPQ.peek())
                    break;
                MaxPQ.add(num);
                if (MaxPQ.size() > k)
                    MaxPQ.remove();
            }
        }
        return MaxPQ.remove();
    }
```
˼·������
* Ҫ�ҵ�kС��Ԫ�أ�һ��������������ʹ�����ȶ��С�
    * �ҵ�kС��Ԫ�أ��ͱ���k����С��Ԫ�أ����������Ǹ����Ǵ𰸣����Կ���ʹ��������ȶ��С�
    * ���������е�Ԫ�أ���Ԫ����ӵ������У����������Ԫ����Ŀ`MaxPQ.size() > k`���ͽ��ѵ�����Ԫ�ص�����
    * ���������󵯳��Ѷ�Ԫ�أ�������С��k��Ԫ�������ģ�����kС��Ԫ�ء�
* ����������þ������������һ��С���Ż���
    * ����ڱ����Ĺ����У������е�Ԫ����Ŀ�Ѿ�Ϊk�ˣ��������ǰԪ�ش��ڶѶ�Ԫ�أ����Ԫ�ط�������л��ᱻ���������Ծ�û��Ҫ���롣
    * ���ұ�������ѭ���Ǵ�ĳһ�еĴ����ұ�������ǰԪ�ص��ұ�Ԫ�رȵ�ǰԪ�ظ���Ҳû��Ҫ������У����Ե�`MaxPQ.size() == k && num > MaxPQ.peek()`��ֱ�Ӵ����ѭ����������һ�еı�����
* ʱ�临�Ӷ�Ϊ$O(n^2log(k))$���ռ临�Ӷ�Ϊ$O(k)$��

���н����
* ִ����ʱ :21 ms, ������ Java �ύ�л�����34.35%���û�
* �ڴ����� :45.8  MB, ������ Java �ύ�л�����7.69%���û�

##### 2.���ַ�������
```java
public int kthSmallest2(int[][] matrix, int k) {
        int n = matrix.length - 1;
        int left = matrix[0][0], right = matrix[n][n];
        while(left < right){
            int mid = left + (right - left) / 2;
            int count = countNotMoreThanMid(matrix, mid, n);
            if(count < k)
                left = mid + 1;
            else
                right = mid;
        }
        return left;
    }

    private int countNotMoreThanMid(int[][] matrix, int mid, int n){
        int count = 0;
        int x = 0, y = n;
        while(x <= n && y >= 0){
            if(matrix[y][x] <= mid){
                count += y + 1;
                x++;
            }else{
                y--;
            }
        }
        return count;
    }
```
˼·������
* �ӷ���һ���������Կ������Ծ�������������ò����㣬����͵����˲������Ž⡣
* ��kС��������ζ��С�ڵ�������Ԫ��һ����k������������������n*n-k��������ĳ����Ϊ`mid`
    * ���С�ڵ���`mid`��Ԫ�ظ���С��k��˵��`mid`���ǵ�kС��������`mid`С�����͸����������ˡ����Ե�kС����������`mid + 1`��
    * ���С�ڵ���`mid`��Ԫ�ظ������ڵ���k��˵��`mid`����Ϊ��kС����������С����Ҳ�п����Ǵ𰸡�
* ����Ƕ��ַ���˼·���ٶ����ҵķ�ΧΪ`[left, right]`�����ȼ���`int mid = left + (right - left) / 2;`��Ȼ���ھ����м����ж��ٸ�Ԫ��С�ڵ���`mid`���������Ϊ`count`��
    * ���`count < k`����ô��kС��������Ϊ`mid + 1`������`left = mid + 1`��
    * ��֮��`right = mid`��
    * ѭ������������Ϊ`left >= right`����ʱ`left`��Ϊ�𰸡�
* �������������м����ж��ٸ�Ԫ��С�ڵ���`mid`���ο�����ͼʾ��˼·��
    * ![kthSmallestͼʾ.png](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/ArrayAndMatrix/kthSmallest%E5%9B%BE%E7%A4%BA.png?raw=true)
    * ��ɫ��ʾ`mid`����ɫ����Ǳ�ʾС�ڵ�������Ԫ�أ���ɫ��ͷ��ʾ�ڽ����ж�ʱ������ƶ�����
* ���ھ�����ϵ��µ����������ҵ��������帨������`int countNotMoreThanMid(int[][] matrix, int mid, int n)`��ͳ��С�ڵ���`mid`��Ԫ�ظ�����n��ʾ�������������`x,y`��ʾ��`mid`���бȽ�Ԫ�ص�����:
    * �����½ǿ�ʼ���ң����ɼ���һ��tip���������Բ�������Ԫ�ر�����
    * ���`matrix[y][x] <= mid`����ô������Ϊx��������С��y��Ԫ�ؿ϶�����`mid`С������`matrix[y][x]`һ����`y + 1`����`matrix[y - 1][x]`�Ѿ��жϱ�`mid`С��������һ��ֱ��ȥ�ж�`matrix[y][x + 1]`������`x++`
    * ���򣬻���ȷ��`matrix[y][x]`��Ҫ�����ж�`y--`��
    * ѭ�������������ǵ�Ҫ�жϵ�Ԫ������Խ������߽�`x <= n && y >= 0`
    * ��ѭ��������仯·�����֣���������ͳ��ʱ���������Ǵ����½��ߵ����Ͻǣ�ֻ��Ҫ�Ա�2*n��Ԫ�ش�С��
* ������������ɶ��ֲ��ҡ����ֲ��ҵĴ���Ϊ$log(max - min)$������max��min��ʾ����������СԪ�ص�ֵ��ÿ�β��ҷ������飨���бȽϣ�2*n�Σ�����ʱ�临�Ӷ�Ϊ$2nlog(max - min)$���ռ临�Ӷ�Ϊ$O(1)$��

���н����
* ִ����ʱ :0 ms, ������ Java �ύ�л�����100.00%���û�
* �ڴ����� :45.4 MB, ������ Java �ύ�л�����7.69%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз