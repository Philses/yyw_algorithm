# 77.组合：0，1...n的序列中k个数的组合

### 原题
给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。
示例:
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

来源：力扣（LeetCode）
[链接](https://leetcode-cn.com/problems/combinations)：https://leetcode-cn.com/problems/combinations

****

### 解法：回溯

```java
    private List<List<Integer>> result = null;
    public List<List<Integer>> combine(int n, int k) {
        result = new ArrayList<>();
        if (k == 0 || k > n)
            return result;
        backTrack(n, k, 0, new int[k], 0);
        return result;
    }

    private void backTrack(int n, int k, int pre, int[] temp, int curIndex) {
        if (curIndex == k) {
            List<Integer> tempRes = new ArrayList<>();
            for (int i : temp)
                tempRes.add(i);
            result.add(tempRes);
            return;
        }

        for (int i = pre + 1; i <= n; i++) {
            temp[curIndex] = i;
            backTrack(n, k, i, temp, curIndex + 1);
        }
    }
```

思路分析：

* 组合问题：当选定了第一位数字之后，只需要再选第2-k位数字即得到一个组合；当选定了第一第二位数字之后，只需要再选定第3-k位数字即可得到一个组合......以此类推，直到选定第k个数字。这是递归的关系。
* 这里存在一个问题，以原题中的示例举例：
    * 第一位选择1，第二位选择2得到[1,2]；第一位选择2，第二位选择1得到[2,1]。对于组合问题，这是同一个结果。
    * 第一位选择2，第二位选择4得到[2,4]；第一位选择4，第二位选择2得到[4,2]。对于组合问题，这是同一个结果。
    * 要避免这样的重复，只要限定在选取第`curIndex`位时，当前位选择的数字大于前面一位的数字，也就是从`pre+1`开始。
* 在递归中，需要一个变量`pre`代表上一位选定的数字，需要一个数组`temp`存放组合的结果，需要一个`curIndex`表示当前在选定第几个数字，`curIndex`从0开始。

代码解释：

* 第4-5行，条件`k == 0 || k > n`意味着选不出组合。
* 第6行,`backTrack(n, k, 0, new int[k], 0);`第一次调用，前面没有选定的数，所以第三个实参为0；接下来要选择第0位的数字（咋那么别扭，这里是索引😐）
* 第11行，要`curIndex == k`意味着已经选出了k个数字，因为`curIndex`从0开始。
* 第19行，`int i = pre + 1`，为了不出现重复结果，当前位要比前一位选的数字大一。

运行结果：

* 执行用时 :9 ms, 在所有 Java 提交中击败了72.85%的用户
* 内存消耗 :42.8 MB, 在所有 Java 提交中击败了11.56%的用户

---

### 反思
优化过程(剪枝过程)就是：把 `i <= n` 改成` i <= n - (k - curIndex) + 1`
题解大佬的做法 在`backTrack`中的`for`循环` i`的截至为` i <= n - (k - curIndex) + 1`

可以这么想：
当剩余要选的数为2时，当前可选的最大的数为n-1，因为如果当前选了n，则下一个数没法选
当剩余要选的数为3时，当前可选的最大的数为n-2，当前选了n-1则下一个数选n，但最后一个数就没法选了
所以剩余x位时，可选最大数位 n - x + 1
在选择`curIndex`位时，剩余要选的数位` k - curIndex`