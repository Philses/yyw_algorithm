# ������05. �滻�ո�
### ԭ��
��ʵ��һ�����������ַ��� s �е�ÿ���ո��滻��"%20"��

ʾ�� 1��
���룺s = "We are happy."
�����"We%20are%20happy."

���ƣ�
0 <= s �ĳ��� <= 10000

��Դ�����ۣ�LeetCode��
���ӣ�https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof
����Ȩ������������С���ҵת������ϵ�ٷ���Ȩ������ҵת����ע��������

### �ⷨ
```java
class Solution {
    public String replaceSpace(String s) {
        StringBuilder res = new StringBuilder();
        for(char c : s.toCharArray()){
            if(c == ' ')
                res.append("%20");
            else 
                res.append(c);
        }
        return res.toString();
    }
}
```
˼·������
* ���ַ������ַ����б�������������ո��ַ������滻Ϊ`"%20"`������ʹ��`StringBuilder res`�������ַ�����ƴ��Ƶ�������µĶ���

���н����

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз