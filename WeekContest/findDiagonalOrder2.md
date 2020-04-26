# 5394. �Խ��߱��� II
### ԭ��
����һ���б�` nums` ������ÿһ��Ԫ�ض���һ�������б��������������ͼ�Ĺ��򣬰�˳�򷵻�` nums` �жԽ����ϵ�������

ʾ�� 1��
���룺`nums = [[1,2,3],[4,5,6],[7,8,9]]`
�����`[1,4,2,7,5,3,8,6,9]`

ʾ�� 2
���룺`nums = [[1,2,3,4,5],[6,7],[8],[9,10,11],[12,13,14,15,16]]`
�����`[1,6,2,8,7,3,9,4,12,10,5,13,11,14,15,16]`

ʾ�� 3��
���룺`nums = [[1,2,3],[4],[5,6,7],[8],[9,10,11]]`
�����`[1,4,2,5,3,8,6,9,7,10,11]`

ʾ�� 4��
���룺`nums = [[1,2,3,4,5,6]]`
�����`[1,2,3,4,5,6]`

��ʾ��

```
1 <= nums.length <= 10^5
1 <= nums[i].length <= 10^5
1 <= nums[i][j] <= 10^9
nums ������� 10^5 �����֡�
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/diagonal-traverse-ii)��https://leetcode-cn.com/problems/diagonal-traverse-ii

### �ⷨ
```java
public int[] findDiagonalOrder(List<List<Integer>> nums) {
        int count = 0;
        for(List l : nums)
            count += l.size();
        int[] res = new int[count];
        count = 0;
        Queue<int[]> queue = new LinkedList<>();
        queue.add(new int[]{0,0, nums.get(0).get(0)});
        while (!queue.isEmpty()){
            int[] item = queue.remove();
            int x = item[0], y = item[1];
            res[count++] = item[2];
            add(queue, x + 1, y , nums);
            add(queue, x, y + 1, nums);
        }
        return res;
    }

    private void add(Queue<int[]> queue, int x, int y, List<List<Integer>> nums){
        if(nums.size() > x && nums.get(x).size() > y && nums.get(x).get(y) > 0){
            queue.add(new int[]{x, y, nums.get(x).get(y)});
            nums.get(x).set(y, -1);
        }
    }
```
˼·������
* ÿһ���Խ��ߵĺ�������֮����ͬ����������˼·ȥ�����ᳬʱ����Ϊ���������10^5 * 10^5�ġ�
* �۲����ֱ���ӵ���������е�˳����ʾ��1������Ԫ���������ʾ��
    * �����`[0, 0]`��Ȼ����`[1, 0]`��`[0, 1]`
    * Ȼ�����`[2, 0]`��`[1, 1]`��`[1, 1]`��`[0, 2]`����
    * ����һ��bfs����������ٽ�Ԫ�ص�˳�����������ҡ�
* bfs�ö�����ģ��ͺã����Ǳ���������������Ҫ�����
    * ���ȷ��ĳһ��������`[x, y]`��ʾ��Ԫ�ش��ڡ�����ÿһ�ж�������Ԫ�ز����ģ�����ȡԪ��֮ǰҪ���ж�`nums.size() > x && nums.get(x).size() > y`
    * ����һ�������������ж�ĳ��Ԫ���Ѿ���ȡ������Ϊ�ڱ����б���`[1, 0]`���ұ�һ��Ԫ�غ�`[0, 1]`����һ��Ԫ����ͬһ����Ҫ�����ظ���ȡ�����ʹ�ö�ά��`boolean`��������ʶ�Ƿ���ȡ���������ռ����ƣ��ײ⣩����Ŀ�е�����`1 <= nums[i][j]`�������ã�����ȡ��ĳ��Ԫ�أ��ͽ�������Ϊ`-1`��������ֻ�е�`nums.get(x).get(y) > 0`ʱ��ȡ���Ԫ�ء�
* �����е�Ԫ����һ����Ԫ���飬ǰ����ֵ�ֱ��ʾx��y��������ֵ��Ϊ�������Ӧ��Ԫ�ء�
* ���ڴ�Ҫ��������飬�����ȱ���`nums`�е�ÿ��list��ȷ�������ܹ��ж��ٸ�Ԫ�ء�
* ������ÿһ��Ԫ�أ�ʱ�临�Ӷ���$O(n)$�ģ�����n��ʾ���ָ�����

���н����

* 42ms

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз