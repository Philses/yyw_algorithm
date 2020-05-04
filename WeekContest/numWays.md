# LCP 07. ������Ϣ
### ԭ��
С���� A �ں� ta ��С������洫��Ϣ��Ϸ����Ϸ�������£�
�� n ����ң�������ұ�ŷֱ�Ϊ 0 �� n-1������С���� A �ı��Ϊ 0
ÿ����Ҷ��й̶������ɸ��ɴ���Ϣ��������ң�Ҳ����û�У�������Ϣ�Ĺ�ϵ�ǵ���ģ����� A ������ B ����Ϣ���� B ������ A ����Ϣ����
ÿ����Ϣ������Ҫ���ݸ���һ���ˣ�����Ϣ���ظ�����ͬһ����
����������� n���Լ��� [��ұ��,��Ӧ�ɴ�����ұ��] ��ϵ��ɵĶ�ά���� relation��������Ϣ��С A (��� 0 ) ���� k �ִ��ݵ����Ϊ n-1 ��С��鴦�ķ������������ܵ������ 0��

ʾ�� 1��
���룺n = 5, relation = [[0,2],[2,1],[3,4],[2,3],[1,4],[2,0],[0,4]], k = 3
�����3
���ͣ���Ϣ��С A ��� 0 ����ʼ���� 3 �ִ��ݣ������� 4������ 3 �ַ������ֱ��� 0->2->0->4�� 0->2->1->4�� 0->2->3->4��

ʾ�� 2��
���룺n = 3, relation = [[0,2],[2,1]], k = 2
�����0
���ͣ���Ϣ���ܴ�С A ������ 2 �ִ��ݵ���� 2

���ƣ�
```
2 <= n <= 10
1 <= k <= 5
1 <= relation.length <= 90, �� relation[i].length == 2
0 <= relation[i][0],relation[i][1] < n �� relation[i][0] != relation[i][1]
```

��Դ�����ۣ�LeetCode��
���ӣ�https://leetcode-cn.com/problems/chuan-di-xin-xi

### �ⷨ
```java
public class numWays {
    private int count;
    public int numWays(int n, int[][] relation, int k) {
        Map<Integer, List<Integer>> map = new HashMap<>();
        for(int[] temp : relation){
            if(!map.containsKey(temp[0]))
                map.put(temp[0], new ArrayList<>());
            map.get(temp[0]).add(temp[1]);
        }
        count = 0;
        backTracking(map, k, n, 0, 0);
        return count;
    }

    private void backTracking(Map<Integer, List<Integer>> map, int k, int n, int cur, int curPerson){
        if(cur == k){
            if(curPerson == n - 1)
                count++;
            return;
        }
        if(!map.containsKey(curPerson))
            return;
        for(int i : map.get(curPerson)){
            backTracking(map, k, n, cur + 1, i);
        }
    }
}
```
˼·������
* ָ�������Ĵ�0��n-1��·������Ҫͳ���ܹ��ж��١�������Ŀ������������֮�䴫����Ϣ�Ĺ�ϵ��ע����������ġ����������Ŀ��������һ������ͼ���ҵ���ָ�����0���������г���ָ����·��������·�����յ���Ҳ���ƶ��Ľڵ�n-1��
* ���������������Ȱ�ͼ����������ʹ�ù�ϣ����Ϊ��㣬ֵΪ�ý��ͨ������߿��Ե�������ڽ�㹹���List��Ȼ���ʼ��`count = 0`�����������ʾ��������Ȼ����ø������������ݺ�����
* ��ʵBFS,DFSȥ����·�������ԡ�������ʹ�û��ݵ�д����ʵ���Ͼ���DFS��������ݺ���`void backTracking(Map<Integer, List<Integer>> map, int k, int n, int cur, int curPerson)`
    * ��һ��������������ͼ�����ݽṹ��
    * �ڶ�������ָ��·�����ȣ�Ҳ���Ǵ�����Ϣ���ִ���
    * ������������ʾ�ܹ���n����ң���ô���һ����Ҿ���n-1
    * ���ĸ�������ʾ�����ǵڼ��ִ�����Ϣ����0��ʼ��
    * �����������ʾ��ǰ��ҵı�š�
* ���ݲ������壬������ʵ�����£�
    * ��`cur == k`��������Ϣ�Ĵ����Ѿ�ʹ�����ˣ�·������Ϊk�ˣ�����ʱ����Ҫ�жϵ�ǰ��ҵı���ǲ���n-1���������`count++`��Ȼ�󷵻ء�
    * ���򣬴��ݴ���û���꣬���`!map.containsKey(curPerson)`����ʾ�������޷������˴�����Ϣ������ֱ�ӷ��ء�
    * ��ȥ�������������˵����Ҫ��������Ѱ��·�������еĿ���Ϊ`for(int i : map.get(curPerson))`��Ȼ�����` backTracking(map, k, n, cur + 1, i);`�����ĸ�������������Ϣ����+1���������������һ��Ҫ���д�����Ϣ���˱�Ϊi��

���н����

* 3ms

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз