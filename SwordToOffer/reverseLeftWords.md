# ������58 - II. ����ת�ַ���
### ԭ��
�ַ���������ת�����ǰ��ַ���ǰ������ɸ��ַ�ת�Ƶ��ַ�����β�����붨��һ������ʵ���ַ�������ת�����Ĺ��ܡ����磬�����ַ���`"abcdefg"`������2���ú�������������ת��λ�õ��Ľ��`"cdefgab"`��

ʾ�� 1��
����: s =` "abcdefg"`, k = 2
���: `"cdefgab"`

ʾ�� 2��
����: s =` "lrloseumgh"`, k = 6
���: `"umghlrlose"`

���ƣ�
`1 <= k < s.length <= 10000`

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof)��https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof

### �ⷨ
```java
public class reverseLeftWords {
    public String reverseLeftWords(String s, int n) {
        return s.substring(n + 1) + s.substring(0, n + 1);
    }
}
```
˼·������
* �۲�ʾ�������־���ͨ��n��ǰn���ַ���ͷ��ȡ֮��ŵ�ԭ�ַ���ĩβ��
* ����java��String��`substring()`�Ϳ��Խ������ʹ�����API���޷����Ƿ�����ѭ�����Ƚ���һ��������ַ��ŵ�`StringBuilder`ʵ���У��ٽ�ǰһ��������ַ����뼴�ɡ�

���н����

* ִ����ʱ :0 ms, ������ Java �ύ�л�����100.00%���û�
* �ڴ����� :39.7 MB, ������ Java �ύ�л�����100.00%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз