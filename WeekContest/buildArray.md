# 5404. ��ջ������������
### ԭ��
����һ��Ŀ������ target ��һ������ n��ÿ�ε�������Ҫ��  list = {1,2,3..., n} �������ȡһ�����֡�
��ʹ����������������Ŀ������ target ��
Push���� list �ж�ȡһ����Ԫ�أ� ���������������С�
Pop��ɾ�������е����һ��Ԫ�ء�
���Ŀ�����鹹����ɣ���ֹͣ��ȡ����Ԫ�ء�
��Ŀ���ݱ�֤Ŀ�������ϸ����������ֻ���� 1 �� n ֮������֡�
�뷵�ع���Ŀ���������õĲ������С�
��Ŀ���ݱ�֤����Ψһ�ġ�

ʾ�� 1��
���룺target = [1,3], n = 3
�����["Push","Push","Pop","Push"]
���ͣ� 
��ȡ 1 ���Զ��������� -> [1]
��ȡ 2 ���Զ��������飬Ȼ��ɾ���� -> [1]
��ȡ 3 ���Զ��������� -> [1,3]

ʾ�� 2��
���룺target = [1,2,3], n = 3
�����["Push","Push","Push"]

ʾ�� 3��
���룺target = [1,2], n = 4
�����["Push","Push"]
���ͣ�ֻ��Ҫ��ȡǰ 2 �����־Ϳ���ֹͣ��

ʾ�� 4��
���룺target = [2,3,4], n = 4
�����["Push","Pop","Push","Push","Push"]

��ʾ��

```
1 <= target.length <= 100
1 <= target[i] <= 100
1 <= n <= 100
target ���ϸ������
```

��Դ�����ۣ�LeetCode��
���ӣ�https://leetcode-cn.com/problems/build-an-array-with-stack-operations

### �ⷨ
```java
public class buildArray {
    public List<String> buildArray(int[] target, int n) {
        List<String> res = new ArrayList<>();
        int pre = 0;
        for(int i = 0; i < target.length; i++){
            for(int j = pre + 1; j < target[i]; j++){
                res.add("Push");
                res.add("Pop");
            }
            res.add("Push");
            pre = target[i];
        }
        return res;
    }
}
```
˼·������
* `target`��һ���������С����`target[i]`���ڵ�ǰ����`j`����ô������Ž�ȥ֮��Ӧ�õ�����ֱ����ǰ����`j == target[i]`���Ž���ǰ���Ž�ȥ���������͸ÿ���`target[i + 1]`������`target[i + 1] > target[i]`����ô��һ�����ܱ����벢�ұ�������Ӧ�ô�`target[i] + 1`��ʼ��Ȼ���ظ��������衣
* ��ѭ��`for(int i = 0; i < target.length; i++)`���ǹ���Ŀ�����飬��ѭ��`for(int j = pre + 1; j < target[i]; j++)`
    * ��`pre + 1`��ʼ���ԣ���һ����ѭ��ʱ��Ҫ����`target[0]`��Ҫ������1��ʼ������������ѭ���ⲿ��ʼ��`int pre = 0`��
    * ��ѭ����`j < target[i]`�����Բ��Ϸ����ٵ�����
    * ��ѭ��ֹͣʱ������`j = target[i]`ʱ����ʱҪ`res.add("Push");`��Ȼ�����`pre = target[i];`��������һ�βŴ�`target[i] + 1`��ʼ���ԡ�
* ��Ȼ������ѭ��������`target[i]`���Ϊn�����Ե�����Ҳ���Ǵ�1��n������ʱ�临�Ӷ�Ϊ$O(n)$��

���н����

* 0ms

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз