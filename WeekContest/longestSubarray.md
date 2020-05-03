# 5402. ���Բ�������Ƶ������������
### ԭ��
����һ���������� `nums` ����һ����ʾ���Ƶ����� `limit`�����㷵�������������ĳ��ȣ����������е���������Ԫ��֮��ľ��Բ����С�ڻ��ߵ���` limit` ��
������������������������飬�򷵻� 0 ��

ʾ�� 1��
���룺nums = [8,2,4,7], limit = 4
�����2 
���ͣ��������������£�
[8] �����Բ� |8-8| = 0 <= 4.
[8,2] �����Բ� |8-2| = 6 > 4. 
[8,2,4] �����Բ� |8-2| = 6 > 4.
[8,2,4,7] �����Բ� |8-2| = 6 > 4.
[2] �����Բ� |2-2| = 0 <= 4.
[2,4] �����Բ� |2-4| = 2 <= 4.
[2,4,7] �����Բ� |2-7| = 5 > 4.
[4] �����Բ� |4-4| = 0 <= 4.
[4,7] �����Բ� |4-7| = 3 <= 4.
[7] �����Բ� |7-7| = 0 <= 4. 
��ˣ�����������������ĳ���Ϊ 2 ��

ʾ�� 2��
���룺nums = [10,1,2,4,7,2], limit = 5
�����4 
���ͣ������������������� [2,4,7,2]���������Բ� |2-7| = 5 <= 5 ��

ʾ�� 3��
���룺nums = [4,2,2,2,4,4,2,2], limit = 0
�����3

��ʾ��

```
1 <= nums.length <= 10^5
1 <= nums[i] <= 10^9
0 <= limit <= 10^9
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit)��https://leetcode-cn.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit

### �ⷨ
```java
public class longestSubarray {
    public int longestSubarray(int[] nums, int limit) {
        int n = nums.length;
        int res = 1, i = 0, j = 0;
        PriorityQueue<Integer> min = new PriorityQueue<>();
        PriorityQueue<Integer> max = new PriorityQueue<>(Collections.reverseOrder());
        while (j < n && i < n) {
            if(min.size() == 0){
                min.add(nums[j]);
                max.add(nums[j]);
                j++;
                continue;
            }
            if (Math.abs(min.peek() - nums[j]) <= limit && Math.abs(max.peek() - nums[j]) <= limit) {
                min.add(nums[j]);
                max.add(nums[j]);
                res = Math.max(res, j - i + 1);
                j++;
            }
            else {
                min.remove(nums[i]);
                max.remove(nums[i]);
                i++;
            }
        }
        return res;
    }
}
```
˼·������
* ������Ҫ���������ģ�Ҫ֪��������ĳ��ȣ�ֻ��Ҫ֪�������������Ԫ�ص����������ұ�Ԫ������`i, j`����ô�����鳤��Ϊ`j - i + 1`��
* ����������������Ԫ�صľ���ֵС�ڵ���`limit`��ֻ��Ҫ�������ڵ����ֵ����Сֵ֮�����㼴�ɱ�֤������Ԫ��֮������Ҫ������Ҫά���������е����Ԫ������СԪ�ء�
* emmm����֪����ν�����ô���뵽�������ڣ��������Ϊ�������������������ģ������������ÿһ��Ԫ�ص���Ϣ���ã�Ҫ֪������Ԫ��ֵ��֪����С�����ֵ�أ���ά�����Ԫ������СԪ�أ����Էֱ�ʹ�������С���ȶ��С�
* ��ʼ��`res = 1`����Ϊÿ������Ԫ�ض���������������Ϊ1��
* �ڴ��ڻ����Ĺ����У�
    * ���������Ԫ�ظ���Ϊ0��˵���������䳤��Ϊ0��Ҫ����ǰԪ��`nums[j]`�������������ȶ����У�Ȼ��`j++; continue`��
    * �����ǰԪ��������������С�����Ԫ�صľ���ֵ��С�ڵ���`limit`��`Math.abs(min.peek() - nums[j]) <= limit && Math.abs(max.peek() - nums[j]) <= limit`����ʱ���Ԫ�ؿ��Ա����������飬Ҫ�������������С���ֵ�ͽ�������������У�Ȼ����Ҫ����`res = Math.max(res, j - i + 1);`����󴰿���������1��`j++`��
    * �������Ԫ�ز��ܼ��������飬���������߽����ƶ�1�����Ƚ�Ԫ��`nums[i]`�Ӷ�����ɾ����`i++`��

���н����

* 43ms

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз