# 78. �Ӽ�
### ԭ��
����һ�鲻���ظ�Ԫ�ص���������` nums`�����ظ��������п��ܵ��Ӽ����ݼ�����
˵�����⼯���ܰ����ظ����Ӽ���

ʾ��:
����: `nums = [1,2,3]`
���:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/subsets)��https://leetcode-cn.com/problems/subsets

### �ⷨ
```java
public class subsets {
    private List<List<Integer>> result;
    public List<List<Integer>> subsets(int[] nums) {
        result = new ArrayList<>();
        result.add(new ArrayList<>()); // �ռ�
        if (nums.length == 0)
            return result;
        for (int i = 1; i <= nums.length; i++) {
            backTrack(nums, i, 0, new int[i], 0);
        }
        return result;
    }

    private void backTrack(int[] nums, int k, int start, int[] temp, int curIndex) {
        if(curIndex == k){
            List<Integer> tempRes = new ArrayList<>();
            for(int i : temp)
                tempRes.add(i);
            result.add(tempRes);
            return;
        }
        // ����ļ���֦���������Բο�77�� �Ӽ���ʵҲ����һ����ϣ�������ѡ����ʱ�����ѡ��̫�󣬻ᵼ�º�������ѡ��
        for(int i = start; i < nums.length - k + curIndex + 1; i++){
            temp[curIndex] = nums[i];
            backTrack(nums, k, i + 1, temp, curIndex + 1);
        }
    }
}
```
˼·������
* ���һ�����ϵ������Ӽ������Խ��Ӽ���Ԫ�ظ���0��1��2����n�����֣���ͬ���ȵ��Ӽ���϶���������ظ���
* ���ڼ��ϣ���ϵ���Ŀ�����뵽ʹ�û��ݣ�Ϊ�˼򻯵ݹ�ʱ�Ĵ��Σ��������`List<List<Integer>> result;`����Ϊ��Ա���������������У����ȴ���List��Ȼ�󽫿ռ���������`result.add(new ArrayList<>());`�����������ԭ����Ԫ��Ϊ0��ֱ�ӷ��ء������Ӽ�����1��`nums.length`�������Ӽ�����������
* ���ڶ���`void backTrack(int[] nums, int k, int start, int[] temp, int curIndex)`������Ѱ��ָ�����ȵ��Ӽ��ĵ�ǰԪ�ء�
    * �ڶ�������`int k`��ʾ�Ӽ��ĳ��ȣ����ĸ�����`int[] temp`�ǳ���Ϊ`k`�����飬���ڴ���Ӽ���Ԫ��
    * ������������ʾѰ��Ԫ��Ӧ�ô�ԭ��������`start`����ʼѰ���Ӽ��ĵ�ǰԪ�ء�����Ϊ�˱���������磺��1��2��3���루1��3��2���������ظ������ڼ������ظ�����Ҳ����ѡ����1��1��1���������Եļ��ϡ�
    * �����������ʾ���������Ӽ��ĵ�`curIndex`��Ԫ�ء�
    * �ݹ鿪ʼʱ�����`curIndex == k`˵���Ѿ��ҹ�`k`��Ԫ�أ���ʱ�������Ӽ���������������ݹ顣
    * Ȼ��������п��ܵ�Ԫ�أ�`temp[curIndex] = nums[i];`���ҵ���`backTrack(nums, k, i + 1, temp, curIndex + 1);`��ʾ��һ��Ҫ�ҵ�Ԫ�ش�ԭ��������`i + 1`��ʼ����Ԫ���ǵ�`curIndex + 1`�����������ͨ��`temp[curIndex]`�ĸ�ֵ������ɼ��ɡ�
* ���ҵ�ǰԪ��ʱҪע���֦����������������[77. ���](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/BackTracking/combine77.md)�з�˼���ֵļ�֦��
    * ˼·���ǣ������ǰѡ��Ԫ�ص������ܿ��󣬺���ʣ���ѡ��Ԫ�ؾͲ����Դչ�k����
    * ���赱ǰ��ѡ��Ԫ�ص�����Ϊ`i`����ʣ�Ŀ�ѡ��Ԫ��Ϊ����`[i + 1, nums.length - 1]`����ʣ���Ԫ�ظ���Ϊ`nums.length - i - 1`��
    * ����`i`����ѡ��Ԫ�ظ���Ϊ`curIndex + 1`��Ҫѡ`k`��Ԫ�أ�����Ҫ`k - curIndex - 1`��
    * Ҫ�ܱ�֤ʣ��Ԫ����ѡ��`k`������Ҫ��`nums.length - i - 1 >= k - curIndex - 1`����`i <= nums.length - k + curIndex`��Ҳ����`i < nums.length - k + curIndex + 1`

���н����

* ִ����ʱ :0 ms, ������ Java �ύ�л�����100.00%���û�
* �ڴ����� :39.3 MB, ������ Java �ύ�л�����5.08%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз