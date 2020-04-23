# 235. �����������������������
### ԭ��
����һ������������, �ҵ�����������ָ���ڵ������������ȡ�

�ٶȰٿ�������������ȵĶ���Ϊ���������и��� T ��������� p��q������������ȱ�ʾΪһ����� x������ x �� p��q �������� x ����Ⱦ����ܴ�һ���ڵ�Ҳ���������Լ������ȣ�����

���磬�������¶���������:  root = [6,2,8,0,4,7,9,null,null,3,5] 

ʾ�� 1:
����: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
���: 6 
����: �ڵ� 2 �ͽڵ� 8 ��������������� 6��

ʾ�� 2:
����: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
���: 2
����: �ڵ� 2 �ͽڵ� 4 ��������������� 2, ��Ϊ���ݶ�������������Ƚڵ����Ϊ�ڵ㱾��


˵��:
���нڵ��ֵ����Ψһ�ġ�
p��q Ϊ��ͬ�ڵ��Ҿ������ڸ����Ķ����������С�

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree)��https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree

### 3�ֽⷨ
##### 1.�����ͨ���������������ҵĵ�һ�⣩
```java
private TreeNode res;
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        res = null;
        if(q.val > p.val)
            contains(root, p, q);
        else
            contains(root, q, p);
        return res;
    }

    private boolean contains(TreeNode x, TreeNode p, TreeNode q){
        if(x == null) return false;
        if(x.val < p.val)
            return contains(x.right, p, q);
        if(x.val > q.val)
            return contains(x.left, p, q);
        boolean leftCon = contains(x.left, p, q);
        boolean rightCon = contains(x.right, p, q);
        if((x == p && rightCon) || (x == q && leftCon) || (leftCon && rightCon)) {
            res = x;
            return true;
        }
        return x == p || x == q || leftCon || rightCon;
    }
```
˼·������
* ����[236. �������������������](https://github.com/ustcyyw/yyw_algorithm/blob/master/medium/Tree/lowestCommonAncestor.md)��һ�����Ѿ�����ͨ�����������˽������������������Ķ�������Ҳ������ʹ�����������������������Ƶ�˼·�����
* �������`p,q`������`p.val < q.val`�������ڽ��`x`��xΪ`p,q`������������Ƚ�㣬���ҽ����������������
    * xΪq��x���������ְ���p
    * xΪp��x���������ְ���q
    * x�����������������ֱ����p��q��
* Ϊʲôֻ������������������������룬���x����p��q������������Ƚ�㣬���������壺
    * x���ǹ������Ƚڵ㣬��xΪ��������ͬʱ����p��q��
    * x�ǹ������Ƚڵ㣬����������ģ���ôx����������ֻ������֮һͬʱ����p��q��
    * �����������������ʣ��������˵�����������
* ����������Ҫ�ж���ĳ�����Ϊ�������Ƿ���p��q֮һ�����庯��`boolean contains(TreeNode x, TreeNode p, TreeNode q)`���涨`p.val < q.val`�������ں����ڲ����ǻ���Ҫ�жϽ��x�Ƿ�������������Ƚ�㡣
    * �ݹ����������`x == null`����Ȼ��������p��q������`false`
    * ���`x.val < p.val`��x��ֵ��p��q��ֵ��С����ô��xΪ���������Ƿ����p��q֮һ������Ҫȥ���������ֲ���`return contains(x.right, p, q);`�����`x.val > q.val`��ͬ��`return contains(x.left, p, q);`
    * �ݹ����`boolean leftCon = contains(x.left, p, q); `�õ��������Ƿ���p��`boolean rightCon = contains(x.right, p, q);`�õ��������Ƿ���q��
    * �������һ��ʼ˵���������`(x == p && rightCon) || (x == q && leftCon) || (leftCon && rightCon)`�����ҵ�����������ӽڵ�`res = x;`��������xΪ�������ܰ���p��q������`true`��
    * �������xΪq����p��������������ֻ����һ����p��q������true�����򷵻�false��` return x == p || x == q || leftCon || rightCon;`��
    * ע�����`res`����ֵ��һ�Σ�Ȼ�󷵻ؽ����p��q�����ڰ���������������У�������ĵݹ������`leftCon`��`rightCon`ֻ����һ��Ϊtrue�����������㲻�����q����q�����Ա���ÿ�����Ĺ����У�`res`�ĸ�ֵֻ����һ�Σ�����Ҫ�ҵ�����������Ƚ�㡣
* ����������ֻ��Ҫ��`res`��ֵΪ`null`��Ȼ�����p��q��ֵ����`contains()`��������֤�ڶ���������p��q�н�С�Ľ�㣬Ȼ�󷵻�`res`���ɡ�
* ʱ�临�Ӷ�Ϊ$O(n)$���ռ临�Ӷ������߳����ȡ�

���н����
* ִ����ʱ :7 ms, ������ Java �ύ�л�����78.21%���û�
* �ڴ����� :41.9 MB, ������ Java �ύ�л�����5.02%���û�

##### 2.����BST��������
```java
public TreeNode lowestCommonAncestor3(TreeNode root, TreeNode p, TreeNode q) {
        if(p.val > q.val) return find(root, q, p);
        else return find(root, p, q);
    }

    private TreeNode find(TreeNode x, TreeNode p, TreeNode q){
        if(x == p || x == q) return x;
        if(p.val < x.val && q.val > x.val) return x;
        else if(q.val < x.val) return find(x.left, p, q);
        return find(x.right, p ,q);
    }
```
˼·������
* ���������������������������������ʡ�
* ����`TreeNode find(TreeNode x, TreeNode p, TreeNode q)`�ҵ���xΪ����������p��q������������Ƚ�㡣�涨��`p.val < q.val`��
    * ���x����p����q��������Ŀ�趨��p��qһ���й������Ƚڵ㣬��ô��Ȼ��ʱx��������������Ƚ�㡣
    * ���`p.val < x.val && q.val > x.val`��p��x����������q��x������������ôx���ӽ�㲻����ͬʱ����p��q������x��������������Ƚ�㡣
    * ���`q.val < x.val`��˵��p��q����x���������У�x�ǹ������Ƚ�㣬����������ģ�����ȥx�����������������`return find(x.left, p, q)`��
    * ���򣬾��Ƕ�Ӧ��`q.val > x.val`�������˵��p��q����x��������������ȥx�����������������`return find(x.right, p, q)`��
* �������У�ע��涨`p.val < q.val`�����Ե�`p.val > q.val`������`find(root, q, p)`�����򷵻�` find(root, p, q);`
* ʱ�临�Ӷ�Ϊ$O(n)$���Խ�����һ�α������ռ临�Ӷ������߳����ȡ�

���н����
* ִ����ʱ :6 ms, ������ Java �ύ�л�����100.00%���û�
* �ڴ����� :41.1 MB, ������ Java �ύ�л�����100.00%���û�

##### 3.�ٷ����
```java
public TreeNode lowestCommonAncestor2(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val > p.val && root.val > q.val)
            return lowestCommonAncestor2(root.left, p, q);
        if(root.val <p.val && root.val < q.val)
            return lowestCommonAncestor2(root.right, p, q);
        return root;
    }
```
˼·������
* �뷽��2һ�£�����������д�ĸ����~

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз