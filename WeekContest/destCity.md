# 5400. �����յ�վ
### ԭ��
����һ��������·ͼ������·ͼ�е�������·������ paths ��ʾ������` paths[i] = [cityAi, cityBi]` ��ʾ����·�����` cityAi` ֱ��ǰ��` cityBi` �������ҳ�������е��յ�վ����û���κο���ͨ���������е���·�ĳ��С�
��Ŀ���ݱ�֤��·ͼ���γ�һ��������ѭ������·�����ֻ����һ�������յ�վ��

ʾ�� 1��
���룺paths = [["London","New York"],["New York","Lima"],["Lima","Sao Paulo"]]
�����"Sao Paulo" 
���ͣ��� "London" ���������ִ��յ�վ "Sao Paulo" ���������е�·���� "London" -> "New York" -> "Lima" -> "Sao Paulo" ��

ʾ�� 2��
���룺paths = [["B","C"],["D","B"],["C","A"]]
�����"A"
���ͣ����п��ܵ���·�ǣ�
"D" -> "B" -> "C" -> "A". 
"B" -> "C" -> "A". 
"C" -> "A". 
"A". 
��Ȼ�������յ�վ�� "A" ��

ʾ�� 3��
���룺paths = [["A","Z"]]
�����"Z"

��ʾ��
```
1 <= paths.length <= 100
paths[i].length == 2
1 <= cityAi.length, cityBi.length <= 10
cityAi != cityBi
```
�����ַ������ɴ�СдӢ����ĸ�Ϳո��ַ���ɡ�

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/destination-city)��https://leetcode-cn.com/problems/destination-city

### �ⷨ
```java
public class destCity {
    public String destCity(List<List<String>> paths) {
        Map<String, String> map = prepare(paths);
        String from = paths.get(0).get(0);
        while(true){
            if(!map.containsKey(from))
                return from;
            from = map.get(from);
        }
    }

    private Map<String, String> prepare(List<List<String>> paths){
        Map<String, String> map = new HashMap<>();
        for(List<String> path : paths)
            map.put(path.get(0), path.get(1));
        return map;
    }
}
```
˼·������
* �ؼ�����Ҫ�ӳ�������`from`ȥ�ҵ����������һ�����У����������û�п��Ե���ĳ��У���ô�������յ㣬����ͽ�`from`�ƶ�����һ�����С�
* ��Ŀ���Ѿ�˵����֤��·ͼ���γ�һ��������ѭ������·�����Դ���һ�����г������ս����һ������ô��` String from = paths.get(0).get(0); `��
* ���������ĳ�������ܵ������һ�����У�����ʹ��һ��`Map<String, String> map`����Ϊ�������У�ֵΪ������С��������`map`ʹ��`Map<String, String> prepare(List<List<String>> paths)`��
    * ���ǣ�������û�п��Ե���ĳ��о���`!map.containsKey(from)`����ʱ`return from`��
    * ����ͽ�`from`�ƶ�����һ�����С�`from = map.get(from);`��
* `while`ѭ��һ�����������Ϊ��Ŀ˵�ˣ�һ�����յ㡣
* ʱ�临�Ӷ������Եģ��ռ临�Ӷ�Ҳ�����Եġ�

���н����

* 2ms

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз