# 90. �Ӽ� II
### ԭ��
����һ�����ܰ����ظ�Ԫ�ص��������� `nums`�����ظ��������п��ܵ��Ӽ����ݼ�����
˵�����⼯���ܰ����ظ����Ӽ���

ʾ��:
����: [1,2,2]
���:

```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/subsets-ii)��https://leetcode-cn.com/problems/subsets-ii

### �ⷨ
```java
public class subsetsWithDup {
    private List<List<Integer>> res;

    public List<List<Integer>> subsetsWithDup(int[] nums) {
        res = new ArrayList<>();
        res.add(new ArrayList<>());
        if (nums == null || nums.length == 0)
            return res;
        Arrays.sort(nums);
        for (int i = 1; i <= nums.length; i++) {
            backTrack(nums, i, 0, new int[i], 0);
        }
        return res;
    }

    private void backTrack(int[] nums, int k, int start, int[] temp, int curIndex) {
        if (curIndex == k) {
            List<Integer> tempRes = new ArrayList<>();
            for (int i : temp)
                tempRes.add(i);
            res.add(tempRes);
            return;
        }
        for (int i = start; i < nums.length - k + curIndex + 1; i++) {
            if (i != start && nums[i] == nums[i - 1]) // �ظ�Ԫ�صĽ����ʽ���ǣ���ѡ��ĳһλԪ��ʱ���Ѿ�ѡ���ľ�����
                continue;
            temp[curIndex] = nums[i];
            backTrack(nums, k, i + 1, temp, curIndex + 1);
        }
    }
}
```
˼·������
* �������[78. �Ӽ�](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/BackTracking/subsets78.md)����һ�£�˼·����һ�£��������Ҳһ�£����ݺ����Ĳ�������֦�ļ��ɵȶ�һ�£�����ͬ���Ǳ��⵱��ԭ���������ظ�Ԫ�أ�Ҫ�ų��ظ�Ԫ�ش������Ӽ�ѡȡ���ظ���
* �ظ�Ԫ�صĽ����ʽ���ǣ���ѡ��ĳһλԪ��ʱ���Ѿ�ѡ���ľ�������Ҫ�ܴﵽ���Ҫ����Ҫʹ����������������ѡ��ĳ��Ԫ��`i`��ʱ����ǰ��һ��Ԫ�رȽϣ����`nums[i] == nums[i - 1]`��˵���Ѿ�����һ��ѭ����ѡ����ˣ�������������Ȼ���`i == start`�����ǵ�һ����������Ҫ������
* ע�⴦���ظ�Ԫ�ص�ʱ�򲻿���ʹ�ù�ϣ����һ�����ӣ�����[4,4,1,4]����һ��Ԫ��ѡ��������Ϊ0��4��
    * �ڶ���Ԫ��ѡ������Ϊ1��4��Ȼ���¼�˵�ǰѡ���4����ô�ڶ���Ԫ�ػ�����ѡ��1��
    * ������Ԫ��������������ֱ�ѡ��1������Ϊ3��4���õ����Ӽ��ǣ�4��4��1���루4��1��4�����Ӽ��ϵĽǶ���˵�������ͳ������ظ���

���н����

* ִ����ʱ :1 ms, ������ Java �ύ�л�����100.00%���û�
* �ڴ����� :41.8 MB, ������ Java �ύ�л�����5.01%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз