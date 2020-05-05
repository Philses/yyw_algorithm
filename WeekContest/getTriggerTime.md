# LCP 08. ���鴥��ʱ��
### ԭ��
��ս����Ϸ�У����������Ҫ��չ�Լ������������������µľ��顣һ����������Ҫ���������֣��ֱ��������ȼ���C������Դ������R���Լ��˿�������H��������Ϸ��ʼʱ���� 0 �죩���������Ե�ֵ��Ϊ 0��
������Ϸ���̵Ľ��У�ÿһ����ҵ��������Զ����Ӧ���ӣ�������һ����ά���� increase ����ʾÿ�����������������ά�����ÿ��Ԫ����һ������Ϊ 3 ��һά���飬���� [[1,2,1],[3,4,2]] ��ʾ��һ���������Էֱ����� 1,2,1 ���ڶ���ֱ����� 3,4,2��
���о���Ĵ�������Ҳ��һ����ά���� requirements ��ʾ�������ά�����ÿ��Ԫ����һ������Ϊ 3 ��һά���飬����ĳ������Ĵ������� c[i], r[i], h[i]�������ǰ C >= c[i] �� R >= r[i] �� H >= h[i] �������ᱻ������
����������Ϣ�������ÿ������Ĵ���ʱ�䣬����һ�����鷵�ء����ĳ�����鲻�ᱻ��������þ����Ӧ�Ĵ���ʱ��Ϊ -1 ��

ʾ�� 1��
���룺 increase = [[2,8,4],[2,5,0],[10,9,8]] requirements = [[2,11,3],[15,10,7],[9,17,12],[8,1,14]]
���: [2,-1,3,-1]
���ͣ�
��ʼʱ��C = 0��R = 0��H = 0
�� 1 �죬C = 2��R = 8��H = 4
�� 2 �죬C = 4��R = 13��H = 4����ʱ�������� 0
�� 3 �죬C = 14��R = 22��H = 12����ʱ�������� 2
���� 1 �� 3 �޷�������

ʾ�� 2��
���룺 increase = [[0,4,5],[4,8,8],[8,6,1],[10,10,0]] requirements = [[12,11,16],[20,2,6],[9,2,6],[10,18,3],[8,14,9]]
���: [-1,4,3,3,3]

ʾ�� 3��
���룺 increase = [[1,1,1]] requirements = [[0,0,0]]
���: [0]

���ƣ�
```
1 <= increase.length <= 10000
1 <= requirements.length <= 100000
0 <= increase[i] <= 10
0 <= requirements[i] <= 100000
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/ju-qing-hong-fa-shi-jian)��https://leetcode-cn.com/problems/ju-qing-hong-fa-shi-jian

### �ⷨ
```java
public class getTriggerTime {
    public int[] getTriggerTime(int[][] increase, int[][] requirements) {
        int n = requirements.length;
        int m = increase.length;
        int[] cs = new int[m + 1];
        int[] rs = new int[m + 1];
        int[] hs = new int[m + 1];
        prepare(cs, rs, hs, increase);
        int[] res = new int[n];
        for (int i = 0; i < n; i++) {
            doResult(res, i, cs, requirements[i][0], m + 1);
            doResult(res, i, rs, requirements[i][1], m + 1);
            doResult(res, i, hs, requirements[i][2], m + 1);
        }
        return res;
    }

    private void prepare(int[] cs, int[] rs, int[] hs, int[][] increase) {
        int c = 0, r = 0, h = 0;
        for (int i = 0; i < cs.length - 1; i++) {
            c += increase[i][0];
            r += increase[i][1];
            h += increase[i][2];
            cs[i + 1] = c;
            rs[i + 1] = r;
            hs[i + 1] = h;
        }
    }

    private void doResult(int[] res, int i, int[] s, int target, int arrLength) {
        if (res[i] == -1) return;
        int temp = search(s, target);
        if (temp == arrLength) {
            res[i] = -1;
            return;
        }
        res[i] = Math.max(res[i], temp);
    }

    private int search(int[] nums, int target) {
        int temp = Arrays.binarySearch(nums, target);
        if(temp < 0) return -temp - 1;
        for (int i = temp; i >= 0; i--) {
            if (nums[i] != nums[temp])
                return i + 1;
        }
        return 0;
    }
}
```
˼·������
* ����ÿһ�����飬�е�����ġ�ľͰЧӦ��������һ�촥����ȡ����C,R,H����������������Ǹ�������Ҫ��������Ҳ����˵��Ҫ�ҵ�C,R,H�ֱ�����`C >= c[i], R >= r[i], H >= h[i] `�������������Ȼ��������������ȡ���ֵ�����Ǹþ���Ĵ���������

* ������Ŀ���������������ǵ����ģ�Ҫ֪��ʲôʱ���������Էֱ����㴥������������Ҫ����`increase`�����ÿһ����������ֵ�ֱ��Ƕ��١�ʹ�ø�������`prepare(int[] cs, int[] rs, int[] hs, int[][] increase)`��

    * ע��`cs, rs, hs`�ĳ���Ϊ`m + 1`����Ϊ��0����������Ϊ0���еľ���Ҫ�������ֵΪ0�����Ե�0�첻�����ǡ�
    * Ȼ��ͨ��ѭ���ۼӣ���¼��ÿһ����ۼӺ͵���Ӧ�������С���PS��������˵�����ǰ׺��?��

* Ȼ��������ȥ����ĳһ���������������������һ�졣

    * ʹ�����Բ��ң������������Ȼ��ʱ��
    * �ڼ�����ÿһ�������ֵ������ʱ��������������ǵ����ģ���ô��Ӧ��ʹ�ö��ֲ��ҡ�
    * ���ֱ�ӵ��ÿ⺯�������صĽ������һ���������������������һ�죬��Ϊ������һ�����ȵ�Ԫ�أ����ص�������һ��������ߵ��Ǹ����������Ը�����ֲ��ҡ�`search(int[] nums, int target)`:
        * ���ȵ��ÿ⺯�����õ�`temp`�����`temp < 0`˵��û���ҵ����Ԫ�أ����λ����Ҫ�����λ�ã����λ�ñ�����Ԫ�ؾ��Ǵ���`target`����С��Ԫ�أ����Է���`-temp - 1`����Ϊ�⺯������ֵ���Ǹ�Ԫ������+1��ȡ����Ҫ�õ������������㣩��
        * ���򣬾��ǲ��ҳɹ�����`temp`��ʼ�������ҵ���һ��������`nums[temp]`��Ԫ�أ�������Ϊ`i`����ô`i + 1`�������������������������һ�졣

* ��������������`void doResult(int[] res, int i, int[] s, int target, int arrLength)`��

    * ��һ��������Ϊ������`res[i]`�����i������Ĵ���ʱ��
    * ����������ڲ���ĳһ����������Ҫ�������������Ȼ���޸�`res[i]`���������ĸ�����Ϊ��Ӧ���������������Ҫ�������ֵ���������������������ĳ��ȡ�
    * ���`res[i] == -1`������ζ��ĳһ������ֵ�޷����㣬���鲻�ᴥ������ô�Ե�ǰ���ԵĲ��ҾͲ����ˣ�ֱ�ӷ��ء�
    * ���ҽ��`temp = search(s, target)`�����`temp == arrLength`��˵����һ�������������Դﲻ��������`res[i] = -1`�����򣬾͸���`res[i] = Math.max(res[i], temp);`

* ����������������Ϊ��������������󣬶Ծ��鵱��ѭ�������������Ե�`doResult`���ɡ�

* ʱ�临�Ӷ�Ϊ$O(nlog(m))$���ռ临�Ӷ�Ϊ$O(3m + n)$��

* �����ÿ⺯�����Լ�д��Ѱ�����������д��ڵ���`target`��������С��Ԫ�ص�����

    * ```java
        private int mySearch(int[] nums, int target) {
                int lo = 0, hi = nums.length - 1;
                while (lo <= hi) {
                    int mid = (hi - lo) / 2 + lo;
                    if (nums[mid] < target) lo = mid + 1;
                    else hi = mid - 1;
                }
                return lo;
            }
        ```

    * ���ַ������Ǳ�ʹ�ÿ⺯�������������ķ����ܳ��Ľ������������Ŀ⺯���Ż���á�

���н����

 * ִ����ʱ :51 ms, ������ Java �ύ�л�����56.31%���û�
 * �ڴ����� :97.6 MB, ������ Java �ύ�л�����100.00%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз