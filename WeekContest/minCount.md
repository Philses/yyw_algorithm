# LCP 06. ��Ӳ��
### ԭ��
������ n �����۱ң�ÿ�ѵ��������������� coins �С�����ÿ�ο���ѡ������һ�ѣ��������е�һö������ö���������������۱ҵ����ٴ�����

ʾ�� 1��
���룺[4,2,1]
�����4
���ͣ���һ�����۱�������Ҫ�� 2 �Σ��ڶ���������Ҫ�� 1 �Σ�������������Ҫ�� 1 �Σ��ܹ� 4 �μ������ꡣ

ʾ�� 2��
���룺[2,3,10]
�����8

���ƣ�
1 <= n <= 4
1 <= coins[i] <= 10

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/na-ying-bi)��https://leetcode-cn.com/problems/na-ying-bi

### �ⷨ
```java
public int minCount(int[] coins) {
        int res = 0;
        for(int i : coins)
            res += count(i);
        return res;
    }

    private int count(int num){
        int count = 0;
        while(num > 0){
            num -= 2;
            count++;
        }
        return count;
    }
```
˼·������
* ÿ������2������1���ң�Ҫ�õ����ٻ�ȡ������ÿ�ζ���2���Ҽ��ɣ�ֻʣ1��ʱҲ��װ��2����Ȼ��ʣ��-1��Ӳ�Ҽ��ɣ���
* ����ÿһ��Ӳ�ң���Ҫȡ�����ٴ���ʹ�ø�������`int count(int num)`���㣬ÿ��������Ӳ�ң�ֻҪʣ��Ӳ��������0��һֱȡ��
* ���ս�����Ǳ���ÿһ��Ӳ�ң���ÿһ��Ӳ�ҵĻ�ȡ���ۼӡ�

���н����

* 0ms

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз