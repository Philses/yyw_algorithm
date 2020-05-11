# 127. ���ʽ���
### ԭ��
�����������ʣ�beginWord �� endWord����һ���ֵ䣬�ҵ��� beginWord �� endWord �����ת�����еĳ��ȡ�ת������ѭ���¹���
ÿ��ת��ֻ�ܸı�һ����ĸ��
ת�������е��м䵥�ʱ������ֵ��еĵ��ʡ�
˵��:
���������������ת�����У����� 0��
���е��ʾ�����ͬ�ĳ��ȡ�
���е���ֻ��Сд��ĸ��ɡ�
�ֵ��в������ظ��ĵ��ʡ�
����Լ��� beginWord �� endWord �Ƿǿյģ��Ҷ��߲���ͬ��

ʾ�� 1:
����:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]
���: 5
����: һ�����ת�������� "hit" -> "hot" -> "dot" -> "dog" -> "cog",
�������ĳ��� 5��

ʾ�� 2:
����:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

���: 0
����: endWord "cog" �����ֵ��У������޷�����ת����

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/word-ladder)��https://leetcode-cn.com/problems/word-ladder

### 2�ֽⷨ
##### 1.bfs
```java
private int length;
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        int n = wordList.size();
        if(n == 0)
            return 0;
        length = beginWord.length();
        boolean[] marked = new boolean[n];
        Queue<Pair<String, Integer>> queue = new LinkedList<>();
        queue.add(new Pair<>(beginWord, 1));
        while(!queue.isEmpty()){
            Pair<String, Integer> temp = queue.remove();
            for(int i = 0; i < n; i++){
                String next = wordList.get(i);
                if(!marked[i] && canTransform(temp.getKey(), next)){
                    if(next.equals(endWord))
                        return temp.getValue() + 1;
                    marked[i] = true;
                    queue.add(new Pair<>(wordList.get(i), temp.getValue() + 1));
                }
            }
        }
        return 0;
    }

    private boolean canTransform(String from, String to){
        int count = 0;
        for(int i = 0; i < length; i++){
            if(from.charAt(i) != to.charAt(i)){
                if(count == 1)
                    return false;
                else count++;
            }
        }
        return true;
    }
```
˼·������
* ����֮�䰴�չ�����Խ���ת������ô����ת��������������ʾͿ�����Ϊ����ͨ�ģ���ô`startWord`���ֵ��еĵ��ʾ͹���һ������ͼ��Ҫ������������ҵ�`startWord`��`endWord`֮������·�����ȣ���������������û����ͨ�ͷ���0��������ȻҪʹ��BFS��
* һ���ؼ������������ж����������Ƿ����ӣ����ݹ���ʹ�ø�������`boolean canTransform(String from, String to)`�����жϡ�
    * ������ֻ��һ����ĸ�ܽ���ת��������˵ֻ��һ����ĸ��ͬ��
    * ���ҵ��ʳ���һ�£����Կ��Ա����������ʵĶ�Ӧλ�ã�����ʹ��`count`������Ӧλ����ĸ����ͬ�Ĵ�����
    * ���������Ӧλ�ò���ͬ�����ж����`count == 1`��˵��֮ǰ�Ѿ��й�����ȵ���ĸ���޷�ת������`false`�����򣬾ͽ�`count++`����ʾ�Ѿ���һ����ĸ����ȡ�
* ���������о��Ǳ�׼��BFS�ˣ�
    * �����ֵ��еĵ��ʶ�����ͬ�����Կ���ʹ��` boolean[] marked = new boolean[n];`��ͨ���±�����ʾ�ֵ���ĳ�������Ƿ��ѷ��ʡ�
    * ��������Ҫ������·�������Զ��е�Ԫ��Ӧ��ʹ��`Pair<String, Integer>`���Ե���Ϊ����ֵ��ʾ�任��������ʵ����·���Ľ������������Ŀʾ������������·��������������Խ�`startWord`�Ž�ȥʱ���������`queue.add(new Pair<>(beginWord, 1));`
    * �������ö���ģ��BFS��ȡ����ǰ���ʼ�����˵��ʵĽ�����������ֵ��еĵ��ʣ�����õ���û�з��ʹ����ҿ����ɵ�ǰ����ת���õ�`!marked[i] && canTransform(temp.getKey(), next)`
        * Ȼ���ж���һ���������`next.equals(endWord)`������ɱ任�ˣ�����`temp.getValue() + 1;`
        * ���򣬽���һ����������Ϊ�ѷ��ʣ�Ȼ��`queue.add(new Pair<>(wordList.get(i), temp.getValue() + 1))`�������Ҫ+1��
* ������BFS��ɻ�û�з��ؽ�����൱���Ѿ��ҵ���`startWord`��ͨ��ת���õ������е��ʣ�����û��`endWord`���������ս������0��
* ʱ�临�Ӷ�Ϊ$O(n * word.length)$���ռ临�Ӷ�ȡ���ڶ����е�Ԫ�ء�

���н����
* ִ����ʱ :531 ms, ������ Java �ύ�л�����32.64%���û�
* �ڴ����� :41.2 MB, ������ Java �ύ�л�����44.22%���û�

##### 2.˫��bfs
```java
	private int length;
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        int n = wordList.size();
        boolean flag = false;
        for(int i = 0; i < n; i++){
            if(wordList.get(i).equals(endWord)){
                flag = true;
                break;
            }
        }
        if(!flag) return 0;
        length = beginWord.length();
        Map<String, Integer> beginMap = new HashMap<>(); // ���Ƿ��ʵ����ַ����� ֵ�Ƿ��ʵ����ַ���ʱ��ת�������ĳ���
        Map<String, Integer> endMap = new HashMap<>();
        Queue<String> q1 = new LinkedList<>();
        Queue<String> q2 = new LinkedList<>();
        q1.add(beginWord);
        q2.add(endWord);
        beginMap.put(beginWord, 1);
        endMap.put(endWord, 1);
        while(!q1.isEmpty() && !q2.isEmpty()){
            int temp = search(q1, beginMap, endMap, wordList, n);
            if(temp != -1) return temp;
            temp = search(q2, endMap, beginMap, wordList, n);
            if(temp != -1) return temp;
        }
        return 0;
    }
    
    private int search(Queue<String> q, Map<String, Integer> m1, Map<String, Integer> m2, List<String> wordList, int n){
        String s1 = q.remove();
        for(int i = 0; i < n; i++){
            String next = wordList.get(i);
            if(!m1.containsKey(next) && canTransform(s1, next)){
                if(m2.containsKey(next))
                    return m1.get(s1) + m2.get(next);
                q.add(next);
                m1.put(next, m1.get(s1) + 1);
            }
        }
        return -1;
    }

    private boolean canTransform(String from, String to){
        int count = 0;
        for(int i = 0; i < length; i++){
            if(from.charAt(i) != to.charAt(i)){
                if(count == 1)
                    return false;
                else count++;
            }
        }
        return true;
    }
```
˼·������
* ����ȷ�����϶���ʹ��BFS������ת���ĸ�������ͬ����һ����ô���������Ż�˼·��ʲô�أ�
    * ����һ��BFS����ʵ�����Ǵ�������������������ÿ�ζ��������������չ������ͬ���ȣ�����ʵķ�Χ���Խ�������Ϊһ��ԲȦ��
    * �ӵ�һ���������BFS������Բ���ȴ��������������������Բ����������������ͱ�ʾ���ʵĵ���ࡣ
    * ���Կ����������ʾ��ͼ��
    * ![ladderLength.png](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/BFSorDFS/ladderLength.png?raw=true)
* �������Ǵ�`startWord, endWord`ͬʱ��ʼ����BFS��������Ҫ����������ģ����������BFS������ʹ������`Map<String, Integer>`����ʾ����BFS�зֱ���ʵ��Ľ�㣬��ȻҪ�󵥴ʸ�����ֵ��ʵ���ǵ���õ���ʱ��Ľ������`startWord, endWord`�ֱ������У����ҷֱ���`map`�м�¼��������������Ϊ1��
* Ȼ��ͬʱ����BFS��ѭ������`while(!q1.isEmpty() && !q2.isEmpty())`��
* Ȼ�󿴸�������`int search(Queue<String> q, Map<String, Integer> m1, Map<String, Integer> m2, List<String> wordList, int n)`:
    * ��һ��������ĳ��ģ��BFS�Ķ��У��������������ֱ��Ƿֱ��¼��`startWord, endWord`Ϊ�����ʹ��ĵ��ʡ����ĸ������ǵ����ֵ䡣���������`int n`���������ã������������������·���Ѿ���ͨ����ʾ�Ѿ��ҵ������·������ʱ����n����������·���Ľ����������û����ͨ�ͷ���-1��ʾ��Ҫ��������·������
    * Ȼ�����Ʒ���1����������ȡ��һ�����ʣ�Ȼ����������ֵ䣬���`!m1.containsKey(next) && canTransform(s1, next)`��ʾ��ǰ���ʿ�ת��Ϊ��һ�����ʣ����Ҵ���һ�ߵ���㻹û�з��ʹ��õ㡣�����ʱ`m2.containsKey(next)`��ʾ������һ������Ѿ�����`next`����ʱ·����ͨ�ˣ�����`return m1.get(s1) + m2.get(next);`������`next`����Ϊ����һ������ѷ��ʣ���������Ӧ���С����ֵ��ѭ���������ͷ���-1����ʾ��û����ͨ��
* �ٿ�����������������������Ӧ��`search`�������������ֵ��Ϊ-1�ͷ��ء����������ֱ��ѭ������˵��`startWord`����ת��Ϊ`endWord`������0��

���н����
* ִ����ʱ :119 ms, ������ Java �ύ�л�����55.80%���û�
* �ڴ����� :39.5 MB, ������ Java �ύ�л�����64.98%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз