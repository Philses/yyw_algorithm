# ������50. ��һ��ֻ����һ�ε��ַ�
### ԭ��
���ַ��� s ���ҳ���һ��ֻ����һ�ε��ַ������û�У�����һ�����ո�

ʾ��:

s = "abaccdeff"
���� "b"

s = "" 
���� " "


���ƣ�
0 <= s �ĳ��� <= 50000

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof)��https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof

### �ⷨ:ʹ����������ϣ�����
```java
public class firstUniqChar {
    public char firstUniqChar(String s) {
        int[] count = new int[256];
        char[] chars = s.toCharArray();
        for(char c : chars)
            count[c]++;
        for(char c : chars){
            if(count[c] == 1)
                return c;
        }
        return ' ';
    }
}
```
˼·������
* Ҫ��ֻ����һ�εĵ�һ���ַ�������Ҫȥ����ÿһ���ַ������˼��Ρ�һ�㶼���ù�ϣ�������ַ���������������չ��ASCII��Ҳ��256�����Ϳ���ʹ��`int[] count`�������ϣ���������ַ���Ӧ������ֵ���Ǹ��ַ����ֵĴ�����
* ��һ�α�������ÿ���ַ����ֵĴ���`for(char c : chars) count[c]++;`���ڶ��α�����˳��ȥ�鿴���ַ������˼��Σ�������ַ�������1�Σ������ǵ�һ��������һ�ε��ַ���ֱ�ӷ��ء�
* ����ڶ��α���û�з��أ���˵��û�н�����һ�ε��ַ�������`' '`��
* ʱ�临�Ӷ�Ϊ$O(n)$���ռ临�Ӷ�Ϊ$O(n)$����Ϊʹ���˸������ַ����飩��

���н����

* ִ����ʱ :4 ms, ������ Java �ύ�л�����99.92%���û�
* �ڴ����� :39.7 MB, ������ Java �ύ�л�����100.00%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз