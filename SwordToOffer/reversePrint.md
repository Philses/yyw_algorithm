# ������06. ��β��ͷ��ӡ����
### ԭ��
����һ�������ͷ�ڵ㣬��β��ͷ����������ÿ���ڵ��ֵ�������鷵�أ���

ʾ�� 1��
���룺head = [1,3,2]
�����[2,3,1]

���ƣ�
0 <= ������ <= 10000

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof)��https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof

### �ⷨ
```java
public class reversePrint {
    public int[] reversePrint(ListNode head) {
        if(head == null)
            return new int[0];
        List<Integer> temp = new ArrayList<>();
        while(head != null){
            temp.add(head.val);
            head = head.next;
        }
        int n = temp.size();
        int[] res =new int[n];
        for(int i = 0; i < n; i++){
            res[n - i - 1] = temp.get(i);
        }
        return res;
    }
}
```
˼·������
* Ҫ���ص����ݽṹ��һ�����飬����Ԫ��˳���������˳���෴��
* �������ǵ���Ҫ֪��Ԫ�ظ��������������飬����ⲻ�˵��ȱ���һ����������ʹ��ջ��Ž��ֵ��Ҳ����ʹ��List��Ž��ֵ������ֱ�Ӽ������������С�
* Ȼ���������飬������ʹ��List��������List��ͨ������������Ԫ�ط��ʣ�Ҫ�����������ӡ����ô������������Ϊ`n - i - 1`��Ԫ�ض�ӦList������Ϊ`i`��Ԫ�ء�����������ȷ����ʱ��پ�������־ͺ��ˣ�����List�е�2��Ԫ��i=1����ôҪ��������ĵ�����2��Ԫ��n- 1 - 1����
* ʱ�临�Ӷ���ռ临�Ӷȶ���$O(n)$��

���н����

* ִ����ʱ :2 ms, ������ Java �ύ�л�����59.23%���û�
* �ڴ����� :40.1 MB, ������ Java �ύ�л�����100.00%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз