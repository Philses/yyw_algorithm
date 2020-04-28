# 22. ��������
### ԭ��
���� n �����������ŵĶ������������һ�������������ܹ��������п��ܵĲ��� ��Ч�� ������ϡ�

ʾ����
���룺n = 3
�����

```
	[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/generate-parentheses)��https://leetcode-cn.com/problems/generate-parentheses

### �ⷨ
```java
public class generateParenthesis {
    private List<String> res;
    public List<String> generateParenthesis(int n) {
        res = new ArrayList<>();
        backTrack(n, n, new StringBuilder());
        return res;
    }

    /**
     * �����������ʣ�� 1�� ������Ҳʣ��1������ô������ʹ�������š������Ż�ʣ1���������Ż�ʣ3������ô������ʹ��
     * @param left ʣ����õ�������
     * @param right ʣ����õ�������
     */
    private void backTrack(int left, int right, StringBuilder sb){
        if(right == 0){
            res.add(sb.toString());
            return;
        }
        if(left == right){
            sb.append('(');
            backTrack(left - 1, right, sb);
            sb.deleteCharAt(sb.length() - 1);
        } else {
            if(left > 0){ // ����Ҫע�� ���û��ʣ��������� �Ͳ��ܵݹ� �������޵ݹ���
                sb.append('(');
                backTrack(left - 1, right, sb);
                sb.deleteCharAt(sb.length() - 1);
            }
            sb.append(')'); // Ϊʲô�����Ų���Ҫ���ʣ�� ��Ϊ�ݹ����һ��ʼ������������������ʣ��ʱ�Ѿ��ҵ���Ҫ������ˣ��ͷ�����
            backTrack(left, right - 1, sb);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```
˼·������
* ���������һ��������⣬������Ȼ�뵽ʹ�û����㷨����Ч���ţ����Ǵ������������ŵĹ����������ŵ�����һ�����ڵ��������ŵ����������������������ŵ�������ȡ�
* ������Ч���ŵ��ص㣬��Ȼ�����ڴ��ϵ�ʱ�����Ҫʹ���������Ա�ʾ��ǰ��ʹ�õ��������ŵ�������������ѡ��`left, right`�ֱ��ʾʣ��Ŀ��õ��������ŵ�������
    * ���һ��ʹ��`n - left`������ʹ�õ�����������������
* Ȼ������ݺ���`void backTrack(int left, int right, StringBuilder sb)`��
    * ����������ʹ��`StringBuilder`Ϊ�˱���Ƶ����ƴ���ַ������ҷ������ʱɾ���ַ���
    * ������Ч���ŵĶ��壬���ʹ�õ�һ���������ţ����Ե�`right == 0`ʱ��ע��`left`һ����С�ڵ���`right`�ģ���ʾ�Ѿ�ѡ���������ţ�` res.add(sb.toString());`��Ȼ�󷵻ء�
    * ��`left == right`ʱ����ʹ�õ�����������������ʹ�õ���������������ʱ��һ�����ž�ֻ��ѡ�������š�`sb.append('(');`�������ڵ�ǰʹ����һ�������ţ����Եݹ����`backTrack(left - 1, right, sb);`����ɵ���֮����ݾ���`sb.deleteCharAt(sb.length() - 1);`��ɾ����ǰѡ�����š�
    * ������������Ż���ʣ�࣬��ǰ����ʹ�������š����ߵ�ǰ����ʹ�������š���������һ���ĵݹ������
        * ����Ϊʲô����Ҫ�ж�`right > 0`������Ҫ�ж�`left > 0`.��Ϊ`right == 0`���ں�����һ��ͷ�ͷ��أ������ܳ���`right !> 0`�������
* ���������ɽ��List(��Ա�����򻯻��ݺ�������)`res = new ArrayList<>();`Ȼ����û��ݺ������ٷ��ؽ�����ɡ�

���н����

* ִ����ʱ :1 ms, ������ Java �ύ�л�����99.02%���û�
* �ڴ����� :39.2 MB, ������ Java �ύ�л�����5.04%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз