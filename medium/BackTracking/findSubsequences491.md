# 491. ����������
### ԭ��
����һ����������, ����������ҵ����и�����ĵ��������У����������еĳ���������2��

ʾ��:
����: [4, 6, 7, 7]
���: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]

˵��:
��������ĳ��Ȳ��ᳬ��15��
�����е�������Χ�� [-100,100]��
���������п��ܰ����ظ����֣���ȵ�����Ӧ�ñ���Ϊ������һ�������

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/increasing-subsequences)��https://leetcode-cn.com/problems/increasing-subsequences

### �ⷨ
```java
public class findSubsequences491 {
    private List<List<Integer>> res;
    private int n;
    public List<List<Integer>> findSubsequences(int[] nums) {
        res = new ArrayList<>();
        n = nums.length;
        if(n == 0)
            return res;
        backTrack(nums, new int[n], 0, -1, Integer.MIN_VALUE);
        return res;
    }

    private void backTrack(int[] nums, int[] temp, int curPos, int preIndex, int pre){
        if(curPos > 1){
            List<Integer> tempRes = new ArrayList<>();
            for(int i = 0; i < curPos; i++)
                tempRes.add(temp[i]);
            res.add(tempRes);
        }

        Set<Integer> set = new HashSet<>();
        for(int i = preIndex + 1; i < n; i++){
            if(!set.contains(nums[i]) && nums[i] >= pre){
                set.add(nums[i]);
                temp[curPos] = nums[i];
                backTrack(nums, temp, curPos + 1, i, nums[i]);
            }
        }
    }
}

```
˼·������
* ��ĿҪ��ľ���һϵ����ϣ�����Ԫ�ظ�������1�������ǵ����ģ����Ҳ��Ϊ��������������������ⶼ�뵽ʹ�û����������
* �����㷨��Ҫ���ǻ��ݺ����Ķ���`void backTrack(int[] nums, int[] temp, int curPos, int preIndex, int pre)`:
    * ���ȵ�һ����������Ȼ�Ǵ�ѡ���ԭ���顣
    * �ڶ�������`int[] temp`�������ڴ����ѡ�����֡�
    * ������Ŀ�涨Ԫ�ظ���Ҫ����1���ɣ�����������Ҫһ������`int curPos`��һ�κ�������ҪѰ�ҵ����ַ���`temp`������`curPos`�������Ե�`curPos > 1`ʱ����ζ�ŵ�ǰ`temp`�������Ѿ�����1����Ҫ�������Ϸ�����List�С�
        * �½�һ����ʾĳ��ϵ�List`List<Integer> tempRes = new ArrayList<>();`����`temp`��`[0, curPos - 1]`�����ַ���`tempRes`��
        * Ȼ��`res.add(tempRes);`
    * ������ѡ�����Ҫ������������Ҫ���������`int pre`��ʾ��һ�������Ƕ��٣���ǰҪѡ�����־ͱ������`pre`��
    * ���ĸ����������ã�����һ��tip��
* �����������������ظ��Ĵ���ʽ��
    * ���ݺ����ĵ��ĸ�����`preIndex`����ʾ��һ��ѡ����Ԫ����`nums`�е�����������һ�����ֵ�ѡȡҪ��`preIndex + 1`��ʼȥѡ������������Ԫ�ء�����Ŀ����ʾ��������
        * ��һ������ѡ����4���ڶ�������ѡ`nums[2]`������7������������ѡ����`nums[3]`������7
        * ��һ������ѡ����4���ڶ�������ѡ`nums[3]`������7������������ѡ����`nums[2]`������7
        * ����������ظ�����������������У�Ҫ��һ��������ʾ��һ��ѡȡ���ֵ���������������ظ�
    * ����һ���ظ�������ǣ���ǰ`curPos`������ѡ����ظ�������Ŀ����ʾ��������
        * ��һ����������ѡ��4��6������������ѡ��`nums[2]`������7��
        * ��һ����������ѡ��4��6������������ѡ��`nums[3]`������7��
        * ����������ظ���������ѡ��ǰ�����ǣ�ʹ��`Set<Integer> set = new HashSet<>();`����ŵ�ǰ��ѡ������֡�
* ���ڻ��ݣ�����ʹ��`int[] temp`��������֣���ô�ڵݹ����ʱ���Ὣ`curPos`���������ֵ���ϸ��ǣ������ڴ�Ž��ʱ����List������Ϊ`[0, curPos - 1]`������Ȼ�ﵽ�˻��ݵ�Ŀ�ġ�
* ���ݺ��������⣺���ȱ�����`int i = preIndex + 1`��ʼ����������`!set.contains(nums[i]) && nums[i] >= pre`�����⵱ǰѡ���ظ���������������������֣��Ƚ������`set.add(nums[i]);`��Ȼ��ֵ��`temp[curPos] = nums[i];`���ٵݹ����` backTrack(nums, temp, curPos + 1, i, nums[i]);`����������ǰ�涨�崫�뼴�ɡ�
* �������У�����Ա�������򻯻��ݺ����Ĵ��Σ���ֵ���ж����`n == 0`����Ҫѡ��ֱ�ӷ��أ�������û��ݺ���` backTrack(nums, new int[n], 0, -1, Integer.MIN_VALUE);`
    * ��������������ε���Ҫѡ�����ַ���`temp[0]`��ѡ��һ�����֣�
    * ���ĸ�������ʹ����ε��ô�`-1 + 1 = 0`��ʼѡ���֡�
    * �����������ʾ��֮ǰû��ѡ�����֣����Ե�һ�����ֿ���ѡ�κ����֣���Ϊ`nums[i] >= Integer.MIN_VALUE`�϶���������

���н����
* ִ����ʱ :6 ms, ������ Java �ύ�л�����92.85%���û�
* �ڴ����� :47.3 MB, ������ Java �ύ�л�����100.00%���û�
----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз