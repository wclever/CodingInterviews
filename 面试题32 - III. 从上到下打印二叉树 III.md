## [面试题32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```

**提示：**

1. `节点总数 <= 1000`

**bfs**

```java
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        LinkedList<TreeNode> queue = new LinkedList<>();
        boolean flag = true;
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            LinkedList<Integer> tmp = new LinkedList<>();
            while(size > 0){
                TreeNode n = queue.poll();
                if(flag) tmp.addLast(n.val);
                else tmp.addFirst(n.val);
                if(n.left != null) queue.offer(n.left);
                if(n.right != null) queue.offer(n.right);
                size--;
            }
            res.add(tmp);
            flag = !flag;
        }
        return res;
    }
```

**dfs**

```java
    List<List<Integer>> reses = new ArrayList<>();
    public List<List<Integer>> levelOrder(TreeNode root) {       
        recur(root, 0);
        return reses;
    }
    void recur(TreeNode root, int level) {
        if (root == null) return;
        if (reses.size() == level) reses.add(new LinkedList<Integer>());
        LinkedList<Integer> res = (LinkedList<Integer>) reses.get(level);
        if ((level & 1) == 0) res.addLast(root.val);
        else res.addFirst(root.val);
        recur(root.left, level+1);
        recur(root.right, level+1);
    }
```

