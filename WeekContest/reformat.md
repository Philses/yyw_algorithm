# 5388. ���¸�ʽ���ַ���
### ԭ��
����һ����������ֺ���ĸ���ַ��� s�����е���ĸ��ΪСдӢ����ĸ��
���㽫���ַ������¸�ʽ����ʹ���������������ַ������Ͷ���ͬ��Ҳ����˵����ĸ����Ӧ�ø������֣������ֺ���Ӧ�ø�����ĸ��
���㷵�� ���¸�ʽ���� ���ַ���������޷���Ҫ�����¸�ʽ�����򷵻�һ�� ���ַ��� ��

ʾ�� 1��
���룺s = "a0b1c2"
�����"0a1b2c"
���ͣ�"0a1b2c" ���������������ַ������Ͷ���ͬ�� "a0b1c2", "0a1b2c", "0c2a1b" Ҳ��������ĿҪ��Ĵ𰸡�

ʾ�� 2��
���룺s = "leetcode"
�����""
���ͣ�"leetcode" ��ֻ����ĸ�������޷��������¸�ʽ����������

ʾ�� 3��
���룺s = "1229857369"
�����""
���ͣ�"1229857369" ��ֻ�����֣������޷��������¸�ʽ����������

ʾ�� 4��
���룺s = "covid2019"
�����"c2o0v1i9d"

ʾ�� 5��
���룺s = "ab123"
�����"1a2b3"

��ʾ��
1 <= s.length <= 500
s ����СдӢ����ĸ��/��������ɡ�

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/reformat-the-string)��https://leetcode-cn.com/problems/reformat-the-string

### �ⷨ
```java
public String reformat(String s) {
        List<Character> nums = new ArrayList<>();
        List<Character> letters = new ArrayList<>();
        for (int i = 0; i < s.length(); i++) {
            char temp = s.charAt(i);
            if (temp >= '0' && temp <= '9')
                nums.add(temp);
            else letters.add(temp);
        }
        int temp = letters.size() - nums.size();
        if (temp >= 2 || temp <= -2)
            return "";
        StringBuilder res = new StringBuilder();
        if (temp == 1) {
            res.append(letters.get(letters.size() - 1));
            return create(nums, letters, res, letters.size() - 2);
        } else if (temp == -1) {
            res.append(nums.get(nums.size() - 1));
            return create(letters, nums, res, nums.size() - 2);
        } else
            return create(letters, nums, res, nums.size() - 1);
    }

    private String create(List<Character> one, List<Character> two, StringBuilder sb, int hi) {
        for (int i = hi; i >= 0; i--) {
            sb.append(one.get(i));
            sb.append(two.get(i));
        }
        return sb.toString();
    }
```
˼·������
* Ҫ��ֻ��Сд��ĸ�����ֹ��ɵ��ַ����������������ĸ����������ʽ
    * ����ĸ���������־��ɡ�
    * ���ԭ�ַ����Ѿ���������ĸ������֣���Ҫ���¹���һ���ַ�����
* ����������ĸҪ������֣�����һ��Ҫ����ĸ���������ָ�����ľ���ֵΪС�ڵ���1
    * ��ĸ���࣬�������ַ�������ĸ��ͷ
    * ���ָ��࣬�������ַ��������ֿ�ͷ
    * һ���࣬���㿪�ľͺ�?
* Ҫ֪����ĸ���������ָ�����������Ҫ�����Ƿֿ������飬����ȡ��һ��Ԫ�ء�Ϊ�˱��⹹�����ԭ�ַ���һ�����ַ������Ӹ��������Ԫ�ؿ�ʼ��ǰȡ�����Ա����ж�ÿһ���ַ���Ȼ�������Ӧ��`List`�С�
* ����`int temp = letters.size() - nums.size();`��
    * ���`temp >= 2 || temp <= -2`��������ĸ������̫�࣬�ܻ��г�˫�ģ��޷����������������ַ���������`""`
    * ���`temp == 1`����ĸ��һ�������ַ�������ĸ��ͷ��`res.append(letters.get(letters.size() - 1));`��Ȼ����ø�������������`return create(nums, letters, res, letters.size() - 2);`
    * ���`temp == -1`������һ������Գ�д��
    * ���`temp == 1`��������ĸ��ͷ�����ԣ�ֱ�ӷ���`create(letters, nums, res, nums.size() - 1);`
* ��������`String create(List<Character> one, List<Character> two, StringBuilder sb, int hi)`��
    * ��һ��������ʾ�ڸ���������ѭ��ʱ��ȡ����һ�������Ϊ�ڵ��ø�������ǰ������`StringBuilder sb`��������ַ�or��ĸ�������ڸ��������ڲ���Ҫ������ȡ��һ����𡣵ڶ���������ʾ�ڸ��������к�ȡ����һ�����
    * ���һ��������ʾ��List����һ��������ʼȡ���������֮������Ҫ������Ϊ������𳤶Ȳ�һ�������ⲿ��һ������Ѿ�ȡ��һ��Ԫ�ء�
* ʱ�临�Ӷȣ��������������븨�������������Ա���$O(1)$���ռ临�ӶȾ����ַ����ĳ��ȡ�

���н����

* easy 8ms��

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](123)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз