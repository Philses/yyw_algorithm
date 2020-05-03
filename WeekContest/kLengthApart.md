# 5401. �Ƿ����� 1 ��������� k ��Ԫ��
### ԭ��
����һ�������� 0 �� 1 ��ɵ����� nums �Լ����� k��������� 1 ��������� k ��Ԫ�أ��򷵻� True �����򣬷��� False �� 

ʾ�� 1��
���룺nums = [1,0,0,0,1,0,0,1], k = 2
�����true
���ͣ�ÿ�� 1 ��������� 2 ��Ԫ�ء�

ʾ�� 2��
���룺nums = [1,0,0,1,0,1], k = 2
�����false
���ͣ��ڶ��� 1 �͵����� 1 ֮��ֻ���� 1 ��Ԫ�ء�

ʾ�� 3��
���룺nums = [1,1,1,1,1], k = 0
�����true

ʾ�� 4��
���룺nums = [0,1,0,1], k = 1
�����true

��ʾ��
1 <= nums.length <= 10^5
0 <= k <= nums.length
nums[i] ��ֵΪ 0 �� 1

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/check-if-all-1s-are-at-least-length-k-places-away)��https://leetcode-cn.com/problems/check-if-all-1s-are-at-least-length-k-places-away

### �ⷨ
```java
public class kLengthApart {
    public boolean kLengthApart(int[] nums, int k) {
        for (int pre = -100000, next = 0; next < nums.length; next++) {
            if (nums[next] == 1) {
                if (next - pre <= k)
                    return false;
                pre = next;
            }
        }
        return true;
    }
}
```
˼·������
* ����ÿһ��1���������������1�ļ����ڵ���k����֤�����е�1�ļ����ڵ���k������ֻҪ˳��ȥ����1��Ȼ������1�ļ������жϼ��ɡ�ֻҪ������������������ڵ�1���С��k�Ͳ��������⡣
* ��Ҫ�����������ڵ�1�ļ�࣬��Ҫ֪��������1�������Ƕ��٣�����ʹ��˫ָ��`pre, next`�ֱ��ʾһǰһ��������������
* ͨ������ѭ��������ȥ����һ��1��
    * ����ʼ`pre = -100000, next = 0`����Ϊ��һ��1�����û��0��������Ҫ�ж��жϼ�࣬���ǰ�����������߼���������࣬�Ǿͱ�֤������ļ��һ������k�ͺ��ˡ����鳤���Ϊ10000����`pre = -100000`���ܱ�֤��
    * ���`nums[next] == 1`���ҵ�����һ��1����ʱ����1֮��ļ��Ϊ`next - pre + 1`�����С��`k`Ҳ����`next - pre <= k`������`false`��Ȼ��Ҫ������һ������1���жϣ���`pre = next`��ѭ��`next++`�����Ǵ�`pre + 1`����ȥ����һ��1��
    * ��������ƶ�`next`��
* ʱ�临�Ӷ�Ϊ$O(n)$���ռ临�Ӷ�Ϊ$O(1)$��

����һ����ֱ�۵Ĵ��루û�б������𣩣�

```java
class Solution {
    public boolean kLengthApart(int[] nums, int k) {
        int pre = 0, next;
        int n = nums.length;
        for(; pre < n; pre ++){
            if(nums[pre] == 1){
                break;
            }
        }
        for(next = pre + 1; next < n; next++){
            if(nums[next] == 1){
                if(next - pre <= k)
                    return false;
                pre = next;
            }
        }
        return true;
    }
}
```

���н����

* 1ms

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз