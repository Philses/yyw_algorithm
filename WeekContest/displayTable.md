# 5389. ���չʾ��
### ԭ��
����һ������ orders����ʾ�ͻ��ڲ�������ɵĶ�����ȷ�е�˵�� `orders[i]=[customerNamei,tableNumberi,foodItemi]` ������` customerNamei` �ǿͻ���������`tableNumberi` �ǿͻ����ڲ��������ţ���` foodItemi` �ǿͻ���Ĳ�Ʒ���ơ�

���㷵�ظò����� ���չʾ�� �������ű��У����е�һ��Ϊ���⣬���һ��Ϊ�������� ��Table�� ������ÿһ�ж��ǰ���ĸ˳�����еĲ�Ʒ���ơ�������ÿһ���е������ʾÿ�Ų�����������Ӧ��Ʒ��������һ��Ӧ�����Ӧ�����ţ�����������д�µ��Ĳ�Ʒ������

ע�⣺�ͻ��������ǵ��չʾ���һ���֡����⣬���е�������Ӧ�ð����������������С�


ʾ�� 1��

���룺orders = [["David","3","Ceviche"],["Corina","10","Beef Burrito"],["David","3","Fried Chicken"],["Carla","5","Water"],["Carla","5","Ceviche"],["Rous","3","Ceviche"]]
�����[["Table","Beef Burrito","Ceviche","Fried Chicken","Water"],["3","0","2","1","0"],["5","0","1","0","1"],["10","1","0","0","0"]] 
���ͣ�
���չʾ��������ʾ��
Table,Beef Burrito,Ceviche,Fried Chicken,Water
3    ,0           ,2      ,1            ,0
5    ,0           ,1      ,0            ,1
10   ,1           ,0      ,0            ,0
���ڲ��� 3��David ���� "Ceviche" �� "Fried Chicken"���� Rous ���� "Ceviche"
������ 5��Carla ���� "Water" �� "Ceviche"
���� 10��Corina ���� "Beef Burrito" 

ʾ�� 2��

���룺orders = [["James","12","Fried Chicken"],["Ratesh","12","Fried Chicken"],["Amadeus","12","Fried Chicken"],["Adam","1","Canadian Waffles"],["Brianna","1","Canadian Waffles"]]
�����[["Table","Canadian Waffles","Fried Chicken"],["1","2","0"],["12","0","3"]] 
���ͣ�
���ڲ��� 1��Adam �� Brianna ������ "Canadian Waffles"
������ 12��James, Ratesh �� Amadeus ������ "Fried Chicken"

ʾ�� 3��

���룺orders = [["Laura","2","Bean Burrito"],["Jhon","2","Beef Burrito"],["Melissa","2","Soda"]]
�����[["Table","Bean Burrito","Beef Burrito","Soda"],["2","1","1","1"]]

��ʾ��

```
1 <= orders.length <= 5 * 10^4
orders[i].length == 3
1 <= customerNamei.length, foodItemi.length <= 20
customerNamei �� foodItemi �ɴ�СдӢ����ĸ���ո��ַ� ' ' ��ɡ�
tableNumberi �� 1 �� 500 ��Χ�ڵ�������
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/display-table-of-food-orders-in-a-restaurant)��https://leetcode-cn.com/problems/display-table-of-food-orders-in-a-restaurant

### �ⷨ
```java
public class displayTable {
    public List<List<String>> displayTable(List<List<String>> orders) {
        Set<String> foodName = new HashSet<>();
        Set<String> tableID = new HashSet<>();
        Map<String, Map<String, Integer>> map = new HashMap<>(); // ׿�Ŷ�Ӧ���� ������һ��map
        buildMap(orders, foodName, tableID, map);

        String[] foods = getSortedArr(foodName, null);
        String[] tables = getSortedArr(tableID, Comparator.comparingInt(x -> Integer.parseInt((String) x)));

        List<List<String>> res = new ArrayList<>();

        List<String> line1 = new ArrayList<>();
        line1.add("Table");
        for (String s : foods)
            line1.add(s);
        res.add(line1);

        for (String table : tables) {
            List<String> line = new ArrayList<>();
            line.add(table);
            Map<String, Integer> order = map.get(table);
            for (String s : foods) {
                line.add(String.valueOf(order.getOrDefault(s, 0)));
            }
            res.add(line);
        }
        return res;
    }

    private void buildMap(List<List<String>> orders, Set<String> foodName,
                          Set<String> tableID, Map<String, Map<String, Integer>> map) {
        for (List<String> order : orders) {
            String food = order.get(2);
            foodName.add(food);
            String tableNum = order.get(1);
            tableID.add(tableNum);
            if (!map.containsKey(tableNum))
                map.put(tableNum, new HashMap<>());
            Map<String, Integer> foodCount = map.get(tableNum);
            foodCount.put(food, foodCount.getOrDefault(food, 0) + 1);
        }
    }

    private String[] getSortedArr(Set<String> items, Comparator c) {
        String[] foods = new String[items.size()];
        int index = 0;
        for (String food : items) {
            foods[index++] = food;
        }
        if (c != null)
            Arrays.sort(foods, c);
        else
            Arrays.sort(foods);
        return foods;
    }
}
```
˼·������
* ����������Ŀ�ͻᷢ������������ˣ��������ݽṹ��Ҫ���ص����ݽṹ�����鷳������ʵҪ�����������ģ�⡣������?��������ʱ��ͼ�飬�����������������ĸ��࣬���߰���ģ�
* ����ע������ĸ�ʽ��
    * ����һ�У���Ҫ�Բ�����Ӧ���ַ������ֵ������У��������ǵ���Ҫ֪���˵��г�������Щ�ˣ���Ҫ�Բ�������
    * ����һ�У���Ҫ�����Ž��������������ַ���������Ҫ�����ֽ�������Ҳ��Ҫ֪����������Щ׿�š�
    * �����Ҫͳ��ÿһ��ÿһ���˵��˼��֣�û�����0��
* ��������ĸ�ʽ��ѡ����ʵ����ݽṹ��
    * ÿһ����Ҫ���ɲ��ף�����ʹ��`Map<String, Map<String, Integer>> map`��������Ϊ�����˵�Ϊֵ���˵�Ҳ��һ����ֵ�ṹ������Ϊ��������Ϊֵ��
    * ���ڻ���Ҫ֪�������˶����ֲˣ��������š��ֱ�ʹ��`Set<String> foodName, tableID`����¼�������¼��û��˳��ģ������Ҫ�������Ժ���ת��Ϊ����������
* ��������`void buildMap`��������ɢ�Ĳ˵����������������ŵļ��ϣ����ҽ���ɢ�Ĳ˵�������Ϊ�����ϵ�һ�𣬲��ϸ��¸�������˵�������
* ��������`String[] getSortedArr(Set<String> items, Comparator c)`���ڶԲ�������������
    * �ڶ���������Ϊ�˷�������������Ϊ���Ÿ������ַ������ͣ�����Ҫ��������˳�����򣬲�ʹ���Զ����`Comparator c`�ʹ��ˣ��Զ���Ϊ`Comparator.comparingInt(x -> Integer.parseInt((String) x))`
* ׼��������ɣ�������ͷ��"table" �����ֵ���Ĳ���`for (String s : foods)`����Ȼ������` for (String table : tables)`���ɱ���ÿһ�У�ͨ���������õ�ͳ���˸����˳��ִ�����map��Ȼ���ղ����ֵ����ȡ������û�г��ֵ�����Ϊ0��

���н����

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз